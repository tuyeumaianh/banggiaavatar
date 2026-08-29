# Changelog

Tất cả thay đổi đáng chú ý của Toonie Emulator (dựa trên AngelChipEmulator_AutoSleep gốc) được ghi lại tại đây.

---

## V6

### Sửa lỗi
- **Menu bar bị dạt xa nhau**: "Tối ưu CPU" và "Clean RAM" từng bị tách rời khỏi nhóm `File / Options / Help` bởi một khoảng trắng lớn, do Windows Look-and-Feel tự động đẩy menu tên "Help" sang lề phải. Đã ép menu bar dùng layout dồn trái, toàn bộ 5 menu giờ nằm sát nhau ở mọi kích thước cửa sổ.

---

## V5

### Thêm mới
- **Menu "Clean RAM"**: submenu chọn chu kỳ tự động dọn bộ nhớ heap (`System.gc()`) — 5 giây / 10 giây / 30 giây / 1 phút / 5 phút / 30 phút, hoặc Dừng.
- **Trạng thái Clean RAM trên status bar**: hiển thị `Clean RAM: Hoạt động | Time: Xs | Ram: X%`, cập nhật theo đúng chu kỳ đã chọn; đổi về `Không hoạt động` khi dừng.
- Thiết kế lấy cảm hứng từ giao diện VPS-CleanTool (dropdown chu kỳ + trạng thái + đồng hồ đếm).

### Ghi chú kỹ thuật
- Label trạng thái mới được chèn vào vùng giữa (Center) của status bar sẵn có, không đụng tới label "Status" hay nút "Resize" gốc — tránh xung đột với cơ chế cập nhật status bar nguyên bản của emulator.
- Timer tự hủy khi chọn "Dừng" hoặc chuyển sang mức khác — đã kiểm tra không rò rỉ thread qua nhiều lần bật/tắt.

---

## V4

### Thêm mới
- **App RAM** trên màn hình sleep: hiển thị thêm dòng RAM riêng mà tiến trình Java (file jar) đang chiếm dụng, đọc qua `Runtime.getRuntime()`. Tách biệt rõ với RAM hệ điều hành đã có ở V3.

---

## V3

### Thêm mới
- **Thông tin CPU/RAM hệ thống trên màn hình Sleep**: hiển thị `CPU: X%` và `RAM: X.X/X.X GB` ngay dưới dòng tiêu đề, tự làm mới mỗi giây bằng timer riêng.
- Áp dụng cho cả 2 đường vào màn hình sleep: tự động sau 300 giây không thao tác, và khi bấm nút "Tối ưu CPU".

### Ghi chú kỹ thuật
- Dùng `com.sun.management.OperatingSystemMXBean` (API sẵn có trong JDK, không cần thư viện ngoài).
- Dùng API tương thích Java 8 (`getSystemCpuLoad`, `getTotalPhysicalMemorySize`) để đảm bảo chạy được trên JRE cũ.
- Timer tự dừng ngay khi thoát màn hình sleep, tránh rò rỉ thread.

---

## V2

### Thêm mới
- **Đổi thương hiệu toàn diện**: tên ứng dụng đổi từ "AngelChip Emulator" thành "Toonie Emulator" — ở tiêu đề cửa sổ, dialog About, và chữ hiển thị trên màn hình sleep (trước là "AngelChip.Net").
- **Logo mới**: chữ "T" trắng bóng đỏ trên nền vàng cam, bo góc — thay thế icon gốc ở taskbar và dialog About.

### Sửa lỗi
- **Lỗi "A Java Exception has occurred" khi khởi động**: nguyên nhân do class mới được biên dịch với bytecode Java 21 trong khi toàn bộ ứng dụng gốc dùng bytecode Java 8, gây `UnsupportedClassVersionError` trên máy chạy JRE cũ hơn. Đã build lại toàn bộ class tùy chỉnh với `--release 8` để khớp bytecode với ứng dụng gốc.

---

## V1 (bản khởi tạo mod)

### Thêm mới
- **Nút "Tối ưu CPU"** trên menu bar, cạnh "Help": bấm vào có tác dụng tương đương phím tắt `\` — chuyển ngay lập tức sang màn hình sleep, không cần chờ auto-sleep 300 giây mặc định.

### Ghi chú kỹ thuật
- Giữ nguyên toàn bộ hành vi gốc của AngelChipEmulator_AutoSleep (auto-sleep sau 300s không thao tác, sleep ngay khi nhấn `\`).
- Đóng gói qua launcher class riêng (`CpuOptimizeLauncher`) để không phải sửa trực tiếp bytecode của class `Main` gốc — launcher gọi lại đúng luồng khởi động nguyên bản rồi chèn thêm UI sau khi cửa sổ đã dựng xong.
- Giữ nguyên phần native launcher stub (EXE header) ở đầu file, đảm bảo file `.jar` vẫn chạy được như `.exe` khi double-click trên Windows.
