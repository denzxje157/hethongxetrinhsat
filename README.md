# MicroScout-AI | Web App Bản Đồ Nhiệt Vệ Tinh Trinh Sát Nông Nghiệp

[![Web App](https://img.shields.io/badge/Web%20GIS-Live-brightgreen)](https://denzxje157.github.io/hethongxetrinhsat/)
[![Leaflet](https://img.shields.io/badge/Leaflet-1.9.4-blue)](https://leafletjs.com/)
[![Tailwind CSS](https://img.shields.io/badge/TailwindCSS-v3.0-38bdf8)](https://tailwindcss.com/)

> **Ứng dụng Web GIS mô phỏng bản đồ nhiệt trinh sát cỏ dại & tình trạng sức khỏe cây trồng theo luống bằng ảnh vệ tinh Google Hybrid và định vị GPS thực tế.**

---

## 🌟 Tính Năng Của Web App

1. **Bản Đồ Vệ Tinh Google Hybrid Sắc Nét:**
   - Hiển thị đầy đủ tên Tỉnh, Huyện, Xã, Quốc lộ trên nền ảnh vệ tinh quang học chi tiết của thửa ruộng.
2. **Tự Động Ghim Vị Trí Hiện Tại (GPS Geolocation):**
   - Tự động nhận diện tọa độ GPS của người dùng khi mở trang web, ghim ô quét và xe trinh sát ngay tại thực địa.
   - Cho phép chạm chuột hoặc chạm tay vào bất kỳ thửa ruộng nào để dời ô quét tự do.
3. **Mô Phỏng Quét Luống Tự Động & Lập Bản Đồ Nhiệt (GIS Heatmap):**
   - Xe robot chạy trinh sát ziczac theo từng luống cây (ngô, mía, sắn...).
   - Hiển thị các đốm nhiệt (Heatmap) nhỏ gọn, nhẹ nhàng, bám sát đúng từng khóm cỏ / cây bị sâu bệnh.
4. **Chỉ Dẫn & Dẫn Đường Cho Bác Nông Dân:**
   - Bấm vào bất kỳ điểm nóng nào trên bản đồ để xem ảnh chụp cận cảnh bằng chứng từ Camera AI (cỏ lồng vực, sâu keo cắn lá, nấm đốm lá).
   - Hướng dẫn lộ trình bước chân chi tiết: *"Bác bước dọc Luống số 2 khoảng 35 bước chân là tới ngay ổ cỏ"*.
5. **Thư Viện Ảnh 3D Xe Trinh Sát:**
   - Bộ sưu tập 10 bản vẽ thiết kế 3D chi tiết của mô hình xe tự hành (`XeTrinhSatAI_10anh/`).

---

## 🚀 Cách Mở Web App

Mở trực tiếp file `index.html` bằng bất kỳ trình duyệt web nào (Google Chrome, Microsoft Edge, Safari, Cốc Cốc):

```bash
# Hoặc chạy nhanh bằng Python HTTP Server:
python -m http.server 8000
# Sau đó truy cập: http://localhost:8000
```

---

## 📂 Cấu Trúc Thư Mục Web

```text
hethongxetrinhsat/
├── index.html              # Trang Web App chính (Giao diện + Bản đồ Leaflet + Logic mô phỏng)
├── XeTrinhSatAI_10anh/     # 10 ảnh mô hình thiết kế 3D xe trinh sát
│   ├── 01_tong_the.png
│   ├── 02_goc_sau.png
│   ├── 10_chi_tiet_camera.png
│   └── ...
├── assets/evidence/        # Ảnh nông nghiệp thực tế do camera AI chụp
│   ├── 01_co_long_vuc.jpg  # Ổ cỏ lồng vực giữa luống
│   ├── 02_sau_keo_can_la.jpg # Sâu keo cắn thủng lá ngô
│   ├── 03_co_man_trau_goc.jpg# Cỏ mần trầu quanh gốc
│   └── 04_benh_dom_la_ngo.jpg# Bệnh nấm đốm lá ngô
├── .gitignore              # Bỏ qua các file tài liệu và file tạm
└── README.md               # Hướng dẫn ứng dụng Web
```

---

## 👥 Tác Giả
- **Dự án:** MicroScout-AI
- **Tác giả:** denzxje157
- **Bản quyền:** © 2026 MicroScout-AI
