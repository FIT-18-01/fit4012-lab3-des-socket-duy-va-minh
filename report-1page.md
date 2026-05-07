# Report 1 page - Lab 3

## Thông tin nhóm
- Thành viên 1: Phạm Minh Duy (1871020192)
- Thành viên 2: Vũ Tuấn Minh (1871020394)

## Mục tiêu
Bài lab nhằm xây dựng một hệ thống nhỏ gồm Sender và Receiver giao tiếp qua socket TCP, trong đó dữ liệu được mã hóa bằng DES-CBC với IV và padding PKCS#7. Mục tiêu chính là hiểu luồng hoạt động của giao thức, cấu trúc gói tin (key + IV + header + ciphertext), vai trò của từng thành phần, và cách kiểm thử lỗi cơ bản. Ngoài ra, lab còn yêu cầu phân tích rủi ro bảo mật và áp dụng ethics trong sử dụng hệ thống.

## Phân công thực hiện
- Thành viên 1 (Phạm Minh Duy): Phụ trách chính phần Sender và báo cáo Q1.
- Thành viên 2 (Vũ Tuấn Minh): Phụ trách chính phần Receiver, tests, logs, threat model, và Q2.
- Phần làm chung: Code review, peer review, ethics, và cập nhật README.

## Cách làm
Sender tạo kết nối TCP tới Receiver, sinh key và IV ngẫu nhiên, mã hóa bản tin bằng DES-CBC với padding PKCS#7, rồi gửi tuần tự: key (8 byte) + IV (8 byte) + header độ dài (4 byte) + ciphertext. Receiver lắng nghe kết nối, nhận đúng thứ tự, giải mã và in bản rõ. Kiểm thử bao gồm ca happy path và các ca lỗi như header sai, ciphertext bị cắt, padding không hợp lệ, kết nối đóng đột ngột.

## Kết quả
Hệ thống chạy thành công trên localhost, Receiver lắng nghe trên port 6000, Sender kết nối và gửi bản tin mã hóa. Log cho thấy key, IV, ciphertext được in, và Receiver giải mã đúng bản rõ. Các ca kiểm thử bao gồm happy path, tamper ciphertext, wrong key, truncated ciphertext, và invalid header đều pass hoặc fail như mong đợi với log lỗi phù hợp.

## Kết luận
Bài lab giúp hiểu sâu về socket TCP, DES-CBC, và tầm quan trọng của error handling trong hệ thống mạng. Bài học bảo mật: truyền key plaintext là rủi ro lớn, cần dùng giao thức an toàn như TLS. Trong tương lai, nên áp dụng key exchange protocols và authentication để bảo vệ dữ liệu.
