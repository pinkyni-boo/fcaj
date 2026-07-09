---
title: "Kiến trúc giải pháp"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.1.3. </b> "
---


#### Mục tiêu

Mục này đưa sơ đồ kiến trúc vào ngay trong workshop để người đọc thấy rõ mỗi bước triển khai đang bám vào thành phần nào của hệ thống AWS.

#### Sơ đồ tham chiếu

Sơ đồ dưới đây tóm tắt định hướng triển khai CloudDoc được sử dụng xuyên suốt workshop:

<img src="/images/2-Proposal/aws-drawio-cloudoc.png" alt="CloudDoc AWS Architecture" style="max-width: 90%; height: auto;">

#### Giải thích theo từng lớp

1. **CloudFront và S3 static hosting** chịu trách nhiệm phân phối giao diện frontend tới người dùng cuối.
2. **EC2** chạy backend API để xác thực yêu cầu, sinh presigned URL và điều phối trạng thái tài liệu.
3. **RDS PostgreSQL** lưu metadata, trạng thái kiểm duyệt và dữ liệu phục vụ tìm kiếm.
4. **S3 object storage** lưu file tài liệu tách khỏi application server để luồng truyền file dễ mở rộng hơn.
5. **CloudWatch** cung cấp logs, metrics và alarms để hỗ trợ quan sát vận hành.

#### Ý nghĩa đối với workshop

Mỗi phần trong workshop tương ứng với một mảnh của kiến trúc này:

1. Phần điều kiện tiên quyết xác minh CloudFront, S3, EC2 và RDS đã sẵn sàng.
2. Phần upload chứng minh trình duyệt có thể gửi file trực tiếp lên S3 thông qua presigned URL do backend cấp.
3. Phần kiểm thử và kiểm duyệt xác nhận metadata và trạng thái tài liệu luôn đồng bộ với nhau.
4. Phần quan sát vận hành và cleanup cho thấy môi trường không chỉ được triển khai mà còn được theo dõi và dọn dẹp có kiểm soát.

Việc đặt mục kiến trúc ngay trong workshop giúp báo cáo thể hiện đây là một hệ thống hoàn chỉnh, thay vì chỉ là tập hợp các ảnh AWS rời rạc theo từng bước.
