---
title: "Bảo mật, vận hành và định hướng mở rộng AWS"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---
### Bảo mật cơ bản

- Chỉ backend mới được phép sinh presigned URL.
- Quyền S3 nên giới hạn đúng bucket và đúng hành động.
- Cơ sở dữ liệu chỉ mở cho backend truy cập, không public trực tiếp.
- Áp dụng rõ nguyên tắc **Least Privilege** cho IAM Role gắn vào EC2.
- Không hard-code `Access Key` hoặc `Secret Key` vào file `.env`; backend lấy quyền tạm thời an toàn thông qua **IAM Role** và **IMDSv2**.

### Vận hành

- Theo dõi lỗi upload, lỗi CORS và các phản hồi thất bại từ backend.
- Ghi log cho quá trình tạo presigned URL, lưu metadata và download tài liệu.
- Chuẩn bị dashboard theo dõi để nhóm dễ phát hiện lỗi tích hợp.
- Cấu hình **CloudWatch Agent** để thu thập log backend, log xử lý hàng đợi và các metric vận hành quan trọng.
- Tạo **CloudWatch Alarm** cho CPU `>= 80%` liên tục trong `2` chu kỳ, mỗi chu kỳ `5 phút`.
- Gửi cảnh báo qua **Amazon SNS Topic** để nhóm nhận email khi hệ thống vào trạng thái `IN ALARM`.

### Định hướng mở rộng

Khi CloudDoc phát triển lớn hơn, có thể mở rộng thêm:

- **SQS** để xử lý tác vụ nền như trích xuất nội dung hoặc quét tài liệu.
- **CloudWatch và SNS** để giám sát và cảnh báo.
- **Lifecycle Policy và Glacier** để tối ưu chi phí lưu trữ lâu dài.

### Ý nghĩa đối với checklist chấm điểm

Phần này rất quan trọng vì nó chứng minh workshop không chỉ dừng ở mức upload được file. Một hệ thống đủ tốt còn cần:

- mô hình cấp quyền an toàn bằng IAM Role,
- cơ chế giám sát log và metric,
- cảnh báo tự động khi tài nguyên vượt ngưỡng,
- và tư duy kiểm soát chi phí dài hạn.

### Ý nghĩa thực tế

Phần bảo mật và vận hành cho thấy một workshop tốt không dừng ở mức “làm sao để tính năng chạy được”. Một giải pháp phù hợp còn phải nghĩ đến kiểm soát quyền, cách phát hiện lỗi, cách theo dõi hệ thống và hướng mở rộng trong tương lai. Đây là điểm giúp workshop gắn sát hơn với tinh thần thực tế của FCAJ và dự án CloudDoc.
