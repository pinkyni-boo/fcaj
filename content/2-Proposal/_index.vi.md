---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
## Hệ thống quản lý và tra cứu tài liệu học tập thông minh theo định hướng triển khai trên AWS

### 1. Tóm tắt điều hành
CloudDoc là nền tảng hỗ trợ sinh viên HUTECH lưu trữ, tìm kiếm, chia sẻ và khai thác tài liệu học tập như giáo trình, slide, đề cương, bài tập và đề thi. Bài toán mà hệ thống hướng đến không chỉ là có nơi để tải file lên, mà là xây dựng một thư viện học liệu có cấu trúc, có kiểm duyệt và có khả năng mở rộng lâu dài.

Trong phạm vi thực tập, tôi tham gia chính ở mảng frontend, đồng thời hỗ trợ nhóm kết nối luồng giao diện với backend, metadata và hạ tầng AWS. Vì vậy, bản đề xuất này vừa phản ánh góc nhìn sản phẩm, vừa phản ánh tư duy kỹ thuật để đưa CloudDoc từ một đồ án học tập thành một hệ thống có thể triển khai trên cloud.

Điểm quan trọng của CloudDoc là hệ thống không được thiết kế như một website upload file đơn giản. Thay vào đó, kiến trúc được tách lớp rõ ràng giữa giao diện, logic nghiệp vụ, metadata tài liệu và object storage. Cách tiếp cận này giúp hệ thống dễ mở rộng hơn về hiệu năng, bảo mật và vận hành.

### 2. Tuyên bố vấn đề
Trong môi trường học tập hiện nay, tài liệu thường bị phân tán trên Google Drive cá nhân, nhóm chat, link tạm thời hoặc thư mục nội bộ thiếu tổ chức. Điều này dẫn đến nhiều vấn đề:

- Sinh viên tốn thời gian tìm lại tài liệu đúng môn học hoặc đúng phiên bản.
- Chất lượng tài liệu khó kiểm soát vì không có cơ chế duyệt và gắn metadata thống nhất.
- Tài liệu dễ bị trùng lặp, thất lạc hoặc mất giá trị khi link cũ hết hiệu lực.
- Người dùng mới khó xác định tài liệu nào đáng tin cậy và còn phù hợp.

**Vấn đề hiện tại**

Nếu xây dựng hệ thống theo mô hình đơn giản, nghĩa là toàn bộ upload và download đều đi qua application server, backend sẽ nhanh chóng trở thành nút nghẽn khi số lượng tài liệu và lưu lượng tăng. Ngoài ra, khi file và metadata không tách riêng, hệ thống khó mở rộng phần tìm kiếm, kiểm duyệt, preview và phân quyền.

Một vấn đề khác là nhiều hệ thống chỉ giải quyết phần lưu file, nhưng chưa giải quyết tốt phần khai thác tài liệu. Nếu không có metadata như trường, ngành, môn học, người đăng, trạng thái duyệt và lượt sử dụng, trải nghiệm tra cứu sẽ kém hiệu quả và dữ liệu sẽ dần trở nên lộn xộn.

**Giải pháp đề xuất**

CloudDoc được đề xuất theo cấu trúc sau:

- Frontend React cung cấp trải nghiệm tìm kiếm, upload, preview và quản trị tài liệu.
- Backend Node.js/Express xử lý logic nghiệp vụ, xác thực, phân quyền và cấp presigned URL.
- PostgreSQL lưu metadata tài liệu, thông tin người dùng, trạng thái duyệt và thống kê tải.
- Amazon S3 lưu file gốc để giảm tải cho backend và phù hợp với mô hình object storage.
- Các dịch vụ mở rộng như CloudFront, SQS, CloudWatch, SNS và Glacier được đưa vào định hướng để tăng hiệu năng, xử lý nền, giám sát và tối ưu chi phí.

Mấu chốt của giải pháp là cho frontend upload trực tiếp lên S3 bằng presigned URL, trong khi backend tập trung vào metadata và nghiệp vụ. Kiến trúc này phù hợp hơn cho một nền tảng tài liệu số có xu hướng tăng trưởng cả về dung lượng lẫn số lượng người dùng.

### 3. Kiến trúc giải pháp
Kiến trúc dưới đây mô tả định hướng triển khai CloudDoc trên AWS với lớp phân phối nội dung, lớp ứng dụng, lớp dữ liệu và lớp giám sát vận hành:

