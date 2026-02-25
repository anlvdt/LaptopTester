<p align="center">
  <img src="screenshots/dashboard.png" alt="LaptopTester v3.3" width="800">
</p>

<h1 align="center">LaptopTester v3.3</h1>

<p align="center">
  <a href="https://laptoptester.web.app"><img src="https://img.shields.io/badge/Website-laptoptester.web.app-22c55e?style=for-the-badge" alt="Website"></a>
  <a href="https://github.com/anlvdt/LaptopTester/releases/latest"><img src="https://img.shields.io/badge/Download-v3.3-blue?style=for-the-badge" alt="Download"></a>
</p>

---

## Câu chuyện | The Story

**VI**

Mình là Lê Văn Ẩn, làm nghề mua bán laptop cũ ở Việt Nam.

Một ngày, mình mua một chiếc máy được quảng cáo i7 / 16GB RAM / 512GB SSD với giá hợp lý. Mở máy lên, chuột phải My Computer hiện đúng 16GB RAM. Task Manager cũng hiện đúng. Dxdiag hiện i7. Nhưng khi dùng thực tế, máy chậm bất thường. Kiểm tra kỹ hơn, mình phát hiện: RAM thật chỉ có 8GB (thông số hiển thị trong System Properties đã bị sửa qua Registry), và ổ cứng là HDD 500GB được đặt tên giống SSD trong Disk Management.

Những thủ thuật này không quá phức tạp -- chỉ cần sửa vài giá trị Registry và dùng phần mềm thay đổi thông số hiển thị trong WMI. Người mua bình thường mở máy lên, xem Properties, thấy đúng thông số là tin. Ngay cả một số kỹ thuật viên cũng bị qua mặt nếu chỉ kiểm tra bằng một nguồn duy nhất.

Đó là lý do mình bắt đầu viết LaptopTester. Ban đầu là bản Python vào tháng 10/2025, chạy trên console để so sánh thông số giữa WMI, Registry và SMBIOS. Dần dần mình thêm kiểm tra pin, bàn phím, màn hình, USB... vì mỗi lần mua máy đều cần kiểm tra nhiều thứ mà không có công cụ nào làm hết trong một lần.

Sau khoảng 5 tháng phát triển, phiên bản v3.3 được viết lại hoàn toàn bằng C# / WPF, giao diện tối Spotify-style, chạy trực tiếp từ USB mà không cần cài đặt.

Phần mềm vẫn còn nhiều điểm cần cải thiện. Mình chia sẻ ở đây cho những ai cùng làm nghề và gặp vấn đề tương tự.

**EN**

I'm Le Van An, a used laptop dealer in Vietnam.

One day, I bought a machine advertised as i7 / 16GB RAM / 512GB SSD at a fair price. Right-clicking My Computer showed 16GB RAM. Task Manager confirmed it. Dxdiag showed i7. But in actual use, the machine was unusually slow. After digging deeper, I found the truth: the actual RAM was only 8GB (the display value in System Properties had been modified via Registry), and the storage was a 500GB HDD renamed to look like an SSD in Disk Management.

These tricks aren't overly sophisticated -- just editing a few Registry values and using software to alter WMI display data. Regular buyers open the machine, check Properties, see matching specs and trust it. Even some technicians get fooled if they only check one source.

That's why I started writing LaptopTester. It began as a Python console app in October 2025, cross-checking specs between WMI, Registry and SMBIOS. Over time, I added battery testing, keyboard checks, display tests, USB verification... because every time I bought a used machine, I needed to check many things and no single tool did it all.

After about 5 months of development, version 3.3 was fully rewritten in C# / WPF, with a dark Spotify-style interface, running directly from USB with no installation.

The software still has room for improvement. I share it here for anyone in the same line of work who faces similar problems.

---

## Tính năng chi tiết | Detailed Features

### Chống giả mạo cấu hình | Anti-Fake Hardware Detection

