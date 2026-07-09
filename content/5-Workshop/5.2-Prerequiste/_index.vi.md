---
title: "Điều kiện tiên quyết"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---


#### Mục tiêu

Trước khi bắt đầu workflow upload và kiểm thử end-to-end, cần xác nhận rằng môi trường triển khai đã đầy đủ và tài nguyên AWS đang ở trạng thái sẵn sàng. Nếu bước chuẩn bị bị bỏ qua, các lỗi như sai endpoint, CORS không hợp lệ, EC2 không phản hồi hoặc RDS chưa sẵn sàng sẽ làm cho phần triển khai phía sau khó kiểm chứng và khó chụp minh họa đúng flow.

#### Thành phần cần kiểm tra

- Giao diện web mở được và form upload hoạt động.
- Backend API chạy ổn định.
- Bucket S3 đã tồn tại và cấu hình CORS hợp lệ.
- RDS PostgreSQL kết nối được.
- Tài liệu mẫu đã sẵn sàng để đưa vào hệ thống.

#### Ý nghĩa của bước chuẩn bị

Phần này giúp người đọc thấy rằng nhóm không triển khai theo kiểu thử ngẫu nhiên từng dịch vụ, mà thực sự có một bước pre-check trước khi đi vào luồng chính. Khi frontend, backend, S3 và database đều đã được xác minh, các bước sau như upload, moderation và đồng bộ trạng thái sẽ có giá trị chứng minh cao hơn trong báo cáo.

#### Các bước thực hiện

1. [Kiểm tra môi trường triển khai](5.2.1-verify-frontend-readiness/)
2. [Chuẩn bị dữ liệu và cấu hình hệ thống](5.2.2-prepare-source-data/)
