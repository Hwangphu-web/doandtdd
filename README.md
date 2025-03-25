
# Ứng Dụng Chat Room 

Ứng dụng chat đơn giản được xây dựng bằng Java, cho phép người dùng giao tiếp thời gian thực qua mạng TCP. Ứng dụng hỗ trợ nhắn tin 1-1, gửi tin nhắn đến tất cả người dùng, và chia sẻ file giữa các client. Giao diện thân thiện được xây dựng bằng Java Swing, đi kèm với một server để quản lý kết nối từ các client.

## Mục Lục
- [Tính Năng](#tính-năng)
- [Công Nghệ](#công-nghệ)
- [Cài Đặt](#cài-đặt)
- [Hướng Dẫn Sử Dụng](#hướng-dẫn-sử-dụng)
- [Cấu Trúc Dự Án](#cấu-trúc-dự-án)
- [Đóng Góp](#đóng-góp)
- [Giấy Phép](#giấy-phép)

## Tính Năng
- **Nhắn Tin Thời Gian Thực**: Gửi và nhận tin nhắn ngay lập tức giữa các client.
- **Nhắn Tin 1-1**: Giao tiếp riêng tư với một người bạn được chọn.
- **Gửi Tin Nhắn Hàng Loạt**: Gửi tin nhắn đến tất cả người dùng đang online bằng lệnh `CMD_CHATALL`.
- **Chia Sẻ File**: Chuyển file giữa các client thông qua server (`CMD_SENDFILE`).
- **Danh Sách Người Dùng Online**: Hiển thị danh sách người dùng đang trực tuyến, cập nhật thời gian thực.
- **Giao Diện Thân Thiện**: Được xây dựng bằng Java Swing, đơn giản và dễ sử dụng.
- **Trạng Thái Kết Nối**: Hiển thị trạng thái kết nối (ví dụ: "Online", "Offline") qua giao diện.

## Công Nghệ
- **Java**: Ngôn ngữ lập trình chính cho cả server và client.
- **Java Swing**: Dùng để xây dựng giao diện người dùng (GUI) phía client.
- **TCP Sockets**: Dùng cho giao tiếp mạng giữa server và client.
- **ThreadPoolExecutor**: Quản lý nhiều kết nối client đồng thời phía server.
- **Apache NetBeans**: IDE được khuyến nghị để phát triển và kiểm thử.

## Cài Đặt

### Yêu Cầu
- Bộ công cụ phát triển Java (JDK) phiên bản 8 hoặc cao hơn.
- IDE như Apache NetBeans (không bắt buộc nhưng được khuyến nghị).
- Git (để tải mã nguồn từ repository).

### Các Bước Cài Đặt
1. **Tải Mã Nguồn**:
   ```bash
   git clone https://github.com/Hwangphu-web/chat-room-3des.git
   cd chat-room-3des
   ```

2. **Mở Dự Án**:
   - Mở dự án trong IDE bạn chọn (ví dụ: Apache NetBeans).
   - Cấu trúc dự án bao gồm các gói `server` và `client`.

3. **Biên Dịch Dự Án**:
   - Đảm bảo tất cả thư viện cần thiết đã được thêm (dự án chỉ dùng thư viện chuẩn của Java).
   - Biên dịch dự án bằng IDE hoặc qua dòng lệnh:
     ```bash
     javac -d bin src/**/*.java
     ```

## Hướng Dẫn Sử Dụng

### Chạy Server
1. Khởi động server bằng cách chạy lớp `CombinedServer` (`server/CombinedServer.java`).
   - Giao diện server sẽ hiện ra, cho phép bạn chọn cổng (mặc định: 5056).
   - Nhấn nút "Start Server" để bắt đầu lắng nghe kết nối từ client.
   - Server sẽ ghi lại mọi hoạt động (kết nối client, tin nhắn, chuyển file) trong khu vực log.

### Chạy Client
1. Khởi động client bằng cách chạy lớp `RunClient` (`client/RunClient.java`).
   - Một hộp thoại sẽ yêu cầu bạn nhập tên người dùng (ví dụ: `hoangphuTH28.35`).
   - Client sẽ kết nối đến server (mặc định: `localhost`, cổng 5056).
   - Giao diện sẽ hiển thị danh sách bạn bè online và khu vực chat.

2. **Nhắn Tin**:
   - Chọn một người bạn từ danh sách "Bạn bè online" để bắt đầu trò chuyện.
   - Nhập tin nhắn vào ô nhập và nhấn nút "Gửi" (hoặc phím Enter) để gửi.
   - Tin nhắn sẽ hiển thị trong khu vực chat kèm thời gian.

3. **Chia Sẻ File**:
   - Tính năng chia sẻ file đã được hỗ trợ nhưng chưa tích hợp vào giao diện client.
   - Sử dụng lệnh `CMD_SENDFILE` để chuyển file qua server.

### Ví Dụ
- Khởi động server trên cổng 5056.
- Chạy hai client với tên người dùng `hoangphuTH28.35` và `phu6677`.
- Chọn một người bạn từ danh sách online và gửi tin nhắn như "hello tôi mới mất laptop".
- Người nhận sẽ thấy tin nhắn kèm thời gian (ví dụ: `13:22:53 - hoangphuTH28.35: hello tơi mới mất laptop`).

## Cấu Trúc Dự Án
```
chat-room-3des/
├── src/
│   ├── client/
│   │   ├── Friend.java              # Quản lý thông tin bạn bè và lịch sử chat
│   │   ├── RunClient.java           # Điểm khởi chạy client
│   │   ├── SocketHandlerClientSide.java  # Xử lý giao tiếp socket phía client
│   │   ├── SimpleChatClientHandler.java  # Một phiên bản khác của SocketHandlerClientSide
│   │   └── gui/
│   │       └── ClientChatForm.java  # Giao diện client dùng Java Swing
│   └── server/
│       └── CombinedServer.java      # Server với giao diện quản lý kết nối
├── bin/                             # Thư mục chứa file .class sau khi biên dịch
└── README.md                        # Tài liệu hướng dẫn dự án
```

## Đóng Góp
Chúng tôi hoan nghênh mọi đóng góp! Nếu bạn muốn tham gia:
1. Fork repository này.
2. Tạo một nhánh mới (`git checkout -b feature/tinh-nang-cua-ban`).
3. Thực hiện thay đổi và commit (`git commit -m "Thêm tính năng của bạn"`).
4. Push lên nhánh của bạn (`git push origin feature/tinh-nang-cua-ban`).
5. Mở một pull request.

### Gợi Ý Cải Tiến
- Thêm mã hóa (ví dụ: 3DES) cho tin nhắn và file.
- Chuyển giao diện sang nền tảng web dùng HTML/CSS/JS và WebSocket.
- Tích hợp giao diện gửi file (ví dụ: nút "Gửi File").
- Hiển thị số tin nhắn chưa đọc trong danh sách bạn bè.

## Giấy Phép
Dự án này được cấp phép theo Giấy phép MIT. Xem chi tiết trong file [LICENSE](LICENSE).
