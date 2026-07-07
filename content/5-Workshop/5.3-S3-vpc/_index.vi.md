---
title: "Thiết kế luồng upload bảo mật với Amazon S3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---
### Luồng xử lý đề xuất

1. Người dùng chọn file và nhập metadata trên giao diện CloudDoc.
2. Frontend gửi yêu cầu tới backend để xin presigned upload URL.
3. Backend tạo S3 key phù hợp và trả về URL có thời hạn ngắn.
4. Frontend `PUT` file trực tiếp lên S3.
5. Khi upload thành công, frontend tiếp tục gọi API lưu metadata vào PostgreSQL.

### Vì sao chọn presigned URL

- Giảm tải cho backend vì file không đi xuyên qua application server.
- Nâng cao bảo mật vì URL chỉ có hiệu lực trong thời gian ngắn.
- Dễ mở rộng khi số lượng tài liệu và người dùng tăng lên.

### Điểm cần chú ý

- Kiểm soát kích thước file và định dạng tài liệu ngay từ frontend và backend.
- Sinh S3 key có cấu trúc rõ ràng để dễ quản lý.
- Không cho phép frontend tự ý ghi metadata nếu upload thực tế chưa thành công.

### Ý nghĩa về mặt kiến trúc

Đây là phần quan trọng nhất của workshop vì nó thể hiện rõ tư duy “dùng cloud đúng chỗ”. Thay vì để backend ôm cả việc truyền file lẫn xử lý nghiệp vụ, presigned URL giúp tách trách nhiệm rõ ràng: S3 chịu trách nhiệm lưu trữ file, backend chịu trách nhiệm kiểm soát nghiệp vụ, còn frontend chịu trách nhiệm luồng tương tác với người dùng.
