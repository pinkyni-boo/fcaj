---
title: "Blog 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

Blog thứ ba tôi chọn dịch nói về một vấn đề bảo mật và vận hành rất thiết thực: khi xây dựng các ứng dụng server-side rendering như **Next.js** hoặc **Nuxt** trên AWS, làm sao để phần server của ứng dụng có thể truy cập tài nguyên AWS một cách an toàn mà không cần lưu `Access Key` hoặc `Secret Key` trong source code hay biến môi trường.

AWS đã giới thiệu tính năng **IAM Compute Roles** cho **AWS Amplify Hosting** để giải quyết nhu cầu này. Đây là một điểm tôi đánh giá rất đáng học vì nó gắn trực tiếp với yêu cầu bảo mật mà bất kỳ hệ thống cloud nào cũng cần quan tâm.

### 1. IAM Compute Roles là gì?

IAM Compute Roles cho phép gắn trực tiếp một **IAM Role** vào môi trường thực thi của ứng dụng SSR chạy trên Amplify Hosting. Nhờ đó, code phía server có thể truy cập các dịch vụ AWS thông qua cơ chế cấp quyền tạm thời, tương tự như cách **EC2 Instance Profile** hoặc **Lambda Execution Role** hoạt động.

Ý nghĩa lớn nhất của cơ chế này là:

- Không cần hard-code access key trong ứng dụng.
- Dễ kiểm soát quyền truy cập theo từng môi trường.
- Phù hợp hơn với nguyên tắc **Principle of Least Privilege**.

### 2. Các trường hợp sử dụng phổ biến

Theo bài viết, IAM Compute Roles đặc biệt phù hợp trong các trường hợp:

- Truy cập **AWS Secrets Manager** hoặc **Systems Manager Parameter Store** để lấy thông tin cấu hình.
- Kết nối tới **Amazon RDS** hoặc **Amazon DynamoDB** mà không phải lưu credentials trong ứng dụng.
- Gọi API của các dịch vụ AWS từ phía server.
- Thiết lập quyền truy cập khác nhau cho development, staging và production.

### 3. Ví dụ triển khai

Trong ví dụ của AWS, ứng dụng **Next.js** được cấu hình để truy cập một **Amazon S3 bucket** ở chế độ private. Quy trình chính gồm:

1. Tạo IAM Role có quyền đọc dữ liệu từ S3.
2. Cấp quyền để Amplify Hosting sử dụng role đó.
3. Triển khai ứng dụng Next.js lên Amplify.
4. Dùng AWS SDK trong API Route để truy cập dữ liệu từ S3.

Nhờ IAM Compute Roles, ứng dụng có thể xác thực với AWS mà không cần lưu thông tin nhạy cảm trong source code.

### 4. Điều tôi học được từ bài blog

Bài viết này giúp tôi hiểu rõ hơn rằng bảo mật trong cloud không chỉ nằm ở firewall hay private subnet, mà còn nằm ở cách ứng dụng nhận quyền truy cập tài nguyên. Với vai trò làm frontend và hỗ trợ backend cho CloudDoc, tôi thấy đây là bài học rất quan trọng, vì khi hệ thống phát triển lên các môi trường triển khai thật thì việc quản lý credential và quyền truy cập phải được xử lý bài bản ngay từ đầu.

### 5. Liên hệ với CloudDoc

- CloudDoc nên ưu tiên tư duy dùng **IAM Role** thay vì hard-code access key nếu triển khai trên AWS.
- Các luồng như upload file, lấy presigned URL hoặc truy cập tài nguyên riêng đều cần được thiết kế theo hướng cấp quyền an toàn.
- Bài blog này cũng củng cố thêm phần checklist chấm điểm liên quan tới bảo mật và **least privilege** trong báo cáo FCAJ.

### 6. Kết luận

IAM Compute Roles giúp đơn giản hóa việc quản lý quyền truy cập AWS cho các ứng dụng SSR trên Amplify Hosting. Đây là một tính năng rất hữu ích cho các hệ thống cần truy cập tài nguyên AWS từ phía server nhưng vẫn muốn đảm bảo nguyên tắc bảo mật và quản trị quyền truy cập rõ ràng.

**Link bài đăng trong nhóm FCAJ:** https://www.facebook.com/share/p/1PEvrCKJsS/
