---
title: "Tích hợp ứng dụng khách và quan sát hệ thống"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---


#### Mục tiêu

Sau khi tài liệu đã được phê duyệt, người dùng cần có khả năng tương tác lại với tài liệu theo cách tự nhiên trên ứng dụng, ví dụ như xem trước hoặc tải xuống. Đồng thời, một workshop hoàn chỉnh cũng phải thể hiện phần quan sát vận hành để chứng minh nhóm không chỉ triển khai hạ tầng mà còn theo dõi được trạng thái chạy của hệ thống. Vì vậy, mục này kết hợp cả phần tích hợp ứng dụng khách lẫn monitoring trên AWS.

#### Các bước tích hợp và quan sát

**Bước 1:** Frontend thực hiện lấy dữ liệu tài liệu từ backend thông qua phân phối **CloudFront** để đảm bảo hiệu năng và bảo mật.

<img src="/images/5-Workshop/AWS-Console/cloudfront-details.png" alt="Màn hình phân phối CloudFront của frontend CloudDoc" style="max-width: 90%; height: auto;">

**Bước 2:** Khi người dùng bấm vào tài liệu đã duyệt, frontend lấy thông tin truy cập qua backend để backend cấp URL an toàn cho việc **xem trước (preview)** và **tải xuống (download)**.

<img src="/images/5-Workshop/AWS-Console/preview-download.png" alt="Màn hình xem trước và tải xuống tài liệu đã duyệt" style="max-width: 90%; height: auto;">

**Bước 3:** Ở phía vận hành, **CloudWatch** được sử dụng để thu thập log và metric, giúp nhóm kiểm tra log runtime của hệ thống.

<img src="/images/5-Workshop/AWS-Console/cloudwatch-logs-metrics.jpg" alt="Màn hình CloudWatch log groups và metrics dùng để theo dõi backend CloudDoc" style="max-width: 90%; height: auto;">

**Bước 4:** Cấu hình **CloudWatch Alarm** để tự động theo dõi và cảnh báo các bất thường của môi trường chạy, ví dụ như CPU tăng cao.

<img src="/images/5-Workshop/AWS-Console/cloudwatch-alarm.jpg" alt="Màn hình CloudWatch alarm dùng để cảnh báo trạng thái tài nguyên backend" style="max-width: 90%; height: auto;">

#### Ghi chú kỹ thuật

Ở phần thuyết minh kiến trúc, mục này cũng là nơi phù hợp để nhấn mạnh rằng hệ thống không hard-code access key ở phía client, đồng thời việc giám sát bằng CloudWatch là bằng chứng cho năng lực vận hành và tối ưu hệ thống sau triển khai.
