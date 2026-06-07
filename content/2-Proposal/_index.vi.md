---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# CloudDoc Platform for HUTECH Students
## Hệ thống quản lý và tra cứu tài liệu học tập thông minh tích hợp Full-text Search trên AWS

### 1. Tóm tắt điều hành
Nền tảng CloudDoc được thiết kế nhằm giải quyết bài toán lưu trữ và tra cứu tài liệu học tập như slide, giáo trình và đề thi cho sinh viên HUTECH. Hệ thống cho phép tìm kiếm sâu bên trong nội dung tệp tin bằng Full-text Search với tốc độ mili giây và hỗ trợ tải tệp trực tiếp lên kho lưu trữ đám mây một cách an toàn. Giải pháp sử dụng Amazon S3, DynamoDB, OpenSearch kết hợp với máy chủ Amazon EC2 để đảm bảo hiệu năng cao, đồng thời áp dụng tư duy FinOps thông qua vòng đời lưu trữ tự động nhằm tối ưu chi phí vận hành.

### 2. Tuyên bố vấn đề
**Vấn đề hiện tại**

Các hệ thống chia sẻ tài liệu hiện nay của sinh viên phần lớn vẫn mang tính thủ công, chủ yếu chia sẻ qua các liên kết Google Drive rời rạc. Khi tìm kiếm trên các nền tảng nội bộ, người dùng chỉ có thể tra cứu theo tên tệp. Nếu máy chủ phải quét trực tiếp nội dung PDF hoặc Word để tìm từ khóa, hệ thống sẽ xử lý tuyến tính, dễ gây quá tải và treo server. Ngoài ra, việc lưu trữ vĩnh viễn các tài liệu cũ ít được truy cập làm lãng phí tài nguyên và tăng chi phí hạ tầng.

**Giải pháp**

CloudDoc sử dụng Amazon EC2 làm máy chủ trung tâm chạy Node.js/Express để xử lý nghiệp vụ, phân quyền và giao tiếp với Frontend React. Tệp gốc không được lưu trên ổ cứng máy chủ mà được đưa lên Amazon S3, kết hợp S3 Lifecycle Policy để tự động chuyển các tài liệu ít truy cập sang lớp lưu trữ lạnh S3 Glacier. Đối với bài toán tìm kiếm, hệ thống dùng luồng xử lý nền để bóc tách văn bản từ tài liệu và nạp vào Amazon OpenSearch Service dưới dạng chỉ mục đảo. Siêu dữ liệu nhẹ như tên file, danh mục, người tải lên và lượt tải được lưu trong Amazon DynamoDB. Quá trình upload được tối ưu qua S3 Presigned URL, cho phép trình duyệt gửi tệp trực tiếp lên S3 mà không phải truyền qua EC2.

**Lợi ích và hoàn vốn đầu tư (ROI)**

Giải pháp tạo ra một cổng thông tin học liệu tập trung, giúp sinh viên tìm đúng tài liệu ngay cả khi gõ sai chính tả hoặc không dấu. Về vận hành hạ tầng, hệ thống có thể tiết kiệm đến khoảng 80% chi phí lưu trữ nhờ sử dụng S3 Glacier cho các tài liệu trên 30 ngày không có truy cập. Cơ chế Direct Upload cũng giúp giảm tải băng thông cho EC2. Nhóm tận dụng bộ dữ liệu mẫu từ chính học liệu HUTECH nên hầu như không phát sinh chi phí thu thập dữ liệu đầu vào.

### 3. Kiến trúc giải pháp
Nền tảng phân tách rõ ràng giữa lớp giao diện người dùng và lớp tính toán, lưu trữ. Dữ liệu được quản lý đồng bộ giữa cơ sở dữ liệu NoSQL và bộ máy tìm kiếm chuyên sâu.

![CloudDoc Edge Architecture](/images/2-Proposal/edge_architecture.jpeg)

![CloudDoc Platform Architecture](/images/2-Proposal/platform_architecture.jpeg)

**Dịch vụ AWS sử dụng**

- **Amazon EC2:** Host mã nguồn Backend Node.js, tiếp nhận API và xử lý các tác vụ bóc tách văn bản.
- **Amazon S3 và S3 Glacier:** Lưu trữ file tài liệu vật lý và tự động chuyển lớp lưu trữ lạnh sau 30 ngày.
- **Amazon DynamoDB:** Lưu siêu dữ liệu như tên file, cấu trúc danh mục, thông tin người dùng và lượt tải.
- **Amazon OpenSearch Service:** Lưu chỉ mục văn bản và phục vụ tìm kiếm mờ.

**Thiết kế thành phần**

