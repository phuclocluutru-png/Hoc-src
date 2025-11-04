# H-c-src
Học src
# Học src (MU Online) – Main 5.2 / MuMain

> Mục tiêu: Tự học cách đọc – hiểu – build – tùy biến **client Main 5.2** và các biến thể **MuMain** hiện đại (FPS cao, Unicode, helper, v.v.), đồng thời nắm các khái niệm client–server của MU.

---

## 🎯 Kết quả mong đợi
- Hiểu **luồng khởi động** của client (`WinMain → GetMainInfo/LoadMainConfig → MainLoop`).
- Nắm **cấu hình client** qua `Mu.Main` (hoặc `MainInfo.bmd/.ini`) và công cụ `GetMainInfo.exe`.
- Biết **cấu trúc dự án client** (render, UI, network, resources).
- Build được bản client mẫu; bật/tắt **V-Sync**, giới hạn **FPS**, và test **MU Helper**.
- Đọc sơ bộ **packet** và tương tác với server (OpenMU/Update 15).

> Tham khảo dự án gốc và biến thể: LouisEmulator/Main5.2, Sven-n’s MuMain, OpenMU (protocol).  [oai_citation:1‡GitHub](https://github.com/phuclocluutru-png/Hoc-src.git)

---

## 📦 Thuật ngữ nhanh
- **Main 5.2**: dòng client cổ điển được cộng đồng “dọn sạch”, build VS2019, tích hợp CashShop/ASIO, chuẩn bị sẵn cấu trúc để mở rộng (scene FPS của S6).  [oai_citation:2‡GitHub](https://github.com/phuclocluutru-png/Hoc-src.git)  
- **MuMain (Sven-n)**: client hiện đại hóa từ 5.2, tăng FPS/V-Sync, Unicode (UTF-16LE nội bộ), mở rộng giao thức tới **S6 Ep3**, có **MU Helper**, kết nối qua thư viện mạng C# Native AOT.  
- **OpenMU**: server .NET mã nguồn mở + tài liệu **packet/giao thức** rõ ràng, rất phù hợp để học và test.  

---

## 🧭 Lộ trình học (theo từng tuần)

### Tuần 1 — Tổng quan & khởi động
- Đọc README của **Main5.2** để hiểu mục tiêu làm sạch, build VS2019, ASIO, CashShop, scene FPS S6.  [oai_citation:3‡GitHub](https://github.com/phuclocluutru-png/Hoc-src.git)  
- Hiểu cơ chế **GetMainInfo.exe + maininfo.ini → Mu.Main**: cấu hình IP/Port/flag → client load vào `g_MainInfo`.

### Tuần 2 — Cấu trúc client & cấu hình
- Nhóm **entry/config**: `WinMain/Main.cpp`, `GetMainInfo()/LoadMainConfig()`, struct `MAIN_INFO`.
- Nhóm **resources/UI**: Data\Interface\*, text/font; nơi hiển thị HUD, cửa sổ, chat.
- Thử đổi một vài **flag** (ví dụ bật helper, tên cửa sổ) rồi chạy lại.

### Tuần 3 — Render & FPS
- Tìm phần **game loop/timing**: bật **V-Sync**, lệnh chat `$fps <value>`, `$vsync on|off`, tùy chọn “reduce effects”.  
- Quan sát **OpenGL/vertex arrays** giúp mượt hơn khi đông người/vật thể (MuMain).

### Tuần 4 — Network & Packet
- Xem **ClientLibrary** (C# Native AOT) trong MuMain – thay ngăn mạng C++ cũ; cách publish thư viện trước lần chạy đầu.  
- Đối chiếu **opcode/packet** đăng nhập, chọn nhân vật, vào game qua tài liệu OpenMU.

> Những mục này đều được nêu trong README của Sven-n’s MuMain (FPS/V-Sync/Helper/Unicode/giao thức S6 Ep3, ClientLibrary) và tài liệu packet của OpenMU.  [oai_citation:4‡GitHub](https://github.com/phuclocluutru-png/Hoc-src.git)

---

## 🧱 Cấu trúc thư mục gợi ý cho repo này
Hoc-src/
├─ notes/                    # Ghi chép từng buổi học (md)
│  ├─ 01-overview.md
│  ├─ 02-config-mu.main.md
│  ├─ 03-render-fps.md
│  └─ 04-network-packets.md
├─ demos/                    # Mẫu cấu hình/patch nhỏ để thử
│  ├─ maininfo.ini
│  └─ scripts/
├─ refs/                     # Tài liệu tham khảo (link/tóm tắt)
│  ├─ main5.2.md
│  ├─ mumain-readme-notes.md
│  └─ openmu-protocol.md
└─ README.md
---

## 🔧 Dụng cụ & môi trường đề xuất
- **Visual Studio 2019/2022** (C++ & .NET workloads).
- **DirectX SDK (June 2010)** nếu bản client yêu cầu.  
- Git, một trình **hex editor** (xem thử `Mu.Main`), và **Resource Hacker** (khảo sát file exe).

---

## 🚀 Bài tập nhỏ (hands-on)
1. Viết `notes/02-config-mu.main.md` mô tả pipeline:
maininfo.ini → GetMainInfo.exe → Mu.Main → main.exe (LoadMainConfig)

2. Thêm một **label** nhỏ ở HUD để thử pipeline render/UI.  
3. Bật/tắt **V-Sync** và đặt `$fps 60` → ghi lại cảm nhận FPS.  
4. Log gói **login** đầu tiên (client → server) và map theo tài liệu OpenMU (opcode, độ dài, payload).

---

## 🔗 Nguồn tham khảo (khuyên đọc thẳng)
- **LouisEmulator/Main5.2** – README mô tả: build VS2019, ASIO (On/Off), CashShop tích hợp, “Main Scene updated to S6 system (FPS)”, tiết giảm define/đa ngôn ngữ.  [oai_citation:5‡GitHub](https://github.com/phuclocluutru-png/Hoc-src.git)
- **Sven-n’s MuMain** – README nêu rõ: V-Sync & `$fps`, “reduce effects”, Unicode (UTF-16LE/UTF-8), mở rộng giao thức tới **S6 Ep3**, **MU Helper**, thay ngăn mạng bằng **ClientLibrary (.NET 9 Native AOT)**.  [oai_citation:6‡GitHub](https://github.com/phuclocluutru-png/Hoc-src.git)
- **OpenMU** – Tài liệu **packet/giao thức MU** (dễ tra cứu khi debug network).  [oai_citation:7‡GitHub](https://github.com/phuclocluutru-png/Hoc-src.git)

---

## ⚠️ Lưu ý pháp lý
Một số phần mềm/tài nguyên liên quan MU Online có thể thuộc bản quyền. Hãy đảm bảo bạn chỉ sử dụng mã nguồn/tài nguyên **được cấp phép** hoặc dùng cho mục đích **học tập/nghiên cứu cá nhân**.

---

## 🤝 Đóng góp
- Tạo issue ghi lại câu hỏi/kho kiến thức.  
- PR các **notes** mới, hình minh họa luồng, snippet mã, và cấu hình mẫu.  


