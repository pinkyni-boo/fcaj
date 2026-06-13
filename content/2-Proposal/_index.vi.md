---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# Bản đề xuất: CloudDoc Platform for HUTECH Students
## Hệ thống quản lý và tra cứu tài liệu học tập thông minh tích hợp kiến trúc Sẵn sàng cao trên AWS

### 1. Tóm tắt điều hành
Nền tảng CloudDoc được thiết kế nhằm giải quyết bài toán lưu trữ, quản lý và tra cứu tài liệu học tập như slide, giáo trình và đề thi cho sinh viên HUTECH. Hệ thống cung cấp khả năng tìm kiếm nội dung sâu với tốc độ cao, đồng thời đảm bảo an toàn dữ liệu thông qua kiến trúc mạng nội bộ cô lập với Private Subnet.

Giải pháp sử dụng hệ sinh thái AWS hiện đại gồm Application Load Balancer, Amazon EC2 triển khai theo mô hình Multi-AZ, Amazon RDS PostgreSQL, Amazon SQS, Amazon S3, CloudWatch và SNS để đảm bảo hiệu năng, tính sẵn sàng cao và khả năng xử lý bất đồng bộ. Hệ thống cũng áp dụng tư duy FinOps bằng cách tự động chuyển vòng đời lưu trữ từ Amazon S3 sang S3 Glacier nhằm tối ưu chi phí vận hành dài hạn.

### 2. Tuyên bố vấn đề
**Vấn đề hiện tại**

Các nền tảng chia sẻ tài liệu nội bộ của sinh viên thường được triển khai theo mô hình máy chủ đơn lẻ, dẫn đến rủi ro ngừng dịch vụ khi lượng truy cập tăng cao vào mùa thi. Việc xử lý tệp PDF hoặc Word trực tiếp trên máy chủ làm nghẽn CPU và giảm trải nghiệm người dùng. Ngoài ra, dùng một hệ thống tìm kiếm chuyên biệt cồng kềnh cho phạm vi dự án cấp trường là chưa tối ưu, trong khi việc lưu trữ tài liệu cũ lâu dài trên lớp lưu trữ nóng gây lãng phí chi phí hạ tầng.

**Giải pháp**

CloudDoc áp dụng kiến trúc tách rời và sẵn sàng cao:

- Người dùng truy cập hệ thống qua Application Load Balancer ở Public Subnet.
- Các máy chủ Amazon EC2 và cơ sở dữ liệu RDS PostgreSQL được đặt trong Private Subnet để tăng cường bảo mật.
- Client tải tệp trực tiếp lên Amazon S3 thông qua Presigned URL thay vì đi qua máy chủ ứng dụng.
- Khi có tệp mới trên S3, sự kiện được đẩy vào Amazon SQS để EC2 Worker xử lý bóc tách văn bản theo nền.
- Metadata và dữ liệu tìm kiếm được lưu tập trung trên Amazon RDS PostgreSQL, tận dụng khả năng Full-text Search tích hợp sẵn.
- CloudWatch và SNS theo dõi tài nguyên hệ thống và gửi cảnh báo khi có dấu hiệu quá tải.

**Lợi ích và hoàn vốn đầu tư (ROI)**

Giải pháp tạo ra một cổng học liệu tập trung, tra cứu nhanh, vận hành an toàn và dễ mở rộng. Việc tự động chuyển tài liệu ít truy cập sang S3 Glacier giúp tiết kiệm đáng kể chi phí lưu trữ. Cơ chế tải trực tiếp lên S3 giảm tải băng thông và CPU cho EC2. Việc sử dụng RDS PostgreSQL thay cho một cụm tìm kiếm riêng biệt cũng giúp tối ưu ngân sách cho giai đoạn đầu của dự án.

### 3. Kiến trúc giải pháp
Nền tảng được thiết kế theo hướng phân tách rõ luồng truy cập web và luồng xử lý nền, đồng thời đảm bảo tính sẵn sàng cao nhờ triển khai trên nhiều Availability Zone.

![CloudDoc AWS Architecture](/images/2-Proposal/clouddoc-architecture.png)

**Dịch vụ AWS sử dụng**

- **VPC, Internet Gateway và ALB:** Thiết lập lớp mạng bảo mật và tiếp nhận lưu lượng truy cập từ Internet.
- **Amazon EC2 (Multi-AZ):** Chạy ứng dụng Node.js, xử lý API, tạo Presigned URL và thực hiện các tác vụ nền.
- **Amazon RDS PostgreSQL:** Lưu trữ metadata, dữ liệu nghiệp vụ và hỗ trợ Full-text Search.
- **Amazon S3 và S3 Glacier:** Lưu file tài liệu và tự động chuyển dữ liệu cũ sang lớp lưu trữ lạnh.
- **Amazon SQS:** Tách rời luồng tải tệp và luồng xử lý bóc tách văn bản.
- **Amazon CloudWatch và Amazon SNS:** Giám sát hạ tầng và gửi cảnh báo khi CPU hoặc tài nguyên đạt ngưỡng rủi ro.

