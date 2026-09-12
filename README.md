# Hệ Thống Xe Trinh Sát Nông Nghiệp Tự Hành (MicroScout-AI)

[![VietFuture 2026](https://img.shields.io/badge/Project-VietFuture%202026-brightgreen)](https://github.com/denzxje157/hethongxetrinhsat)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.8.0%2B-red.svg)](https://opencv.org/)
[![GPS RTK](https://img.shields.io/badge/GPS%20RTK-Centimeter%20Accuracy-orange.svg)]()

> **Dự án khởi nghiệp số hóa đồng rẫy: Hệ thống xe trinh sát lập bản đồ nhiệt cỏ dại & tình trạng sức khỏe cây trồng theo luống bằng Edge AI và GPS RTK độ chính xác Centimet.**

---

## 🌟 Tổng Quan Dự Án

Hệ thống **MicroScout-AI** là giải pháp xe tự hành cỡ nhỏ luồn lách qua các rãnh luống hẹp (60–80cm) của các loại cây trồng quy mô lớn (ngô, bắp, mía, sắn, đậu tương...). Xe đảm nhận nhiệm vụ trinh sát lập bản đồ dịch hại khép kín:

1. **Quét thị giác tầm thấp 120 FPS:** Cụm 2 camera góc rộng bên sườn chụp liên tục sát gốc cây mà không bị rung nhòe hình ảnh.
2. **Trí tuệ nhân tạo biên (Edge AI Jetson Orin):** Nhận diện, phân loại cỏ dại (cỏ lồng vực, cỏ mần trầu...) và sâu bệnh (sâu keo mùa thu, đốm lá lớn) trong thời gian thực.
3. **Định vị chính xác Centimet (GPS RTK Holybro NEO-F9P):** Khóa tọa độ các ổ sâu cỏ với sai số dưới 2cm.
4. **Bản đồ nhiệt vệ tinh Google Hybrid (GIS Heatmap):** Tự động tổng hợp dữ liệu thành các quầng nhiệt trực quan trên ảnh vệ tinh thực tế của lô rẫy.
5. **Dẫn đường người nông dân xử lý cục bộ:** Bác nông dân mở ứng dụng trên điện thoại, la bàn GPS chỉ đường đi thẳng tới đúng vị trí để nhổ cỏ hoặc xịt thuốc cục bộ, **tiết kiệm 70% – 80% lượng thuốc bảo vệ thực vật**.

---

## 🏗️ Kiến Trúc Hệ Thống & Module Cam-Controller

Hệ thống thu thập và xử lý dữ liệu hình ảnh được xây dựng trên **4 thư viện cốt lõi**:

- **`pygrabber` (>=0.2):** Quét danh sách thiết bị DirectShow FilterGraph trên Windows, tự động lọc bỏ webcam laptop và nhận diện đúng 2 camera UGREEN rời.
- **`comtypes` (>=1.1.7):** Giao tiếp nhị phân với Windows COM API để cố định ID phần cứng, tránh bị đảo cổng USB.
- **`opencv-python` (>=4.8.0):** Thu nạp luồng camera 1080p @ 60 FPS đa luồng (Multi-threaded), xuất chuỗi Frame ảnh JPG và ghi video MP4.
- **`numpy` (>=1.24.0):** Thao tác ma trận điểm ảnh tốc độ cao trong RAM, ghép ảnh xem trực tiếp (`np.hstack`) chỉ mất 1.5ms.

### 📁 Quy trình lưu trữ tự động:
- `recordings/left/`: Toàn bộ Frame ảnh (`frame_000001.jpg...`) và Video MP4 hoàn chỉnh của Camera Trái.
- `recordings/right/`: Toàn bộ Frame ảnh (`frame_000001.jpg...`) và Video MP4 hoàn chỉnh của Camera Phải.
- `recordings/snapshots/`: Cặp ảnh tĩnh phục vụ huấn luyện mô hình YOLO AI và hiệu chuẩn Stereo 3D.

---

## 📂 Cấu Trúc Mã Nguồn

```text
hethongxetrinhsat/
├── index.html                           # Ứng dụng Web GIS mô phỏng bản đồ nhiệt vệ tinh thời gian thực
├── slide_presentation.html              # Bộ Slide Canva Pitch Deck VietFuture 2026 (10 slide)
├── slide_quy_trinh_nong_dan.html        # Slide quy trình 4 bước người nông dân sử dụng thiết bị
├── slide_cam_workflow_don_gian.html     # Slide sơ đồ trực quan luồng xử lý Cam-Controller 60 FPS
├── slide_cam_pipeline.html              # Slide chi tiết kỹ thuật chuyên sâu module camera
├── slide_data_pipeline.md               # Giáo án bài giảng Slide chuẩn Marp Markdown
├── flow_diagram_preview.html            # Sơ đồ khối quy trình vận hành hệ thống
├── XeTrinhSatAI_10anh/                  # 10 bản vẽ 3D chi tiết mô hình xe trinh sát
│   ├── 01_tong_the.png
│   ├── 02_goc_sau.png
│   ├── 06_chu_thich.png
│   ├── 10_chi_tiet_camera.png
│   └── ...
├── assets/evidence/                     # Ảnh nông nghiệp thực tế do xe thu thập
│   ├── 01_co_long_vuc.jpg               # Cỏ lồng vực mọc giữa luống cây
│   ├── 02_sau_keo_can_la.jpg            # Sâu keo mùa thu cắn rách phiến lá
│   ├── 03_co_man_trau_goc.jpg           # Cỏ mần trầu quanh gốc thân cây
│   └── 04_benh_dom_la_ngo.jpg           # Bệnh nấm đốm lá ngô hoại tử
├── Bao_Cao_Chi_Tiet_Du_An_AgriTech.docx # Báo cáo chi tiết kỹ thuật dự án
├── Bao_gia_thiet_bi_du_an_AgriTech...   # Dự toán ngân sách & danh mục thiết bị (BOM)
└── README.md                            # Tài liệu hướng dẫn dự án
```

---

## 🚀 Hướng Dẫn Chạy Thử Nghiệm

### 1. Mở Web App Bản Đồ Nhiệt Vệ Tinh (GIS Heatmap)
Mở trực tiếp file `index.html` bằng bất kỳ trình duyệt web nào (Chrome, Edge, Firefox, Cốc Cốc):
- Tự động nhận diện tọa độ thực tế qua **GPS Geolocation**.
- Cho phép chạm chuột vào bất kỳ thửa ruộng nào để đặt ô quét luống.
- Bấm **"Quét Bản Đồ Nhiệt"** để xem xe chạy ziczac theo luống và hiển thị các quầng nhiệt điểm nóng.

### 2. Trình Chiếu Slide Thuyết Trình
- Mở `slide_quy_trinh_nong_dan.html` để thuyết minh quy trình thực tế cho người dân và ban giám khảo.
- Mở `slide_cam_workflow_don_gian.html` để trình bày sơ đồ kỹ thuật thu thập dữ liệu 60 FPS.
- Dùng phím mũi tên `←` / `→` để chuyển trang, hỗ trợ nút **"Lưu PDF / In"** xuất file 1 chạm.

---

## 👥 Đội Ngũ Phát Triển
- **Dự án:** MicroScout-AI — Xe Trinh Sát Lập Bản Đồ Cỏ Dại & Sức Khỏe Cây Trồng
- **Tác giả:** denzxje157 (`minhminh887701@gmail.com`)
- **Bản quyền:** © 2026 MicroScout-AI • Make in Vietnam
