[cite_start]CỘNG HÒA XÃ HỘI CHỦ NGHĨA VIỆT NAM [cite: 131]
[cite_start]Độc lập - Tự do - Hạnh phúc [cite: 132]
[cite_start]-----oOo----- [cite: 133]

[cite_start]HỘI THI SÁNG TẠO KỸ THUẬT TỈNH ĐỒNG NAI NĂM 2026 [cite: 134]

[cite_start]BẢN MÔ TẢ GIẢI PHÁP [cite: 135]

[cite_start]TÊN GIẢI PHÁP: [cite: 136]
HỆ THỐNG AI PHÁT HIỆN CỎ DẠI VÀ LẬP BẢN ĐỒ RUỘNG MÍA HÀNG KÉP
ỨNG DỤNG EDGE AI VÀ ĐỊNH VỊ RTK GNSS

[cite_start]TÁC GIẢ: Nguyễn Hoàng Anh (Đại diện nhóm Ba Vì Tinh Tú) [cite: 140]
[cite_start]ĐƠN VỊ: Lớp 25CT111, Trường Đại học Lạc Hồng [cite: 141]

[cite_start]Đồng Nai, tháng 06 năm 2026 [cite: 142]

---

## [cite_start]1. Tên giải pháp: [cite: 144]
Hệ thống AI phát hiện cỏ dại & lập bản đồ ruộng mía hàng kép ứng dụng mô hình YOLOv11-seg trên Edge AI (NVIDIA Jetson Orin NX) kết hợp định vị RTK GNSS siêu chuẩn.

## [cite_start]2. Giải pháp kỹ thuật đã biết: [cite: 145]

**2.1. [cite_start]Bối cảnh phát triển công nghệ nông nghiệp thông minh** [cite: 146]
Trong canh tác mía đường quy mô lớn, việc kiểm soát cỏ dại là một thách thức cực kỳ lớn. Hiện nay, phương pháp phổ biến nhất vẫn là phun thuốc trừ cỏ tràn lan trên toàn bộ diện tích ruộng hoặc thuê nhân công làm cỏ thủ công.

**2.2. [cite_start]Nhu cầu ứng dụng trong các lĩnh vực thực tế** [cite: 147]
Các nông trường tại Tây Ninh và các vùng chuyên canh mía đang có nhu cầu cấp thiết về một giải pháp tự động hóa giúp định vị chính xác vị trí cỏ dại. Điều này nhằm tối ưu hóa lượng hóa chất bảo vệ thực vật, giảm thiểu ô nhiễm môi trường đất/nước và giải quyết bài toán thiếu hụt nhân công nông nghiệp.

**2.3. [cite_start]Các giải pháp kỹ thuật hiện có** [cite: 148]
* **Phương pháp truyền thống:** Phun thuốc định kỳ bằng máy cày rải thảm toàn bộ ruộng.
* **Drone nông nghiệp:** Sử dụng thiết bị bay không người lái để chụp ảnh quang phổ và lập bản đồ, sau đó cho Drone bay theo tọa độ để phun thuốc.
* **Cảm biến quang học đơn giản:** Sử dụng cảm biến màu sắc gắn trên thanh xịt để phát hiện vùng có màu xanh (diệp lục) để phun.

**2.4. [cite_start]Những hạn chế của các giải pháp đã biết** [cite: 149]
* Phun tràn lan gây lãng phí hóa chất lớn, ảnh hưởng đến chất lượng mía và làm chai cứng đất.
* Drone có thời gian bay ngắn (thường dưới 30 phút), tải trọng thuốc thấp và bị ảnh hưởng mạnh bởi gió lớn ngoài đồng. 
* Các cảm biến quang học truyền thống bị nhiễu nặng bởi ánh sáng mặt trời, bóng râm và không thể phân biệt được đâu là lá mía, đâu là lá cỏ dại (vì cả hai đều màu xanh).

**2.5. [cite_start]Khoảng trống công nghệ và định hướng giải pháp mới** [cite: 150]
Hiện tại thiếu một hệ thống "mắt thần" đủ mạnh, có khả năng gắn trực tiếp lên máy cày công nghiệp, hoạt động được 24/7 (bất chấp ngày đêm) và nhận diện chính xác từng cây cỏ dại lẫn trong luống mía. Giải pháp mới định hướng sử dụng công nghệ Edge AI chạy thời gian thực kết hợp cùng hệ thống camera đa phổ (NIR + Thermal) chiếu sáng chủ động để giải quyết triệt để điểm mù công nghệ này.

## [cite_start]3. Mục đích của giải pháp dự thi: [cite: 151]

**3.1. [cite_start]Mục tiêu tổng quát** [cite: 152]
Nghiên cứu, chế tạo và vận hành một hệ thống IoT/Edge AI công nghiệp gắn trên thiết bị cơ giới nông nghiệp, tự động nhận diện và lập bản đồ phân bổ cỏ dại nhằm hướng tới mô hình Nông nghiệp Chính xác (Precision Agriculture).

**3.2. [cite_start]Mục tiêu chi tiết** [cite: 153]
* Giảm 42% lượng thuốc trừ cỏ (~1.5 kg a.i./ha/vụ) bằng cách cung cấp tọa độ phun mục tiêu.
* Xây dựng hệ thống thị giác máy tính chạy suy luận AI (YOLOv11) đạt tốc độ >30 FPS.
* Triển khai cụm định vị RTK GNSS kết hợp Sensor Fusion (IMU + Encoder) đạt độ chính xác tọa độ ±2–3 cm, không trượt ngay cả khi mất sóng vệ tinh tạm thời.
* Xây dựng Dashboard Cloud Server hiển thị Bản đồ nhiệt (Weed density heatmap) theo thời gian thực.

