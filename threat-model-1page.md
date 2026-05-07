# Threat Model - Lab 3

## Thông tin nhóm
- Thành viên 1: Phạm Minh Duy (1871020192)
- Thành viên 2: Vũ Tuấn Minh (1871020394)

## Assets
- Bản rõ của người dùng (plaintext message)
- Khóa DES và IV (được truyền dưới dạng plaintext)
- Dữ liệu ciphertext trên đường truyền
- Log hệ thống (có thể chứa key, IV, plaintext)
- Địa chỉ IP và port của Receiver

## Attacker model
- Người nghe lén trên cùng mạng LAN (sniffing packets)
- Sửa đổi dữ liệu trên đường truyền (man-in-the-middle)
- Gửi gói tin giả mạo hoặc lỗi
- Làm gián đoạn kết nối (DoS)
- Truy cập log files nếu compromised

## Threats
- Lộ key và IV vì truyền plaintext, kẻ tấn công có thể giải mã tất cả ciphertext
- Sửa đổi ciphertext gây lỗi giải mã hoặc thay đổi plaintext
- Giả mạo độ dài header để Receiver đọc sai lượng dữ liệu
- Nghe lén plaintext nếu không mã hóa key
- DoS bằng cách đóng kết nối hoặc gửi dữ liệu lỗi

## Mitigations
- Sử dụng giao thức key exchange an toàn như Diffie-Hellman thay vì truyền key plaintext
- Thêm MAC hoặc signature để xác thực toàn vẹn ciphertext
- Sử dụng TLS để mã hóa toàn bộ luồng TCP
- Thêm authentication cho Sender/Receiver
- Đặt timeout và xử lý exception để chống DoS

## Residual risks
- Máy người dùng bị compromise, lộ key và dữ liệu
- Log files chứa thông tin nhạy cảm nếu không bảo vệ
- Môi trường mạng nội bộ vẫn có thể bị sniffing nếu không dùng encryption end-to-end
