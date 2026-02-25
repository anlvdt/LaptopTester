<p align="center">
  <img src="screenshots/dashboard.png" alt="LaptopTester Dashboard" width="800">
</p>

<h1 align="center">LaptopTester</h1>

<p align="center">
  <a href="https://laptoptester.web.app"><img src="https://img.shields.io/badge/Website-laptoptester.web.app-22c55e?style=for-the-badge" alt="Website"></a>
  <a href="https://github.com/anlvdt/LaptopTester/releases/latest"><img src="https://img.shields.io/badge/Download-v3.3-blue?style=for-the-badge" alt="Download"></a>
</p>

---

## Giới thiệu | Introduction

**VI** -- LaptopTester là phần mềm kiểm tra laptop cũ, giúp người mua và kỹ thuật viên kiểm tra nhanh tình trạng phần cứng trước khi quyết định.

Mình là Lê Văn Ẩn, làm nghề mua bán laptop cũ. Trong quá trình làm việc, mình thường gặp tình trạng máy bị sửa thông số (fake RAM, đổi tên CPU...) mà không dễ phát hiện bằng các công cụ thông thường. Nên mình viết phần mềm này để phục vụ công việc của mình, và chia sẻ cho những ai cần.

Phần mềm còn nhiều hạn chế, mình sẽ cố gắng cải thiện dần theo thời gian.

**EN** -- LaptopTester is a diagnostic tool for used laptops, helping buyers and technicians quickly check hardware condition before making a decision.

I'm Le Van An, a used laptop dealer in Vietnam. During my work, I often encountered machines with modified specs (faked RAM, renamed CPU...) that aren't easy to detect with common tools. So I wrote this software for my own use, and share it for anyone who finds it useful.

The software still has many limitations, and I'll try to improve it over time.

---

## Tính năng chính | Main Features

### Kiểm tra phần cứng | Hardware Inspection
- Đọc thông tin CPU, RAM, GPU, ổ cứng, pin | Read CPU, RAM, GPU, storage, battery info
- So sánh thông số từ nhiều nguồn (WMI, Registry, SMBIOS) để phát hiện sai lệch | Cross-check specs from multiple sources to detect discrepancies

### Kiểm tra thiết bị ngoại vi | Peripheral Testing
- Bàn phím, touchpad, loa, micro, camera | Keyboard, touchpad, speaker, mic, camera
- Cổng USB (phát hiện loại cổng, tốc độ, power delivery) | USB ports (type, speed, power delivery detection)
- WiFi, Bluetooth

### Pin | Battery
- Sức khỏe pin, chu kỳ sạc, dung lượng gốc vs hiện tại | Battery health, charge cycles, original vs current capacity
- Stress test với workload thực tế | Stress test with real workloads

### Khác | Others
- Kiểm tra nhiệt độ CPU/GPU | CPU/GPU temperature monitoring
- Xuất báo cáo | Report export
- Giao diện tiếng Việt và tiếng Anh | Vietnamese and English interface

---

## Ảnh chụp màn hình | Screenshots

<p align="center">
  <img src="screenshots/dashboard.png" alt="Dashboard" width="45%">
  <img src="screenshots/hardware.png" alt="Hardware Scan" width="45%">
</p>
<p align="center">
  <img src="screenshots/antifake.png" alt="Anti-Fake" width="45%">
  <img src="screenshots/battery.png" alt="Battery" width="45%">
</p>
<p align="center">
  <img src="screenshots/keyboard.png" alt="Devices" width="45%">
  <img src="screenshots/usb.png" alt="USB Ports" width="45%">
</p>

---

## Tải về | Download

**[Tải LaptopTester v3.3 | Download LaptopTester v3.3](https://github.com/anlvdt/LaptopTester/releases/latest)**

- File .exe duy nhất, đã tích hợp runtime, không cần cài đặt | Single .exe file, runtime included, no installation needed
- Chạy được trực tiếp từ USB | Runs directly from USB
- Yêu cầu: Windows 10/11 (64-bit), quyền Administrator | Requires: Windows 10/11 (64-bit), Administrator privileges

---

## Phiên bản | Versions

| Version | Ghi chú | Notes |
|---------|---------|-------|
| v3.3 | Phiên bản hiện tại. Viết lại bằng C# / WPF / .NET 8 | Current version. Rewritten in C# / WPF / .NET 8 |
| v2.x | Phiên bản cũ (PowerShell), không còn phát triển | Legacy version (PowerShell), no longer maintained |

---

## Miễn phí và trả phí | Free and Paid

**VI** -- Phần mềm có 2 phiên bản:
- **Free**: Kiểm tra phần cứng cơ bản, màn hình, bàn phím, loa, USB, WiFi...
- **Pro (149K, trả một lần)**: Thêm AI tư vấn, chống fake đa nguồn, benchmark, xuất báo cáo PDF

**EN** -- The software has 2 versions:
- **Free**: Basic hardware checks, display, keyboard, speaker, USB, WiFi...
- **Pro (149K VND, one-time payment)**: Adds AI advisor, multi-source anti-fake, benchmark, PDF report export

Chi tiết | Details: [laptoptester.web.app](https://laptoptester.web.app)

---

## Liên hệ | Contact

- Facebook: [fb.com/anlvdt](https://www.facebook.com/anlvdt)
- Zalo: 0976896621

---

<p align="center">
  <i>(c) 2026 Lê Văn Ẩn | Le Van An</i>
</p>