Đây là tính năng cốt lõi. Thay vì đọc từ một nguồn, LaptopTester truy vấn đồng thời 3 nguồn độc lập:

This is the core feature. Instead of reading from one source, LaptopTester queries 3 independent sources simultaneously:

| Nguồn / Source | Mô tả / Description |
|------|------|
| WMI (Windows Management Instrumentation) | Nguồn mà System Properties, Task Manager, Dxdiag dùng. Có thể bị sửa bằng phần mềm. / Used by System Properties, Task Manager, Dxdiag. Can be modified by software. |
| Registry | Thông số lưu trong Windows Registry. Một số phần mềm fake sửa ở đây để thay đổi hiển thị. / Specs stored in Windows Registry. Some faking software modifies values here. |
| SMBIOS / BIOS | Thông số ghi trực tiếp trên firmware phần cứng. Rất khó giả mạo vì nằm ở tầng thấp hơn OS. / Specs written directly on hardware firmware. Very hard to fake as it's below OS level. |

Nếu có bất kỳ sai lệch nào giữa 3 nguồn, phần mềm sẽ cảnh báo ngay. | If there's any discrepancy between the 3 sources, the software warns immediately.

<p align="center">
  <img src="screenshots/antifake.png" alt="So sánh đa nguồn | Multi-source comparison" width="700">
</p>

### Kiểm tra pin | Battery Testing

Không chỉ hiện phần trăm pin. LaptopTester đọc thông tin chi tiết từ driver pin: | Not just a battery percentage. LaptopTester reads detailed info from the battery driver:

- Sức khỏe pin (%) -- so sánh dung lượng thiết kế vs dung lượng thực tế | Battery health (%) -- comparing design capacity vs actual capacity
- Số chu kỳ sạc đã dùng | Number of charge cycles used
- Nhà sản xuất pin, điện áp, công suất tiêu thụ hiện tại | Battery manufacturer, voltage, current power draw
- Stress test pin: chạy workload thực tế (trình duyệt, Office) và đo thời gian xả | Battery stress test: runs real workloads (browser, Office) and measures drain time

<p align="center">
  <img src="screenshots/battery.png" alt="Kiểm tra pin | Battery testing" width="700">
</p>

### Quét phần cứng | Hardware Scan

Tổng hợp toàn bộ thông tin phần cứng trong một màn hình: | All hardware info summarized in one screen:

- CPU: tên, số nhân/luồng, xung nhịp cơ bản | CPU: name, cores/threads, base clock
- RAM: dung lượng, tốc độ, nhà sản xuất | RAM: capacity, speed, manufacturer
- GPU: tên, phiên bản driver | GPU: name, driver version
- Ổ cứng: loại (NVMe/SATA/HDD), dung lượng, phát hiện ổ ngoài | Storage: type (NVMe/SATA/HDD), capacity, external drive detection
- Đánh giá cân bằng CPU-GPU và khả năng nâng cấp | CPU-GPU balance assessment and upgrade potential

<p align="center">
  <img src="screenshots/hardware.png" alt="Quét phần cứng | Hardware scan" width="700">
</p>

### Kiểm tra thiết bị ngoại vi | Peripheral Device Testing

12 bài test cho các thiết bị đầu vào/đầu ra: | 12 tests for input/output devices:

| Nhập liệu / Input | Hiển thị & Âm thanh / Display & Audio | Kết nối / Connectivity |
|---|---|---|
| Bàn phím -- test từng phím | Màn hình -- điểm chết, hở sáng | WiFi + Bluetooth |
| Touchpad -- cử chỉ đa điểm | Loa -- stereo trái/phải | Cổng USB |
| Webcam -- xem trực tiếp | | |
| Microphone -- thu âm thử | | |

<p align="center">
  <img src="screenshots/keyboard.png" alt="12 bài test thiết bị | 12 device tests" width="700">
</p>

### Kiểm tra cổng USB | USB Port Testing

