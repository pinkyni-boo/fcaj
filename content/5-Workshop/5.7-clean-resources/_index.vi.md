---
title: "Dọn dẹp tài nguyên"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---


#### Mục tiêu

Sau khi hoàn thành workshop, cần dọn dẹp các tài nguyên tạm để tránh phát sinh chi phí không cần thiết và để thể hiện tư duy vận hành có kiểm soát. Trong các dự án AWS, phần clean-up không phải là bước phụ mà là một nội dung quan trọng giúp chứng minh nhóm hiểu vòng đời tài nguyên và ý thức về chi phí sử dụng dịch vụ.

#### Các bước thực hiện

**Bước 1:** Dọn dữ liệu thử nghiệm trong **S3 bucket** (sau khi đã lưu lại minh họa cần thiết cho báo cáo) để giải phóng dung lượng lưu trữ.

<img src="/images/5-Workshop/AWS-Console/cleanup-s3-bucket.png" alt="Kết quả dọn bucket S3 sau khi xóa dữ liệu test" style="max-width: 90%; height: auto;">

**Bước 2:** Tắt hoặc terminate **EC2** dùng cho backend do môi trường này hiện chỉ phục vụ demo.

<img src="/images/5-Workshop/AWS-Console/cleanup-ec2.png" alt="Thao tác terminate EC2 dùng trong bước dọn backend" style="max-width: 90%; height: auto;">

**Bước 3:** Rà soát các cấu hình quan sát như log group hoặc alarm để quyết định giữ lại hay thu hồi.

**Bước 4:** Kiểm tra lại dependency giữa các tài nguyên trước khi xóa để tránh bỏ sót.

#### Hoàn tất

Sau bước này, môi trường demo của CloudDoc được thu hồi an toàn và sẵn sàng cho lần triển khai hoặc kiểm thử tiếp theo. Việc có ảnh minh họa ở phần clean-up cũng giúp workshop đáp ứng rõ hơn yêu cầu “clean-up resources” trong checklist chấm điểm.
