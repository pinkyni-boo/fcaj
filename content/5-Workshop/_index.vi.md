---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---


# Xây dựng hệ thống CloudDoc trên AWS

#### Tổng quan workshop

CloudDoc là dự án quản lý và chia sẻ tài liệu học tập dành cho sinh viên. Trong hệ thống này, người dùng có thể gửi tài liệu từ giao diện web, backend tiếp nhận yêu cầu nghiệp vụ, Amazon S3 chịu trách nhiệm lưu trữ file, cơ sở dữ liệu lưu metadata, còn quản trị viên thực hiện kiểm duyệt trước khi tài liệu được công bố rộng rãi. Mục 5 được viết theo dạng workshop end-to-end để người đọc có thể theo dõi trọn vẹn một vòng đời tài liệu thay vì chỉ xem rời rạc từng dịch vụ AWS.

Điểm trọng tâm của workshop là trình bày một luồng kỹ thuật hoàn chỉnh: chuẩn bị môi trường, upload tài liệu, xác nhận file đã được lưu đúng trên AWS, kiểm thử bước kiểm duyệt, đồng bộ dữ liệu hiển thị ra giao diện và cuối cùng là dọn dẹp tài nguyên để tránh phát sinh chi phí không cần thiết. Cách trình bày này giúp bài báo cáo thể hiện được cả phần thiết kế kiến trúc lẫn phần triển khai thực tế, kiểm thử và vận hành.

#### Mục tiêu

Sau khi đọc xong mục này, người xem có thể:

- hiểu vai trò của từng thành phần trong hệ thống CloudDoc,
- theo dõi được luồng upload và phê duyệt tài liệu từ đầu đến cuối,
- đối chiếu ảnh AWS Console với từng bước triển khai trong workshop,
- xem code snippet đại diện cho phần tích hợp frontend và backend,
- và nhận thấy nhóm có thực hiện cả monitoring, validation lẫn clean-up tài nguyên.

#### Kết quả mong đợi

Kết quả cuối cùng của workshop là một hệ thống trong đó người dùng tải tài liệu lên thành công, quản trị viên duyệt tài liệu trong khu vực quản trị, tài liệu đã duyệt xuất hiện tại trang tìm kiếm, người dùng có thể xem trước hoặc tải xuống, đồng thời hệ thống được theo dõi bằng CloudWatch logs, metrics và alarm.

#### Video demo

Người chấm có thể xem video demo CloudDoc tại đây: [Video demo CloudDoc](https://drive.google.com/drive/folders/1-mvKrbzs08WWHUT0-whSGeNwgtwd4Uid?usp=sharing).

#### Cấu trúc workshop

1. [Giới thiệu](5.1-workshop-overview/)
2. [Điều kiện tiên quyết](5.2-prerequiste/)
3. [Triển khai luồng upload và lưu trữ tài liệu](5.3-s3-vpc/)
4. [Kiểm thử hệ thống end-to-end](5.4-s3-onprem/)
5. [Tích hợp ứng dụng khách và quan sát hệ thống](5.5-policy/)
6. [Cập nhật dữ liệu](5.6-cleanup/)
7. [Dọn dẹp tài nguyên](5.7-clean-resources/)
