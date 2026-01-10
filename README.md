# Drone Detection - YOLOv8

Hệ thống phát hiện drone realtime sử dụng **Ultralytics YOLOv8** với tối ưu hóa cho CPU.

## Demo

![Detection Demo](outputs/detected_video.gif)

_Video demo: Phát hiện drone realtime với bounding boxes_

## Tính năng

- Phát hiện drone realtime với YOLOv8
- Tối ưu hiệu suất: Frame skipping + resize thông minh (640x640)
- Hiển thị FPS realtime
- Lưu video kết quả với bounding boxes
- Hỗ trợ đa luồng (multithread) để tăng tốc
- Hỗ trợ cả GPU (CUDA) và CPU

## Cấu trúc

```
drone-detection/
├── models/              # YOLOv8 model (.pt)
├── demo_videos/         # Video input
├── outputs/             # Video detection kết quả
├── src/
│   ├── detect.py       # Single-thread
└── requirements.txt
```

## Sử dụng

```bash
# Single-thread
python src/detect.py
