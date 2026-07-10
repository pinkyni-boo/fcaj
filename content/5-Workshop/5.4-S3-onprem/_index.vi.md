---
title: "Kiểm thử hệ thống end-to-end"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---


#### Mục tiêu

Phần này xác minh rằng tài liệu đã thật sự đi qua toàn bộ workflow của CloudDoc, từ lúc người dùng gửi file, tài liệu xuất hiện trong khu vực moderation, quản trị viên phê duyệt thành công, cho tới khi tài liệu được hiển thị lại ở các màn hình mà người dùng cuối có thể truy cập. Đây là phần quan trọng nhất để chứng minh tính end-to-end của workshop.

#### Bằng chứng demo

Người chấm có thể xem toàn bộ video demo tại đây: [Video demo CloudDoc](https://drive.google.com/drive/folders/1-mvKrbzs08WWHUT0-whSGeNwgtwd4Uid?usp=sharing).

#### Quy trình kiểm thử

Quy trình kiểm thử được thực hiện theo thứ tự sau:

**Bước 1:** Xác nhận tài liệu xuất hiện trong dashboard quản trị với trạng thái chờ duyệt (`pending`).

<img src="/images/5-Workshop/AWS-Console/admin-approve-dashboard.png" alt="Dashboard admin hiển thị tài liệu đang chờ duyệt" style="max-width: 90%; height: auto;">

**Bước 2:** Thực hiện thao tác approve từ phía quản trị viên. Kiểm tra phản hồi thành công (toast message) và trạng thái của tài liệu được cập nhật sang `approved`.

<img src="/images/5-Workshop/AWS-Console/admin-approve-toast.png" alt="Thông báo xác nhận sau khi admin duyệt và xuất bản tài liệu" style="max-width: 90%; height: auto;">

**Bước 3:** Truy cập lại trang tìm kiếm công khai để xác nhận tài liệu đã xuất hiện. Bạn có thể tiếp tục thử hành vi xem trước hoặc tải xuống để bảo đảm tài liệu hiển thị đúng trên giao diện người dùng.

<img src="/images/5-Workshop/AWS-Console/search-result.png" alt="Trang kết quả tìm kiếm hiển thị tài liệu đã được duyệt" style="max-width: 90%; height: auto;">

#### Kết luận kiểm thử

Khi cả ba màn hình trên đều khớp với mô tả nghiệp vụ, nhóm có thể kết luận rằng luồng upload, moderation và publish của CloudDoc hoạt động xuyên suốt giữa frontend, backend, S3 và cơ sở dữ liệu. Đây cũng là căn cứ để ghi nhận rằng dự án đã đáp ứng yêu cầu triển khai end-to-end trong checklist workshop.
