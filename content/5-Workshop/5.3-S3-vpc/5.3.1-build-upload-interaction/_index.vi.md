---
title: "Khởi tạo luồng upload"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---


#### Mục tiêu

Mục tiêu của bước này là khởi tạo được một yêu cầu upload hợp lệ từ giao diện web và chuyển đổi nó thành thao tác lưu file thực tế trên Amazon S3. Đây là lúc người dùng bắt đầu tương tác với hệ thống, nên cả phần UX ở frontend lẫn contract dữ liệu giữa frontend và backend đều cần hoạt động nhất quán.

#### Các bước thực hiện

1. Người dùng chọn file, nhập tiêu đề, mô tả và các metadata cần thiết trên giao diện.
2. Frontend gửi yêu cầu xin presigned URL đến backend kèm theo thông tin của file.
3. Backend kiểm tra đầu vào, tạo khóa lưu trữ phù hợp và trả về upload URL.
4. Frontend sử dụng phương thức `PUT` để đưa file trực tiếp lên S3.
5. Sau khi upload thành công, frontend tiếp tục gọi API để lưu metadata nghiệp vụ.

#### Kết quả mong đợi

Sau bước này, file đã được đưa lên bucket đúng cách và workflow upload tách biệt rõ giữa phần truyền binary và phần lưu dữ liệu nghiệp vụ. Đây là nền tảng để các bước moderation, tìm kiếm và preview ở phía sau hoạt động ổn định hơn.
