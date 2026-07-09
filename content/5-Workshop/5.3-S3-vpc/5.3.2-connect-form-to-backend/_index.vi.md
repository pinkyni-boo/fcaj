---
title: "Kiểm tra lưu trữ và đồng bộ dữ liệu"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---


#### Mục tiêu

Sau khi upload hoàn tất, cần xác minh rằng file vật lý và metadata nghiệp vụ đều đã được hệ thống ghi nhận đúng. Nếu chỉ có object trên S3 mà không có metadata trong cơ sở dữ liệu, tài liệu sẽ không thể đi tiếp sang bước kiểm duyệt và hiển thị.

#### Các bước kiểm tra lưu trữ

Sau khi upload hoàn tất, cần xác minh:

**Bước 1:** Kiểm tra **File đã xuất hiện trong S3 bucket** chưa. Nếu có object mới nghĩa là luồng upload trực tiếp bằng presigned URL đã thành công.

<img src="/images/5-Workshop/AWS-Console/s3-object-created.png" alt="Object mới đã xuất hiện trong S3 sau khi người dùng upload tài liệu" style="max-width: 90%; height: auto;">

**Bước 2:** Xác nhận **Metadata đã được ghi vào cơ sở dữ liệu**.

**Bước 3:** Đảm bảo **Tài liệu xuất hiện trong khu vực moderation** của Admin.

**Bước 4:** Trạng thái ban đầu của tài liệu phải được hệ thống đặt mặc định là `pending`.

#### Kết quả mong đợi

Tại thời điểm này, tài liệu đã hoàn thành bước ingest ban đầu, có cả file trên S3 lẫn metadata trong hệ thống và sẵn sàng đi tiếp vào quy trình kiểm duyệt của CloudDoc.
