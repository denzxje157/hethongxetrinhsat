# TÀI LIỆU MÔ TẢ SẢN PHẨM & KỸ THUẬT DỰ ÁN (PRODUCT & TECHNICAL SPECIFICATION)

## 1. Thông tin chung
* [cite_start]**Tên dự án:** Hệ thống AI phát hiện cỏ dại & lập bản đồ ruộng mía hàng kép[cite: 2].
* [cite_start]**Phạm vi ứng dụng:** Ruộng mía hàng kép 0.4m + 1.4m tại Tây Ninh, Việt Nam[cite: 2].
* [cite_start]**Cập nhật cấu hình:** Tháng 5/2026[cite: 2].

---

## 2. Mục tiêu và Hiệu quả đầu tư (ROI)
Hệ thống được thiết kế nhằm tối ưu hóa quá trình canh tác nông nghiệp thông minh, mang lại hiệu quả rõ rệt:
* [cite_start]Giảm khoảng **42%** lượng thuốc trừ cỏ (tương đương ~1.5 kg a.i./ha/vụ)[cite: 118].
* [cite_start]Giảm khoảng **61%** chi phí nhân công làm cỏ (tương đương ~24 man-day/ha/vụ)[cite: 118].
* [cite_start]Thời gian hoàn vốn ước tính ở mức **~18 tháng** cho quy mô 50 hecta[cite: 118].
* [cite_start]Tuổi thọ vòng đời hệ thống dự kiến từ **3–5 năm** với lịch bảo trì định kỳ[cite: 118].

---

## 3. Các tính năng cốt lõi (Core Features)
* [cite_start]**Nhận diện AI Thời gian thực:** Khả năng chạy mô hình suy luận (inference) YOLOv11-seg với tốc độ trên 30 FPS[cite: 39], phát hiện và cắt lớp (segmentation) cỏ dại ngay cả khi máy cày đang di chuyển.
* [cite_start]**Thị giác máy tính Xuyên màn đêm (24/7):** Sử dụng hệ thống chiếu sáng chủ động NIR (hồng ngoại cận 850nm) với chế độ nháy chớp (strobe pulse ~20µs)[cite: 29]. [cite_start]Kết hợp với kính lọc băng thông[cite: 27], hệ thống loại bỏ hoàn toàn nhiễu ánh sáng từ môi trường tự nhiên.
* [cite_start]**Lập bản đồ Tọa độ Siêu chuẩn (Precision Mapping):** Sai số định vị cực thấp ở mức ±2–3 cm nhờ module ZED-F9P[cite: 49]. [cite_start]Tích hợp cảm biến gia tốc (IMU 9-axis) [cite: 55] [cite_start]và cảm biến vòng quay bánh xe (Wheel encoder) để nội suy tọa độ (dead reckoning) khi mất tín hiệu GPS[cite: 59].
* [cite_start]**Giám sát Cloud & Dashboard:** Tọa độ phát hiện (dạng JSON) và video được truyền tải qua chuẩn MQTT và lưu trữ trực tuyến [cite: 103][cite_start], tạo bản đồ nhiệt độ tập trung (heatmap) hiển thị realtime[cite: 108].

---

## 4. Kiến trúc hệ thống và Kỹ thuật phần cứng

### 4.1. Khối Cảm biến Quang học (Nhóm A)
Hệ thống kết hợp đa phổ (Sensor Fusion) để thu thập dữ liệu trong mọi điều kiện thời tiết:
* [cite_start]**Camera RGB:** Module 12.3 MP (Raspberry Pi HQ) góc siêu rộng (FOV 120°), trang bị màn trập Global Shutter để thu thập dữ liệu video HD và huấn luyện mô hình (training dataset)[cite: 18].
* [cite_start]**Camera Hồng ngoại cận (NIR):** Sử dụng 02 module Arducam 1MP băng thông 850nm[cite: 20]. [cite_start]Các camera này đi kèm đèn LED ring chiếu sáng chủ động 20W [cite: 29] [cite_start]và kính lọc bandpass 850nm[cite: 27].
* [cite_start]**Camera Ảnh nhiệt (Thermal LWIR):** Sử dụng FLIR Lepton 3.5 để phân biệt nền đất/thực vật và phát hiện giai đoạn cây trồng bị stress nhiệt[cite: 23].

### 4.2. Khối Xử lý Điện toán Biên (Nhóm B)
* [cite_start]Sử dụng bộ vi xử lý nhúng **NVIDIA Jetson Orin NX 16GB**, cung cấp hiệu năng AI 100 TOPS[cite: 39].
* [cite_start]Dữ liệu đệm offline (lưu trữ video và detection JSON) được quản lý trên ổ cứng SSD NVMe 512GB[cite: 43]. 
* [cite_start]Toàn bộ bo mạch được bảo vệ trong hộp nhôm tản nhiệt chuẩn IP65[cite: 45].

