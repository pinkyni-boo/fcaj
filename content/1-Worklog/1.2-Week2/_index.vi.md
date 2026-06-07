---
title: "Thực hành hạ tầng cốt lõi (EC2, S3) và bảo mật IAM"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
### Mục tiêu tuần 2:

* Nắm vững kiến trúc và cách thức vận hành các dịch vụ tính toán (Compute) và lưu trữ (Storage) quan trọng nhất của AWS.
* Tự tay triển khai thành công máy chủ ảo và quản lý kho lưu trữ dữ liệu đám mây.
* Xây dựng tư duy bảo mật hệ thống thông qua việc quản lý định danh và phân quyền truy cập.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Cày lý thuyết: Xem và ghi chú các module bài giảng về Amazon EC2 và Amazon S3.<br><br>- Phân tích các tình huống sử dụng thực tế (Use cases) của từng dịch vụ. | 24/04/2026 | 24/04/2026 |  |
| 3 | - Thực hành Lab (EC2): Khởi tạo máy chủ ảo (Instances), lựa chọn cấu hình phù hợp (CPU, RAM).<br><br>- Cấu hình Security Groups đóng vai trò như tường lửa (mở cổng 22 cho SSH, 80 cho HTTP). | 25/04/2026 | 25/04/2026 |  |
| 4 | - Thực hành Lab (S3): Tạo S3 Bucket, tìm hiểu các hạng lưu trữ (Storage Classes) để tối ưu chi phí.<br><br>- Thao tác upload/download tệp tin và thiết lập chặn truy cập công khai (Block Public Access). | 26/04/2026 | 26/04/2026 |  |
| 5 | - Thực hành cấu hình IAM cơ bản: Tạo người dùng (Users), nhóm người dùng (Groups).<br><br>- Viết và gắn các chính sách phân quyền (Policies) theo nguyên tắc "quyền hạn tối thiểu" (Least Privilege). | 27/04/2026 | 27/04/2026 |  |
| 6 | - Hoàn thành toàn bộ các module lý thuyết còn đọng lại trên hệ thống.<br><br>- Thực hiện các bài kiểm tra đánh giá kiến thức (Knowledge Checks) của tuần để ôn tập. | 28/04/2026 | 28/04/2026 |  |


### Kết quả đạt được tuần 2:

* Đã hoàn tất việc xem và tổng hợp kiến thức từ các video lý thuyết trên YouTube.
* Có khả năng tự triển khai, cấu hình mạng cơ bản và kết nối thành công vào máy chủ ảo Amazon EC2.
* Hiểu và vận dụng được dịch vụ lưu trữ Amazon S3, biết cách thiết lập quyền truy cập để bảo vệ dữ liệu (đây là bước đệm quan trọng cho phần upload file của dự án CloudDoc sau này).
* Nắm vững cơ chế hoạt động của AWS IAM, có thể tự thiết lập các role và policy để bảo vệ an toàn cho tài nguyên dự án.



