---
title: "CloudDoc là gì?"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1.1. </b> "
---


#### Định nghĩa

CloudDoc là hệ thống chia sẻ tài liệu học tập dành cho sinh viên, trong đó tài liệu không được công bố ngay sau khi tải lên mà phải đi qua bước lưu trữ, ghi nhận metadata, kiểm duyệt và đồng bộ trạng thái trước khi hiển thị cho người dùng cuối. Mô hình này phù hợp với các nền tảng có nội dung do người dùng đóng góp vì nó giúp kiểm soát chất lượng tài liệu, hạn chế nội dung không phù hợp và tạo ra một nguồn học liệu có thể quản lý được.

#### Bài toán dự án cần giải quyết

CloudDoc được thiết kế để giải quyết đồng thời nhiều yêu cầu kỹ thuật và nghiệp vụ:

- người dùng cần tải file lên nhanh và đơn giản từ giao diện web,
- backend không nên trở thành nút nghẽn khi phải truyền file dung lượng lớn,
- metadata phải được lưu có cấu trúc để phục vụ tìm kiếm và kiểm duyệt,
- trạng thái của tài liệu phải được theo dõi xuyên suốt vòng đời sử dụng,
- và tài nguyên AWS phải có khả năng quan sát, cảnh báo và dọn dẹp sau khi kiểm thử.

#### Vì sao workflow này quan trọng?

Nếu chỉ xây một chức năng upload đơn thuần thì dự án mới giải được phần đầu của bài toán. Giá trị thật của CloudDoc nằm ở việc biến một file mới tải lên thành một tài liệu có thể quản lý, phê duyệt, tìm kiếm và phân phối lại một cách nhất quán. Vì vậy, workshop này không dừng ở bước lưu file lên S3 mà còn mở rộng sang moderation, update trạng thái hiển thị, preview, download và monitoring hệ thống.

#### Vòng đời tài liệu trong CloudDoc

Một tài liệu trong hệ thống sẽ đi qua các trạng thái chính sau:

1. `pending`: tài liệu vừa được tải lên và chờ kiểm duyệt.
2. `approved`: tài liệu đã được quản trị viên phê duyệt trong khu vực quản trị.
3. `available`: tài liệu đã đủ điều kiện hiển thị ở trang tìm kiếm, xem trước và tải xuống.

Trong workshop, việc chứng minh được ba trạng thái này bằng cả mô tả luồng, code snippet và ảnh AWS Console sẽ giúp phần báo cáo thể hiện rõ dự án đã được triển khai thật chứ không chỉ dừng ở mức ý tưởng.