### 4.3. Khối Định vị Không gian & Dẫn đường (Nhóm C)
* [cite_start]**Mạng RTK:** Trạm Rover trên xe và Trạm Base cố định đều sử dụng module u-blox ZED-F9P [cite: 49, 51][cite_start], giao tiếp dữ liệu sửa lỗi qua sóng radio vô tuyến RFD900x (915 MHz) với độ trễ siêu thấp[cite: 53].
* [cite_start]**Sensor Fusion:** Tích hợp IMU 9 trục (ICM-42688-P) [cite: 55] [cite_start]và bộ mã hóa từ tính AS5048A 14-bit đo vòng quay ở trục bánh xe[cite: 59].

### 4.4. Khối Năng lượng & Truyền thông (Nhóm D & E)
* [cite_start]**Nguồn cung cấp:** Hoạt động độc lập nhờ bộ pin LiFePO4 24V/50Ah (lõi CATL) có khả năng cấp nguồn từ 6-8 giờ liên tục[cite: 63]. [cite_start]Các mạch hạ áp DC-DC chia dòng 12V và 5V ổn định cho linh kiện[cite: 65, 67].
* [cite_start]**Truyền thông:** Kết nối Internet đảm bảo bằng modem Quectel EC25-AF chuẩn 4G LTE Cat-12 (Dual SIM failover)[cite: 75]. [cite_start]Trang bị thêm bộ phát WiFi ngoài trời ở bãi đậu xe để tự động đẩy dữ liệu nặng khi thiết bị về bến[cite: 81].

### 4.5. Khối Cơ khí & Chống chịu Môi trường (Nhóm F)
* [cite_start]**Khung chịu lực:** Gắn vào đuôi máy cày bằng khung thép 3-point hitch tương thích thiết bị công nghiệp (John Deere / Kubota)[cite: 85]. [cite_start]Thanh nhôm ngang CNC dùng để cố định anten và cụm camera[cite: 87].
* [cite_start]**Bảo vệ chuẩn IP67:** Các module camera đặt trong vỏ nhôm phay CNC kháng nước, trang bị van cân bằng áp suất (GORE-TEX vent), chống ẩm bằng Silica gel[cite: 89]. [cite_start]Ống kính được bảo vệ bởi kính đậy Sapphire siêu cứng (Mohs 9) [cite: 31] [cite_start]và kính phân cực CPL giảm lóa[cite: 33]. [cite_start]Hệ thống đi dây bằng cáp PUR chịu dầu với đầu nối M12[cite: 95].

---

## 5. Tổng mức đầu tư dự kiến

**Chi phí đầu tư phần cứng & thiết lập ban đầu (CapEx):**
* [cite_start]Khối A (Cụm cảm biến): 9,720,000 VNĐ [cite: 114]
* [cite_start]Khối B (Edge AI Compute): 24,600,000 VNĐ [cite: 114]
* [cite_start]Khối C (Định vị RTK GPS): 11,250,000 VNĐ [cite: 114]
* [cite_start]Khối D (Nguồn điện): 5,780,000 VNĐ [cite: 114]
* [cite_start]Khối E (Truyền thông 4G): 2,550,000 VNĐ [cite: 114]
* [cite_start]Khối F (Cơ khí & Bảo vệ IP67): 9,460,000 VNĐ [cite: 114]
* [cite_start]Khối G (Cloud server tháng đầu + domain): 650,000 VNĐ [cite: 114]
* [cite_start]Khối H (Phần mềm Cloud backend & Field test): Cụ thể, thiết lập Cloud/Dashboard là 6,000,000 VNĐ [cite: 108] [cite_start]và chi phí thực địa 2 ngày là 3,000,000 VNĐ[cite: 110]. [cite_start]*(Ghi chú: Tổng dự toán ban đầu nhóm H theo thiết kế lên tới ~26,000,000 VNĐ [cite: 111]).*

[cite_start]**Chi phí vận hành hàng tháng (OPEX): ~650,000 VNĐ/tháng** [cite: 116]
* [cite_start]Thuê máy chủ ảo VPS AZDIGI (4vCPU/8GB/200GB): 490,000 VNĐ[cite: 116].
* [cite_start]Gói cước SIM data 4G Viettel (30GB): 150,000 VNĐ[cite: 116].
* [cite_start]Gia hạn tên miền .vn (quy tháng): 10,000 VNĐ[cite: 116].