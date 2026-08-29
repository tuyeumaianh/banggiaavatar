# Toonie Emulator

Bản mod tùy chỉnh của **AngelChip Emulator** (dựa trên MicroEmulator — giả lập điện thoại Java/J2ME), thêm các tính năng tối ưu và tiện ích, đổi thương hiệu, và đóng gói sẵn để chạy trên Windows.

## Tính năng thêm mới

### 🖥️ Tối ưu CPU
Nút bấm trên menu bar, tương đương với việc nhấn phím `\` — chuyển ngay lập tức sang màn hình sleep (tiết kiệm CPU/hiệu năng khi không dùng tới emulator), không cần chờ auto-sleep 300 giây mặc định.

### 🧹 Clean RAM
Menu chọn chu kỳ tự động dọn bộ nhớ heap của emulator (`System.gc()`):
- Các mức: **5 giây / 10 giây / 30 giây / 1 phút / 5 phút / 30 phút**, hoặc **Dừng**
- Trạng thái hiện trực tiếp trên status bar: `Clean RAM: Hoạt động | Time: Xs | Ram: X%`
- Lưu ý: đây là RAM nội bộ của JVM (bộ nhớ mà chính file jar này đang chiếm dụng), **không phải** RAM toàn hệ điều hành Windows.

### 📊 Thông tin hệ thống trên màn hình Sleep
Khi vào chế độ sleep (tự động sau 300s hoặc bấm "Tối ưu CPU"), màn hình hiện thêm:
- **CPU**: % sử dụng CPU của hệ thống
- **RAM**: dung lượng RAM hệ điều hành đang dùng / tổng RAM (GB)
- **App RAM**: dung lượng RAM riêng mà file jar này đang chiếm dụng (MB)

Tự động cập nhật mỗi giây khi đang ở màn hình sleep.

### 🎨 Đổi thương hiệu
- Tên ứng dụng: **AngelChip Emulator** → **Toonie Emulator**
- Logo mới: chữ "T" trắng với bóng đỏ trên nền vàng cam, bo góc — thay thế icon cũ ở tiêu đề cửa sổ, taskbar, và dialog About
- Nội dung dialog About và chữ hiển thị trên màn hình sleep cũng đổi theo tên mới

## Cách chạy

Double-click file `.jar` như một ứng dụng `.exe` bình thường trên Windows (file có kèm sẵn phần khởi động native, không cần cài thêm gì).

Hoặc chạy bằng dòng lệnh:
```
java -jar ToonieEmulator_V6.jar
```

**Yêu cầu:** Java 8 trở lên (bytecode được build tương thích ngược để chạy trên các bản Java cũ).

## Giới hạn đã biết

- **Clean RAM** chỉ dọn được bộ nhớ nội bộ của tiến trình Java (JVM heap), không có quyền dọn RAM toàn hệ điều hành — đây là giới hạn của nền tảng Java, một tiến trình thông thường không có quyền truy cập sâu vào bộ nhớ hệ thống như các công cụ native (ví dụ VPS-CleanTool).
- Ở cửa sổ mặc định (160px), một số icon/text có thể cần resize cửa sổ để hiển thị đầy đủ — dùng nút "Resize" có sẵn trong ứng dụng.

## Ghi công

Dựa trên MicroEmulator / AngelChip Emulator gốc (angelchip.net). Xem chi tiết các thay đổi theo từng phiên bản tại [CHANGELOG.md](./CHANGELOG.md).
