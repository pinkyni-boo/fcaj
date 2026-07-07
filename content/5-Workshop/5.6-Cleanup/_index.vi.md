---
title: "Dọn dẹp tài nguyên và kiểm soát chi phí"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---
### Mục tiêu của bước clean-up

Sau khi hoàn thành demo hoặc kiểm thử, nhóm cần dọn dẹp tài nguyên để tránh phát sinh chi phí không cần thiết. Phần clean-up cũng cho thấy nhóm hiểu rõ quan hệ phụ thuộc giữa các thành phần trong kiến trúc CloudDoc và biết cách kết thúc vòng đời tài nguyên một cách an toàn.

### Thứ tự xóa tài nguyên đề xuất

Thứ tự dọn dẹp được áp dụng theo đúng hướng kiểm soát phụ thuộc:

1. **ALB**
2. **EC2**
3. **RDS PostgreSQL**
4. **SQS, CloudWatch và SNS**
5. **S3 Bucket**
6. **VPC**

Nếu môi trường có bật **CloudFront** để phân phối frontend tĩnh, nhóm nên disable hoặc xóa distribution trước khi xóa bucket static phía sau để tránh lỗi phụ thuộc origin.

### Bước 1 - Xóa Application Load Balancer

- Vào **EC2 > Load Balancers**.
- Chọn đúng ALB của CloudDoc.
- Xóa listener hoặc target group nếu cần theo dependency thực tế.
- Nhấn **Delete load balancer** và chờ trạng thái xóa hoàn tất.

ALB cần được xóa trước để giải phóng liên kết tới target group và các EC2 backend.

### Bước 2 - Dừng và xóa EC2

- Vào **EC2 > Instances**.
- Kiểm tra lại các instance thuộc môi trường CloudDoc.
- Nếu có dữ liệu cần giữ, sao lưu trước khi terminate.
- Thực hiện **Terminate instance**.

Đối với mô hình dùng IAM Role gắn vào EC2, việc terminate instance cũng đồng nghĩa ngắt môi trường chạy backend và dừng quyền tạm thời tại lớp compute.

### Bước 3 - Xóa RDS PostgreSQL

- Vào **RDS > Databases**.
- Chọn cụm hoặc instance PostgreSQL của CloudDoc.
- Kiểm tra nhu cầu snapshot:
  - Nếu cần lưu dữ liệu, tạo snapshot cuối.
  - Nếu chỉ là môi trường demo, có thể bỏ snapshot để giảm chi phí phát sinh.
- Thực hiện **Delete** và xác nhận.

Với cấu hình Multi-AZ, cần chờ hệ thống xóa xong cả primary và standby.

### Bước 4 - Xóa SQS, CloudWatch và SNS

- Vào **SQS** và xóa queue xử lý tài liệu nền nếu đã tạo.
- Vào **CloudWatch** và xóa:
  - log group của backend,
  - custom dashboard,
  - alarm CPU `>= 80%`,
  - metric filter hoặc agent config liên quan nếu có.
- Vào **SNS** và xóa topic gửi cảnh báo email sau khi chắc chắn không còn subscriber cần dùng.

Bước này giúp tránh việc alarm, log retention hoặc queue tồn tại âm thầm sau khi tài nguyên chính đã dừng.

### Bước 5 - Xóa S3 Bucket

- Vào **S3** và mở bucket static, bucket upload nếu có tách riêng.
- Xóa toàn bộ object, version, delete marker và multipart upload còn tồn tại.
- Kiểm tra lại lifecycle rule nếu bucket chưa rỗng.
- Thực hiện **Delete bucket**.

Bucket S3 phải được làm rỗng hoàn toàn trước khi xóa. Đây là bước rất hay bị sót nếu trong bucket còn file upload test, file frontend build hoặc dữ liệu phát sinh từ demo.

### Bước 6 - Xóa VPC

- Vào **VPC** và kiểm tra các thành phần còn phụ thuộc:
  - subnets,
  - route tables,
  - security groups,
  - internet gateway,
  - NAT resource,
  - endpoints.
- Chỉ xóa VPC khi các thành phần con đã được dọn xong.
- Thực hiện **Delete VPC**.

VPC là lớp hạ tầng cuối cùng nên luôn được xóa sau cùng để tránh lỗi dependency.

### Checklist trước khi kết thúc

Trước khi xem môi trường đã cleanup hoàn tất, cần xác nhận:

- Không còn ALB active.
- Không còn EC2 instance chạy.
- Không còn RDS PostgreSQL tính phí.
- Không còn queue SQS, alarm CloudWatch hay topic SNS thừa.
- Bucket S3 đã rỗng và bị xóa.
- VPC demo không còn tồn tại.

### Ý nghĩa đối với báo cáo

Phần clean-up rất quan trọng vì nó chứng minh nhóm không chỉ biết tạo tài nguyên mà còn biết cách kết thúc tài nguyên đúng thứ tự, đúng dependency và đúng tinh thần **FinOps**. Đây là một trong những dấu hiệu cho thấy workshop mang tính thực hành thật chứ không chỉ là mô tả ý tưởng.
