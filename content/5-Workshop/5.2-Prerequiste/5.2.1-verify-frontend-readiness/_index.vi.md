---
title: "Kiểm tra môi trường triển khai"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.2.1. </b> "
---


#### Mục tiêu

Mục tiêu của bước này là xác minh các thành phần chính của hệ thống đang hoạt động đúng trước khi bắt đầu upload tài liệu. Việc kiểm tra này giúp đảm bảo rằng khi lỗi xuất hiện ở các bước sau, nhóm có thể xác định nguyên nhân chính xác là do workflow nghiệp vụ hay do hạ tầng nền chưa sẵn sàng.

#### Các bước xác minh môi trường

Trước khi upload tài liệu, cần thực hiện kiểm tra các điều kiện hạ tầng sau:

**Bước 1:** Kiểm tra **Frontend** truy cập được từ trình duyệt và xác nhận cấu hình phân phối trên **CloudFront**.

<img src="/images/5-Workshop/AWS-Console/cloudfront-distribution.png" alt="CloudFront distribution dùng để phân phối frontend của CloudDoc" style="max-width: 90%; height: auto;">

**Bước 2:** Xác nhận các **Bucket S3** hiển thị đúng trong AWS Console, đảm bảo quyền truy cập và nơi lưu trữ đã sẵn sàng.

<img src="/images/5-Workshop/AWS-Console/frontend-buckets.png" alt="Danh sách S3 buckets dùng trong dự án CloudDoc" style="max-width: 90%; height: auto;">

**Bước 3:** Kiểm tra **EC2 instance** đang chạy đúng phiên bản dịch vụ và **API backend** phản hồi bình thường.

<img src="/images/5-Workshop/AWS-Console/ec2-instances.png" alt="EC2 instance đang chạy backend API của hệ thống" style="max-width: 90%; height: auto;">

**Bước 4:** Đảm bảo **RDS PostgreSQL** đã sẵn sàng nhận kết nối để ghi nhận metadata.

<img src="/images/5-Workshop/AWS-Console/rds-database.png" alt="RDS PostgreSQL sẵn sàng cho phần metadata của tài liệu" style="max-width: 90%; height: auto;">

{{% notice info %}}
**Lưu ý:** Việc kiểm tra kỹ hạ tầng ở bước này giúp khoanh vùng lỗi dễ dàng hơn ở các bước tích hợp sau.
{{% /notice %}}

#### Kết quả mong đợi

Khi hoàn tất bước này, nhóm có thể chuyển sang phần upload mà không cần xử lý lại các lỗi nền tảng như route sai, API chết, thiếu bucket hoặc database chưa sẵn sàng.
