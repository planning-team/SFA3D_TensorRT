# Benchmarking SFA3D

## RTX 2080Ti
Benchmarking Environment:
```
 python==3.6.5
 cuda==11.2
 cudnn==8
 torch==1.10.1+cu111
 tensorrt==8.2.2.1
```
- RTX 2080 Ti

|   Backend    |  Precision  | Mem (GB) | Latency (ms) |  Inference FPS  |  
| :----------: | :-----: | :------: | :------------: | :----: |
|   PyTorch    |   FP32   |   1.6    |      10.96      | 92
|   TensorRT   |   FP32   |   2.6    |       4.65      | 214
|   TensorRT   |   FP16   |   2.2    |       2.30      | 424
  

## Jetson Xavier AGX
Benchmarking Environment:
```
 python==3.6.9
 cuda==10.2
 cudnn==8
 torch==1.10.1
 tensorrt==8.0.1.1
```

|   Backend    |  Precision  | Mem (GB) | Latency (ms) |  Inference FPS  |  
| :----------: | :-----: | :------: | :------------: | :----: |
|   PyTorch    |   FP32   |   1.0    |      48.75      | 20.5
|   TensorRT   |   FP32   |   1.3    |       1.98      | 500
|   TensorRT   |   FP16   |   1.1    |       2.69      | 370


P.S. : Overall TensorRT FP16 is faster than FP32 on AGX. The time taken for stream synchronisation makes up for the fast inference time of TensorRT FP32. Numbers including the sync time as well; TRT FP32 -> 24 FPS, TRT FP16 -> 60 FPS. While there was no such difference on RTX 2080 Ti.