<img src="/images/2-Proposal/aws-drawio-cloudoc.png" alt="CloudDoc AWS Architecture" style="max-width: 90%; height: auto;">

**Mô tả các thành phần chính**

- **Amazon CloudFront và Amazon S3 (Static):** phân phối frontend tĩnh nhanh hơn tới người dùng, giảm độ trễ và giảm tải cho backend.
- **Internet Gateway và Application Load Balancer:** đóng vai trò lớp tiếp nhận và định tuyến request vào backend.
- **Amazon EC2:** chạy backend Express, cấp presigned URL, nhận metadata và xử lý logic nghiệp vụ.
- **Amazon RDS PostgreSQL:** lưu metadata tài liệu, tài khoản, trạng thái phê duyệt và thông tin phục vụ tra cứu.
- **Amazon S3 (Upload):** lưu file gốc và hỗ trợ luồng upload trực tiếp từ frontend.
- **Amazon SQS:** là hướng mở rộng cho các tác vụ bất đồng bộ như quét file, trích xuất metadata hoặc indexing.
- **Amazon CloudWatch và Amazon SNS:** hỗ trợ logging, monitoring, alerting và phản ứng sớm với sự cố.
- **Amazon S3 Glacier:** tối ưu chi phí lưu trữ dài hạn cho tài liệu cũ, ít truy cập.

**Ý nghĩa kiến trúc đối với CloudDoc**

Kiến trúc này cho thấy CloudDoc không chỉ là bài tập giao diện, mà là một hệ thống có lớp phân phối nội dung, lớp xử lý ứng dụng, lớp dữ liệu giao dịch, lớp lưu trữ object và lớp giám sát. Đây là nền tảng cần thiết nếu dự án muốn phát triển tiếp sau kỳ thực tập.

### 4. Triển khai kỹ thuật
Trong kỳ thực tập, nhóm tập trung vào những phần khả thi và bám sát codebase hiện có:

- Xây dựng frontend React cho Home, Search, Upload, Preview, User Profile và Admin Dashboard.
- Thiết kế luồng đăng nhập mô phỏng, phân quyền sinh viên và quản trị viên.
- Chuẩn hóa cấu trúc metadata tài liệu phục vụ tìm kiếm, quản lý và kiểm duyệt.
- Chuẩn bị luồng upload theo mô hình presigned URL.
- Hỗ trợ tích hợp backend Express với PostgreSQL và S3 ở mức phù hợp cho demo.

Điều này cũng có nghĩa là không phải mọi thành phần trong sơ đồ kiến trúc đều đã được triển khai đầy đủ 100%. Một số dịch vụ như SQS, CloudWatch, SNS hoặc Glacier hiện đóng vai trò định hướng mở rộng hợp lý hơn là phần đã hoàn thiện hoàn toàn. Việc trình bày rõ như vậy giúp báo cáo trung thực hơn với phạm vi thực tế.

### 5. Lộ trình và mốc triển khai
**Giai đoạn 1: Hoàn thiện sản phẩm lõi**

- Ổn định trải nghiệm tìm kiếm, upload, preview và điều hướng người dùng.
- Chuẩn hóa metadata và quy trình duyệt tài liệu.
- Hoàn thiện dashboard quản trị và thống kê cơ bản.

**Giai đoạn 2: Tích hợp cloud thực tế**

- Kết nối ổn định hơn giữa frontend, backend Express và PostgreSQL.
- Hoàn thiện upload trực tiếp lên S3 bằng presigned URL.
- Chuẩn hóa môi trường cấu hình và kiểm thử end-to-end.

**Giai đoạn 3: Mở rộng hệ thống**

- Bổ sung background processing cho các tác vụ nặng hoặc bất đồng bộ.
- Thêm monitoring, alerting và logging cho môi trường sẵn sàng triển khai.
- Tối ưu chi phí bằng lifecycle policy và phân tầng dữ liệu lâu năm.

### 6. Ước tính ngân sách
Ảnh dưới đây là bản ước lượng chi phí tháng cho kiến trúc CloudDoc theo mô hình gần production, được tổng hợp từ AWS Pricing Calculator và xuất vào ngày **17/06/2026**:

<img src="/images/2-Proposal/aws-monthly-cost-cloudoc.jpg" alt="CloudDoc AWS Monthly Cost" style="max-width: 90%; height: auto;">