Phát hiện tất cả cổng USB trên máy, hiển thị: | Detects all USB ports on the machine, showing:

- Loại cổng: USB 2.0, 3.0, 3.1, USB-C, Thunderbolt 4 | Port type
- Tốc độ tối đa: 480 Mbps, 5 Gbps, 10 Gbps, 40 Gbps | Maximum speed
- Vị trí: trái/phải | Position: left/right
- Công suất sạc: 2.5W, 4.5W, 60W PD, 100W PD | Charging power

<p align="center">
  <img src="screenshots/usb.png" alt="Kiểm tra cổng USB | USB port testing" width="700">
</p>

### Tính năng khác | Other Features

- Theo dõi nhiệt độ CPU/GPU theo thời gian thực | Real-time CPU/GPU temperature monitoring
- Benchmark hiệu năng CPU, GPU, ổ cứng | CPU, GPU, storage benchmark
- AI tư vấn: phân tích kết quả test, đưa đánh giá tổng quan (cần API Key Cloudflare miễn phí) | AI advisor: analyzes test results, gives overall assessment (requires free Cloudflare API Key)
- Xuất báo cáo HTML/PDF | Export HTML/PDF reports
- Quy trình kiểm tra tùy chỉnh: tạo danh sách kiểm tra riêng theo nhu cầu | Custom test workflows
- Lưu lịch sử test, so sánh kết quả giữa các máy | Save test history, compare results across machines
- Phím tắt F1-F7 để chuyển nhanh giữa các tab | F1-F7 hotkeys for quick tab navigation
- Song ngữ Việt -- Anh, chuyển đổi ngay trong app | Bilingual Vietnamese -- English, switchable in-app

---

## Tải về | Download

**[Tải LaptopTester v3.3](https://github.com/anlvdt/LaptopTester/releases/latest)** | **[Download LaptopTester v3.3](https://github.com/anlvdt/LaptopTester/releases/latest)**

- File .exe duy nhất (~270 MB), đã tích hợp .NET runtime, không cần cài đặt | Single .exe file (~270 MB), .NET runtime included, no installation needed
- Chạy trực tiếp từ USB hoặc ổ cứng | Runs directly from USB or hard drive
- Yêu cầu: Windows 10/11 (64-bit), quyền Administrator | Requires: Windows 10/11 (64-bit), Administrator privileges

---

## Phiên bản | Versions

| Version | Ghi chú / Notes |
|---------|---------|
| v3.3 | Viết lại hoàn toàn bằng C# / WPF / .NET 8. Giao diện tối, AI advisor, song ngữ. / Fully rewritten in C# / WPF / .NET 8. Dark theme, AI advisor, bilingual. |
| v2.x | Python. Phiên bản đầu tiên (10/2025), không còn phát triển. / Python. Original version (10/2025), no longer maintained. |

---

## Miễn phí và trả phí | Free and Pro

| | Free | Pro (149K VND) |
|---|---|---|
| Quét phần cứng / Hardware scan | Có / Yes | Có / Yes |
| Kiểm tra thiết bị / Device testing | Có / Yes | Có / Yes |
| Pin, nhiệt độ / Battery, temperature | Có / Yes | Có / Yes |
| Chống fake đa nguồn / Multi-source anti-fake | -- | Có / Yes |
| Benchmark CPU/GPU | -- | Có / Yes |
| AI tư vấn / AI advisor | -- | Có / Yes |
| Xuất báo cáo PDF / PDF report export | -- | Có / Yes |

Trả một lần, dùng trọn đời. | One-time payment, lifetime use.

Chi tiết: [laptoptester.web.app](https://laptoptester.web.app) | Details: [laptoptester.web.app](https://laptoptester.web.app)

---

## Liên hệ | Contact

- Facebook: [fb.com/anlvdt](https://www.facebook.com/anlvdt)
- Zalo: 0976896621

---

<p align="center">
  <i>(c) 2026 Le Van An</i>
</p>
