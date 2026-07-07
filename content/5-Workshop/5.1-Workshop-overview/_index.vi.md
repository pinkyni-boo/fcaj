---
title: "Tổng quan workshop"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---
### Mục tiêu

Workshop này mô tả luồng xử lý tài liệu của CloudDoc dưới góc nhìn kỹ thuật và triển khai thực tế. Mục tiêu không chỉ là tải file lên cloud, mà còn phải đảm bảo trải nghiệm người dùng mượt, dễ mở rộng và phù hợp với mô hình phân quyền trong môi trường học tập.

### Bài toán

CloudDoc cần giải quyết đồng thời ba yêu cầu:

- Người dùng phải tải tài liệu lên một cách đơn giản.
- Hệ thống không bị nghẽn vì file lớn đi qua backend.
- Metadata vẫn được kiểm soát tốt để hỗ trợ tìm kiếm, preview và kiểm duyệt.

### Tại sao luồng upload lại quan trọng

Trong nhiều hệ thống nhỏ, việc upload thường được làm khá đơn giản: người dùng gửi file về backend, backend nhận file rồi lưu lại. Cách này dễ làm ở giai đoạn đầu nhưng sẽ nhanh chóng bộc lộ nhược điểm khi dung lượng file lớn hơn hoặc số lượng người dùng tăng lên. Với CloudDoc, việc chọn đúng luồng upload là quyết định ảnh hưởng trực tiếp tới trải nghiệm người dùng, hiệu năng backend và hướng phát triển về sau.

### Cách tiếp cận

Giải pháp phù hợp là để backend tạo **presigned URL**, sau đó frontend tải file trực tiếp lên **Amazon S3**. Sau khi upload thành công, frontend gửi metadata về backend để lưu vào **PostgreSQL**. Cách làm này giảm tải cho server ứng dụng và tách rõ phần file với phần dữ liệu nghiệp vụ.
