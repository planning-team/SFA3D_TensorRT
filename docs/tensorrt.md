# TensorRT
The core of NVIDIA TensorRT is a C++ library that facilitates high-performance inference on NVIDIA graphics processing units (GPUs). TensorRT takes a trained network, which consists of a network definition and a set of trained parameters, and produces a highly optimized runtime engine that performs inference for that network.
This doc has instructions for tensorrt setup, conversion and inference.

## Setup
### TensorRT in docker
- Pull TensorRT docker container from [nvidia](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/tensorrt).
```bash
 $ docker pull nvcr.io/nvidia/tensorrt:22.02-py3
```

- Run TensorRT docker container with SFA3D repo.
```bash
 $ docker run --gpus all -it -v /home/path_to_sfa3d_dir:/home nvcr.io/nvidia/tensorrt:22.01-py3
```

- Install SFA3D requirements.
```bash
 $ pip install -r requirements.txt
```

### Install via pip
```bash
 $ pip install pycuda
 $ pip install nvidia-tensorrt --index-url https://pypi.ngc.nvidia.com
```

## PyTorch to TensorRT
- Convert PyTorch model to TensorRT FP32 model via ONNX.
```bash 
 $ python export.py --pretrained_path "pytorch_model_path" --onnx_path "onnx_model_path" --trt_path "tensorrt_model_path"
```

- Use flag ```--fp16``` to quantize TensorRT model.
```bash
 $ python export.py --pretrained_path "pytorch_model_path" --onnx_path "onnx_model_path" --trt_path "tensorrt_model_path" --fp16
```

## Inference with TensorRT model
- Inference with TensorRT FP32 model.
```bash
 $ python infer_tensorrt.py --trt_path "tensorrt_model_path"
```

- Use flag ```--fp16``` if inference using qunatized TensorRT FP16 model
```bash
 $ python infer_tensorrt.py --trt_path "tensorrt_model_path" --fp16
```
