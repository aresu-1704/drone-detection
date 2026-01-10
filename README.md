# 🚁 Drone Detection - YOLOv8

Hệ thống phát hiện drone realtime sử dụng **Ultralytics YOLOv8** với tối ưu hóa hiệu suất cho CPU.

## ✨ Tính năng

- ✅ Phát hiện drone realtime với YOLOv8
- ⚡ Tối ưu hiệu suất với frame skipping
- 🎯 Resize thông minh (640x640) để tăng tốc độ
- 📊 Hiển thị FPS realtime
- 💾 Lưu video kết quả với bounding boxes
- 🧵 Hỗ trợ đa luồng (multithread) để tăng FPS
- 🎮 Hỗ trợ GPU (CUDA) hoặc CPU

## 📁 Cấu trúc Project

```
drone-detection/
├── models/                  # Model YOLO (.pt files)
│   └── drone_detect_yolov8.pt
├── demo_videos/             # Video input để test
│   └── demo.mp4
├── outputs/                 # Video kết quả sau khi detect
│   └── detected_video.mp4
├── src/                     # Source code
│   ├── detect.py           # Script detection cơ bản (single-thread)
│   └── detect_multithread.py  # Script với đa luồng (nhanh hơn)
├── requirements.txt         # Python dependencies
└── README.md
```

## 🚀 Cài đặt

### 1. Clone repo

```bash
git clone <repo-url>
cd drone-detection
```

### 2. Tạo virtual environment

```bash
python -m venv .venv
.venv\Scripts\activate  # Windows
# hoặc
source .venv/bin/activate  # Linux/Mac
```

### 3. Cài đặt dependencies

```bash
pip install -r requirements.txt
```

### 4. Chuẩn bị model

Đặt file model YOLOv8 (`.pt`) vào thư mục `models/`. Script sẽ tự động detect file `.pt` đầu tiên tìm thấy.

## 📖 Sử dụng

### Cơ bản (Single-thread)

```bash
python src/detect.py
```

**Cấu hình trong `detect.py`:**

```python
VIDEO_PATH = "demo_videos/demo.mp4"    # Video input
OUTPUT_PATH = "outputs/detected_video.mp4"  # Video output
CONF_THRESHOLD = 0.3    # Ngưỡng confidence (0-1)
IMG_SIZE = 640          # Kích thước detection (640x640)
FRAME_SKIP = 3          # Skip 3 frames (detect mỗi 4 frame)
```

### Tối ưu (Multi-thread) - Khuyến nghị

```bash
python src/detect_multithread.py
```

Script này sử dụng 3 threads riêng biệt:

- **Thread 1**: Đọc frame từ video (I/O)
- **Thread 2**: Detection (CPU/GPU)
- **Thread 3**: Ghi video output (I/O)

**→ Tăng FPS ~30-50% so với single-thread**

## ⚙️ Tối ưu hiệu suất

### Frame Skipping

Để tăng FPS, tăng giá trị `FRAME_SKIP`:

```python
FRAME_SKIP = 3   # FPS ~11 (detect mỗi 4 frame)
FRAME_SKIP = 7   # FPS ~20 (detect mỗi 8 frame)
FRAME_SKIP = 10  # FPS ~28 (detect mỗi 11 frame)
```

### Giảm kích thước detection

```python
IMG_SIZE = 640   # Chất lượng cao, chậm hơn
IMG_SIZE = 416   # Cân bằng
IMG_SIZE = 320   # Nhanh nhất, độ chính xác thấp hơn
```

## 🎥 Kết quả Demo

### Cách 1: Embed video trực tiếp (GitHub)

Kéo thả video từ `outputs/` vào GitHub Issue/PR, copy link và paste vào README:

```
https://github.com/user-attachments/assets/your-video-link.mp4
```

### Cách 2: GIF Preview

Chuyển video sang GIF và embed:

```bash
# Sử dụng ffmpeg để tạo GIF
ffmpeg -i outputs/detected_video.mp4 -vf "fps=10,scale=640:-1" outputs/demo.gif
```

Sau đó trong README:

```markdown
![Demo Detection](outputs/demo.gif)
```

### Cách 3: Link đến video file

```markdown
[📹 Xem video kết quả](outputs/detected_video.mp4)
```

### Cách 4: YouTube/External hosting

Upload video lên YouTube và embed:

```markdown
[![Demo Video](https://img.youtube.com/vi/VIDEO_ID/0.jpg)](https://www.youtube.com/watch?v=VIDEO_ID)
```

## 📊 Performance Benchmark

Tested trên video 576x1024 @ 30fps, 482 frames:

| Script                      | FPS    | Thời gian xử lý | Frame Skip |
| --------------------------- | ------ | --------------- | ---------- |
| detect.py (CPU)             | 11 FPS | ~43s            | 3          |
| detect.py (CPU)             | 20 FPS | ~24s            | 7          |
| detect_multithread.py (CPU) | 29 FPS | ~17s            | 10         |

## 🛠️ Troubleshooting

### Lỗi: "Không tìm thấy file .pt"

Đảm bảo có file model `.pt` trong thư mục `models/`:

```bash
ls models/
# Phải có file .pt như: drone_detect_yolov8.pt
```

### Video output bị mờ/nhòe

Tăng `IMG_SIZE` lên 640 hoặc cao hơn trong config.

### FPS quá thấp

1. Tăng `FRAME_SKIP`
2. Sử dụng `detect_multithread.py`
3. Giảm `IMG_SIZE` xuống 416 hoặc 320

## 📝 Requirements

- Python 3.8+
- OpenCV
- Ultralytics YOLOv8
- PyTorch (CPU hoặc CUDA)
- Numpy

Xem đầy đủ trong `requirements.txt`

## 🤝 Contributing

Pull requests are welcome!

## 📄 License

MIT License

---

**Made with ❤️ using Ultralytics YOLOv8**
