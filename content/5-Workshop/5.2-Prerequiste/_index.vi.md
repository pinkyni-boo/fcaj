---
title: "Điều kiện chuẩn bị"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---
### Thành phần cần có

- Frontend React có form upload và các trường metadata.
- Backend Express có API tạo presigned URL và API lưu metadata tài liệu.
- PostgreSQL để lưu title, subject, school, department, uploader, trạng thái và đường dẫn S3.
- Một S3 bucket dành riêng cho tài liệu upload.

### Cấu hình kỹ thuật

- Biến môi trường cho bucket S3, thời gian hết hạn presigned URL và thông tin kết nối cơ sở dữ liệu.
- CORS trên S3 phải cho phép domain frontend truy cập để upload trực tiếp.
- IAM role hoặc access policy chỉ nên cấp đúng quyền cần thiết cho backend.

### Điều kiện kiểm thử

Trước khi kiểm thử end-to-end, cần xác nhận:

- Frontend gọi được API backend.
- Backend tạo được upload URL hợp lệ.
- Bucket S3 nhận được file.
- Metadata sau upload được lưu đúng trong PostgreSQL.

### Ý nghĩa của bước chuẩn bị

Phần chuẩn bị nghe có vẻ đơn giản nhưng lại quyết định rất nhiều đến độ ổn định của toàn bộ luồng upload. Chỉ cần sai một cấu hình CORS, một biến môi trường hoặc một quyền IAM là toàn bộ trải nghiệm người dùng có thể thất bại dù frontend và backend đều “đúng code”. Vì vậy, bước này đóng vai trò như nền móng kỹ thuật cho workshop.