**Thiết kế thành phần**

- **Frontend:** Xây dựng bằng React và Tailwind CSS, cung cấp giao diện Upload, Search, Filter và Preview tài liệu.
- **Application Layer:** EC2 App Server tiếp nhận request từ ALB, xử lý logic người dùng và cấp Presigned URL.
- **Background Processing:** EC2 Worker nhận tin nhắn từ SQS để xử lý bóc tách nội dung tài liệu.
- **Storage Layer:** Tệp gốc lưu trên S3, metadata lưu trong RDS PostgreSQL, dữ liệu ít truy cập được chuyển sang Glacier.
- **Monitoring Layer:** CloudWatch thu thập metrics, SNS gửi email cảnh báo khi phát sinh sự cố.

### 4. Triển khai kỹ thuật
**Các giai đoạn triển khai**

1. **Thiết kế và hoạch định:** Hoàn thiện AWS Architecture Diagram, thiết kế UI/UX và chuẩn hóa schema PostgreSQL.
2. **Khởi tạo mạng và tài nguyên:** Cấu hình VPC, Public Subnet, Private Subnet, Security Group, ALB, EC2, RDS và SQS.
3. **Phát triển và tích hợp:** Xây dựng Frontend React, API Node.js, luồng Presigned URL, luồng xử lý nền và Full-text Search trong PostgreSQL.
4. **Giám sát và tối ưu:** Cấu hình CloudWatch Alarm, SNS, kiểm thử tải, tối ưu vòng đời lưu trữ S3 và đo độ ổn định toàn hệ thống.

**Yêu cầu kỹ thuật**

- **Frontend:** React Context API, bất đồng bộ với Fetch/Axios, xử lý form, preview tài liệu.
- **Backend/Cloud:** Node.js, AWS SDK, S3 Presigned URL, SQS, RDS PostgreSQL, Full-text Search, IAM, Security Groups và các nguyên lý mạng AWS cơ bản.

### 5. Lộ trình và mốc triển khai
- **Tháng 1:** Khảo sát yêu cầu, thiết kế sơ đồ hệ thống, dựng giao diện ban đầu trên Figma.
- **Tháng 2:** Khởi tạo VPC, ALB, EC2, RDS PostgreSQL, S3 và xây dựng luồng upload trực tiếp.
- **Tháng 3:** Tích hợp SQS Worker, Full-text Search, CloudWatch, SNS, kiểm thử toàn hệ thống và quay video demo.

### 6. Ước tính ngân sách
- **Amazon EC2 (2 máy nhỏ Multi-AZ):** Tối ưu trong giới hạn học tập và có thể tận dụng Free Tier ở giai đoạn đầu.
- **Amazon RDS PostgreSQL:** Có thể triển khai kích thước nhỏ để tiết kiệm chi phí trong giai đoạn demo.
- **Application Load Balancer:** Là thành phần chi phí chính để duy trì mô hình High Availability.
- **Amazon S3 và S3 Glacier:** Chi phí thấp, tối ưu tốt nhờ Lifecycle Policy.
- **Amazon SQS, CloudWatch và SNS:** Chi phí nhỏ trong quy mô sử dụng hiện tại.

**Tổng chi phí dự kiến:** khoảng 20 đến 25 USD mỗi tháng, chủ yếu tập trung ở ALB và cơ sở dữ liệu RDS.

### 7. Đánh giá rủi ro
| Rủi ro | Mức độ ảnh hưởng | Xác suất | Chiến lược giảm thiểu |
| --- | --- | --- | --- |
| Sự cố hạ tầng cục bộ | Rất cao | Thấp | Triển khai Multi-AZ để tăng khả năng dự phòng |
| EC2 quá tải khi truy cập tăng đột biến | Cao | Trung bình | Sử dụng ALB kết hợp giám sát CloudWatch |
| Nghẽn băng thông do upload tệp lớn | Trung bình | Cao | Dùng Presigned URL và giới hạn dung lượng tải lên |
| Mất dữ liệu xử lý nền | Cao | Thấp | Tách hàng đợi xử lý bằng Amazon SQS |

### 8. Kết quả kỳ vọng
**Về kỹ thuật:** Xây dựng thành công một nền tảng CloudDoc chạy trên kiến trúc AWS hiện đại, có tính sẵn sàng cao, bảo mật tốt và hỗ trợ tìm kiếm nội dung tài liệu hiệu quả.

**Về giá trị:** Hệ thống giúp sinh viên HUTECH tra cứu tài liệu học tập tập trung và nhanh chóng, đồng thời thể hiện rõ năng lực thiết kế hệ thống cloud chuyên nghiệp của nhóm phát triển.