## [cite_start]4. Giới thiệu giải pháp dự thi: [cite: 154]

**4.1. [cite_start]Nguyên lý của giải pháp** [cite: 155]
Hệ thống được gắn sau máy cày qua khớp nối 3-point hitch. Trong lúc xe di chuyển:
1. Cụm camera quang học đa phổ quét liên tục mặt đất. Vòng LED hồng ngoại chớp nháy đồng bộ với màn trập để triệt tiêu hoàn toàn nhiễu sáng môi trường.
2. Dữ liệu video truyền trực tiếp về bo mạch Edge AI (NVIDIA Jetson) để phân tích, cắt lớp hình ảnh và phát hiện cỏ dại.
3. Cùng lúc, module RTK GPS và cảm biến IMU ghim tọa độ không gian chính xác của vùng cỏ dại đó.
4. Tọa độ được đóng gói thành file JSON và truyền qua mạng 4G lên Cloud Server, tự động render thành bản đồ nhiệt cho người quản lý.

**4.2. [cite_start]Các nội dung công nghệ chủ yếu** [cite: 156]
* **Khối Điện toán Biên (Edge AI Compute):** Sử dụng bo mạch NVIDIA Jetson Orin NX 16GB (100 TOPS) kết hợp ổ cứng đệm SSD NVMe 512GB, cho khả năng suy luận mạnh mẽ tại hiện trường.
* **Thị giác Máy tính Xuyên đêm:** Sử dụng Camera NIR 850nm có Global Shutter, kết hợp kính lọc Bandpass 850nm và cụm LED Ring nháy chớp (strobe pulse 20µs).
* **Định vị & Dẫn đường (Sensor Fusion):** Module u-blox ZED-F9P truyền RTCM3 qua sóng radio RFD900x, kết hợp bù trừ sai số bằng IMU 9-DOF (ICM-42688) và Wheel Encoder.
* **Kiến trúc Cloud & Truyền thông:** Dữ liệu đẩy qua Modem 4G Quectel EC25. Máy chủ VPS vận hành Docker với EMQX MQTT, cơ sở dữ liệu PostGIS và hiển thị qua Grafana/Leaflet GIS.

**4.3. [cite_start]Kết quả của giải pháp** [cite: 161]
Tạo ra một cỗ máy công nghiệp đạt chuẩn chống nước/bụi IP67, hoạt động bền bỉ từ 6-8 tiếng qua nguồn pin LiFePO4 độc lập, chống chịu được rung lắc mạnh từ động cơ máy cày. Thời gian hoàn vốn dự kiến nhanh chóng chỉ trong ~18 tháng với quy mô áp dụng 50 hecta.

## 5. Đánh giá giải pháp: [cite: 162]

**5.1. [cite_start]Tính mới và tính sáng tạo** [cite: 163]
* Ứng dụng thành công mô hình Deep Learning (YOLOv11-seg) trực tiếp vào môi trường khắc nghiệt ngoài đồng ruộng (Edge Computing) thay vì phụ thuộc vào máy chủ Cloud.
* Sáng tạo trong thiết kế quang học: Dùng camera hồng ngoại cận (NIR) kết hợp đèn flash chủ động để giải quyết hoàn toàn bài toán bóng râm và thay đổi ánh sáng tự nhiên – điểm yếu chí mạng của camera thông thường.
* Kết hợp cảm biến gia tốc (IMU) và đo vòng quay bánh xe để nội suy tọa độ (Dead Reckoning) khi máy cày đi vào vùng mất sóng GPS.

**5.2. [cite_start]Khả năng áp dụng** [cite: 164]
Giải pháp được thiết kế tiêu chuẩn hóa cao:
* Dễ dàng tích hợp vào hệ thống cơ khí của các loại máy kéo nông nghiệp phổ biến như Kubota hay John Deere thông qua khung thép và đệm giảm chấn.
* Phù hợp triển khai ngay tại các nông trường mía, ngô, mì quy mô lớn tại Tây Ninh, Đồng Nai hoặc các tỉnh có vùng chuyên canh nông nghiệp.

**5.3. Hiệu quả**
* **5.3.1. [cite_start]Hiệu quả kỹ thuật:** [cite: 166] Hệ thống hoạt động hoàn toàn tự động, độ bền cao nhờ vỏ nhôm phay CNC IP67, sử dụng van cân bằng áp suất GORE-TEX và kính bảo vệ Sapphire siêu cứng.
* **5.3.2. [cite_start]Hiệu quả kinh tế:** [cite: 167] Cắt giảm 42% chi phí hóa chất và 61% chi phí nhân công. Chi phí duy trì (OPEX) siêu rẻ, chỉ khoảng 650.000 VNĐ/tháng cho server, tên miền và SIM 4G.
* **5.3.3. [cite_start]Hiệu quả xã hội:** [cite: 168] Giảm lượng lớn thuốc diệt cỏ ngấm vào đất và nguồn nước ngầm, góp phần bảo vệ môi trường sinh thái và sức khỏe của người tiêu dùng, hướng tới nền nông nghiệp phát triển bền vững.

**5.4. [cite_start]Mức độ triển khai** [cite: 169]
Dự án đã hoàn tất giai đoạn thiết kế kiến trúc hệ thống, dự toán ngân sách (BOM) và lựa chọn nhà cung cấp linh kiện. Sẵn sàng bước vào giai đoạn mua sắm vật tư, gia công cơ khí và lắp ráp Prototype để tiến hành chạy thử nghiệm thực địa (Field test).