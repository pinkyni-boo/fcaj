---
title: "Chuẩn bị dữ liệu và cấu hình hệ thống"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2.2. </b> "
---


#### Mục tiêu

Phần này chuẩn bị dữ liệu mẫu và rà soát những cấu hình quan trọng nhất cho luồng upload. Với bài toán upload trực tiếp từ trình duyệt lên S3, các thiết lập như bucket, CORS và thông tin môi trường phải khớp nhau; nếu không, file có thể không được đưa lên thành công dù frontend và backend đều đang chạy.

#### Các bước thực hiện

Trước khi bắt đầu luồng upload trực tiếp từ trình duyệt, bạn cần đảm bảo các cấu hình lưu trữ đã chính xác:

**Bước 1:** Kiểm tra **CORS configuration** trên bucket S3 dùng cho upload để trình duyệt được phép gửi request `PUT` hoặc `POST` trực tiếp.

<img src="/images/5-Workshop/AWS-Console/s3-upload-cors.png" alt="Cấu hình CORS cho bucket dùng trong luồng upload tài liệu" style="max-width: 90%; height: auto;">

**Bước 2:** Cấu hình **Public access** cho bucket frontend, đảm bảo bỏ block tất cả public access để file tĩnh có thể được phục vụ ra ngoài.

<img src="/images/5-Workshop/AWS-Console/frontend-bucket-public-access.png" alt="Thiết lập public access của bucket frontend để phục vụ phân phối tĩnh" style="max-width: 90%; height: auto;">

**Bước 3:** Kích hoạt tính năng **Static website hosting** trên bucket frontend và trỏ index document về `index.html`.

<img src="/images/5-Workshop/AWS-Console/frontend-bucket-static-hosting.jpg" alt="Cấu hình static website hosting của bucket frontend" style="max-width: 90%; height: auto;">

{{% notice info %}}
**Lưu ý:** Ngoài các cấu hình S3 trên, bạn cần chuẩn bị tài liệu mẫu (như 1 file PDF) và đảm bảo các biến môi trường của Frontend/Backend đã khớp nhau.
{{% /notice %}}

#### Kết quả mong đợi

Sau bước này, nhóm có trong tay cả dữ liệu đầu vào lẫn môi trường kỹ thuật phù hợp để thực hiện upload thật, kiểm tra object trên S3 và tiếp tục sang bước ghi metadata.