- **Frontend:** Xây dựng bằng React và Tailwind CSS, cung cấp bộ lọc 3 tầng `Trường -> Ngành -> Môn` và thanh tìm kiếm thông minh.
- **Luồng tải lên:** EC2 cấp S3 Presigned URL để trình duyệt đẩy file trực tiếp lên S3.
- **Đồng bộ dữ liệu:** ID của bản ghi trên DynamoDB được thiết kế đồng nhất với `_id` trên OpenSearch để truy xuất chéo nhanh chóng.

### 4. Triển khai kỹ thuật
**Các giai đoạn triển khai**

Dự án được chia thành 2 phân hệ chính là Frontend UI/UX và Cloud Infrastructure, triển khai qua 4 giai đoạn:

1. **Thiết kế hệ thống:** Vẽ sơ đồ kiến trúc, thiết kế UI/UX trên Figma và xác định cấu trúc bảng DynamoDB.
2. **Khởi tạo nền tảng:** Tạo VPC, cài đặt EC2, tạo các S3 bucket và thiết lập quyền IAM.
3. **Phát triển và tích hợp:** Lập trình React components, viết API Node.js cấp Presigned URL và xây dựng luồng bóc tách văn bản để đẩy dữ liệu vào OpenSearch.
4. **Kiểm thử và tối ưu:** Kiểm tra Full-text Search, xác thực S3 Lifecycle, đo độ trễ mạng và dọn dẹp tài nguyên.

**Yêu cầu kỹ thuật**

- **Frontend:** Thành thạo React State Management, xử lý bất đồng bộ bằng Promise/Async-await, tích hợp iframe hoặc `react-pdf` cho Document Preview.
- **Cloud/Backend:** Hiểu Node.js, AWS SDK, nguyên lý CORS, IAM Policy, cách đồng bộ dữ liệu NoSQL và cấu trúc Inverted Index của OpenSearch.

### 5. Lộ trình và mốc triển khai
- **Tháng 1:** Tìm hiểu AWS services, lên ý tưởng, thiết kế sơ đồ kiến trúc và thu thập dữ liệu mẫu như slide và đề cương.
- **Tháng 2:** Dựng giao diện web, khởi tạo tài nguyên AWS như EC2, S3, DynamoDB và thiết lập môi trường Backend.
- **Tháng 3:** Hoàn thiện luồng upload trực tiếp, tích hợp OpenSearch, kiểm thử tính năng tìm kiếm mờ, đóng gói tài liệu hướng dẫn và quay video demo.

### 6. Ước tính ngân sách
- **Amazon EC2 (t2.micro):** Nằm trong Free Tier, khoảng 0.00 USD/tháng.
- **Amazon S3 Standard và Glacier:** Lưu trữ dự kiến 10 GB dữ liệu, khoảng 0.25 USD/tháng.
- **Amazon DynamoDB:** Tải đọc/ghi thấp, chủ yếu metadata, nằm trong Free Tier.
- **Amazon OpenSearch (t3.small.search):** Dịch vụ cốt lõi, khoảng 15.00 đến 25.00 USD/tháng.
- **Băng thông truyền dữ liệu:** Tối ưu nhờ Presigned URL, khoảng 0.50 USD/tháng.

**Tổng chi phí dự kiến:** khoảng 25.75 USD/tháng, trong đó OpenSearch là thành phần chiếm chi phí lớn nhất.

### 7. Đánh giá rủi ro
**Ma trận rủi ro**

- **Nghẽn băng thông server:** Ảnh hưởng cao, xác suất thấp.
- **Lỗi đồng bộ dữ liệu:** Ảnh hưởng cao, xác suất trung bình.
- **Vượt ngân sách do OpenSearch chạy 24/7:** Ảnh hưởng trung bình, xác suất trung bình.

**Chiến lược giảm thiểu**

- **Luồng dữ liệu:** Validate dung lượng file nhỏ hơn 20 MB ngay từ phía trình duyệt trước khi gọi API.
- **Đồng bộ dữ liệu:** Xây dựng cơ chế rollback hoặc transaction nếu ghi DynamoDB thành công nhưng đồng bộ OpenSearch thất bại.
- **Chi phí:** Thiết lập AWS Budgets và CloudWatch Alarms để gửi email cảnh báo khi ngân sách vượt ngưỡng.

### 8. Kết quả kỳ vọng
**Về kỹ thuật:** Xây dựng thành công một web app với kiến trúc cloud hiện đại, xử lý tốt luồng upload và tra cứu tài liệu học tập bằng Full-text Search.

**Về giá trị:** Chứng minh được năng lực thiết kế hạ tầng tối ưu chi phí thông qua vòng đời lưu trữ và pipeline dữ liệu an toàn, đồng thời tạo tiền đề để mở rộng hệ thống cho nhiều trường đại học khác trong tương lai.