| Hạng mục | Chi phí ước tính / tháng (USD) | Ghi chú |
| --- | ---: | --- |
| RDS PostgreSQL Multi-AZ | 85.50 | Thành phần chiếm tỷ trọng lớn nhất vì ưu tiên tính sẵn sàng |
| EC2 Server (t4g.micro x2) | 19.51 | Hai máy ứng dụng ở hai AZ |
| Application Load Balancer | 18.98 | Phân phối tải và đảm bảo điểm vào thống nhất |
| NAT Instance (t4g.nano) | 4.64 | Hỗ trợ outbound traffic cho private subnet |
| CloudWatch | 4.01 | Metric, log và alarm cơ bản |
| Khác (SNS, CloudFront) | 0.89 | Chi phí nhỏ cho cảnh báo và phân phối nội dung |
| **Tổng cộng** | **133.53** | Mức chi phí tham chiếu cho kiến trúc định hướng |

Mức chi phí trên phù hợp hơn với một kiến trúc định hướng production hoặc demo hoàn chỉnh, không phải cấu hình tối thiểu cho môi trường học tập. Đối với giai đoạn thực tập hoặc thử nghiệm, nhóm có thể giảm chi phí bằng các cách sau:

- Dùng cấu hình đơn AZ cho môi trường dev/test trước khi cần mức sẵn sàng cao hơn.
- Tắt hoặc thu nhỏ EC2 khi không cần chạy liên tục.
- Tận dụng S3 lifecycle để chuyển dữ liệu ít dùng sang Glacier.
- Chỉ bật CloudWatch log chi tiết cho các thành phần thật sự cần theo dõi.
- Tận dụng IAM Role và S3 Gateway Endpoint để giảm rủi ro cấu hình sai thay vì hard-code access key.

### 7. Đánh giá rủi ro
| Rủi ro | Tác động | Cách giảm thiểu |
| --- | --- | --- |
| Sai lệch giữa frontend, backend và luồng presigned URL | Upload lỗi, dữ liệu không đồng bộ | Chuẩn hóa API contract, test từng bước và test end-to-end trước khi demo |
| Metadata không nhất quán hoặc thiếu kiểm duyệt | Tìm kiếm kém hiệu quả, tài liệu lộn xộn | Định nghĩa metadata bắt buộc, thêm trạng thái duyệt và quy trình admin review |
| Cấu hình quyền truy cập AWS chưa chặt chẽ | Rò rỉ dữ liệu hoặc thao tác vượt quyền | Áp dụng IAM Role, Principle of Least Privilege và tránh hard-code key trong source code |
| Chi phí tăng cao nếu giữ kiến trúc lớn cho môi trường dev | Lãng phí ngân sách khi hệ thống chưa có tải thật | Phân tách môi trường dev/demo, giảm tài nguyên và theo dõi cost định kỳ |
| Thiếu quan sát vận hành khi hệ thống lỗi | Khó phát hiện và xử lý sự cố kịp thời | Thiết lập metric, log, CloudWatch Alarm và SNS notification cho các điểm quan trọng |
| Phạm vi thực tập không đủ để hoàn thiện toàn bộ kiến trúc | Báo cáo dễ bị hiểu là overclaim | Ghi rõ phần nào đã làm, phần nào là định hướng mở rộng và minh họa bằng roadmap |

### 8. Kết quả kỳ vọng
CloudDoc mang lại giá trị ở cả ba góc độ:

- **Đối với người dùng cuối:** sinh viên có một nơi tập trung để tìm kiếm và khai thác tài liệu nhanh hơn, đáng tin cậy hơn.
- **Đối với nhóm phát triển:** dự án kết nối frontend, backend, metadata design và tư duy kiến trúc cloud trong cùng một sản phẩm.
- **Đối với định hướng học tập:** dự án là cầu nối giữa UI/UX, nghiệp vụ thực tế và triển khai hệ thống trên AWS.

Từ góc nhìn cá nhân, bản đề xuất này cũng phản ánh quá trình tôi chuyển từ suy nghĩ làm giao diện cho đẹp sang thiết kế trải nghiệm phải đi cùng luồng dữ liệu, bảo mật, chi phí và vận hành hệ thống. Đó là giá trị học tập lớn nhất mà CloudDoc mang lại cho tôi trong kỳ thực tập này.
