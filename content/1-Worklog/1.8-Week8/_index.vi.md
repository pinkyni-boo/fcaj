---
title: "Thiết lập dự án Frontend và Thiết kế Kiến trúc hệ thống CloudDoc"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
### Mục tiêu tuần 8:

* Hoàn thiện và chốt bản vẽ sơ đồ kiến trúc hạ tầng đám mây (AWS Architecture Diagram) theo chuẩn Multi-AZ để làm kim chỉ nam cho dự án.
* Khởi tạo dự án ứng dụng Web (Frontend) bằng ReactJS, thiết lập môi trường lập trình và xây dựng các giao diện chức năng cốt lõi (Upload, Tìm kiếm, Bộ lọc) cho hệ thống CloudDoc.
* Kết hợp quá trình tự phát triển với việc tham gia học tập trực tiếp tại văn phòng để trao đổi định hướng kỹ thuật và hoàn thiện giao diện theo góp ý của mentor.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu / Công cụ |
| --- | --- | --- | --- | --- |
| 2 | Hoàn thiện sơ đồ kiến trúc hạ tầng (AWS Architecture):<br>- Vẽ và thiết kế flow kết nối chi tiết giữa VPC, ALB, EC2, RDS PostgreSQL, S3, SQS và CloudWatch.<br>- Rà soát luồng dữ liệu (Data Flow) đảm bảo tính sẵn sàng cao (HA) và bảo mật Private Subnet. | 08/06/2026 | 08/06/2026 |  |
| 3 | Tham gia học tập trực tiếp tại văn phòng kết hợp khởi tạo dự án Frontend & Global State:<br>- Trao đổi với mentor và các thành viên về định hướng giao diện, luồng người dùng và cách tổ chức source code.<br>- Khởi tạo source code ReactJS, tích hợp framework Tailwind CSS.<br>- Thiết lập React Context API (AppContext) để quản lý trạng thái toàn cục (Đăng nhập, Thông báo/Chuông báo). | 09/06/2026 | 09/06/2026 |  |
| 4 | Phát triển giao diện Phân hệ Đăng tải (Upload Module):<br>- Thiết kế Form Upload hỗ trợ kéo thả tệp tin (Drag & Drop).<br>- Xây dựng các trường nhập Metadata và thanh tiến trình tải lên (Progress Bar) mô phỏng thời gian thực. | 10/06/2026 | 10/06/2026 |  |
| 5 | Phát triển Phân hệ Tìm kiếm & Khám phá:<br>- Xây dựng thanh Tìm kiếm trực quan (Search Bar).<br>- Lập trình logic cho Bộ lọc đa tầng động: Liên kết dữ liệu 3 tầng (Trường -> Ngành -> Môn học) tự động thay đổi theo lựa chọn. | 11/06/2026 | 11/06/2026 |  |
| 6 | Tích hợp Trình xem tài liệu & Phân quyền cơ bản:<br>- Tích hợp thẻ iframe (hoặc react-pdf) để xem trước (Preview) tài liệu PDF/Docx trực tiếp trên web.<br>- Cấu hình Role-based Routing (Phân quyền): Ẩn chức năng Upload đối với khách vãng lai. | 12/06/2026 | 12/06/2026 |  |


### Kết quả đạt được tuần 8:

* Chốt duyệt thành công bản vẽ sơ đồ kiến trúc AWS CloudDoc, đáp ứng tiêu chí tối ưu hóa và bảo mật của mentor.
* Kết hợp hiệu quả việc học tập tại văn phòng với quá trình phát triển cá nhân, giúp định hình rõ hơn luồng chức năng và tiêu chuẩn giao diện của hệ thống.
* Thiết lập thành công bộ khung source code Frontend với ReactJS và Tailwind CSS, xử lý mượt mà luồng dữ liệu toàn cục bằng Context API.
* Xây dựng hoàn thiện biểu mẫu Upload hỗ trợ kéo thả và thanh hiển thị phần trăm tiến trình tải lên chuyên nghiệp.
* Lập trình thành công tính năng bộ lọc danh mục 3 tầng tương tác động (Trường -> Ngành -> Môn) và thanh tìm kiếm từ khóa.
* Nhúng thành công trình xem tài liệu trực tuyến vào giao diện, cho phép người dùng đọc PDF trực tiếp với độ trễ thấp.



