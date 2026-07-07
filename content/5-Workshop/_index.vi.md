---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

Workshop này được điều chỉnh theo đúng dự án **CloudDoc** thay vì giữ nội dung lab AWS cũ. Trọng tâm của phần này là mô tả cách thiết kế và triển khai một luồng **upload tài liệu an toàn trên AWS**, trong đó frontend tải file trực tiếp lên Amazon S3 bằng presigned URL, còn backend chịu trách nhiệm quản lý metadata, quyền truy cập và các bước nghiệp vụ liên quan.

Sở dĩ tôi chọn chủ đề này cho workshop vì đây là một phần giao thoa rất rõ giữa frontend, backend và cloud architecture. Khi làm CloudDoc, tôi nhận ra rằng chỉ cần thay đổi cách upload file là toàn bộ tư duy hệ thống cũng thay đổi: backend đỡ bị nghẽn hơn, dữ liệu được tách rõ hơn và hạ tầng cloud được khai thác hợp lý hơn.

### Mục tiêu của workshop

- Mô tả một luồng upload thực tế phù hợp với bài toán quản lý tài liệu.
- Giải thích vì sao presigned URL là giải pháp phù hợp cho CloudDoc.
- Trình bày mối liên hệ giữa frontend form upload, backend API và S3 storage.
- Làm rõ những điểm cần lưu ý về bảo mật, metadata, quyền truy cập và khả năng mở rộng.

### Vì sao chủ đề này phù hợp với CloudDoc

CloudDoc là hệ thống có đặc thù xử lý tài liệu học tập. Điều đó có nghĩa là:

- File có thể nhiều và dung lượng không nhỏ.
- Người dùng cần upload dễ, nhanh và ít lỗi.
- Hệ thống cần lưu metadata rõ ràng để phục vụ tìm kiếm và kiểm duyệt.
- Kiến trúc phải đủ tốt để về sau có thể phát triển thêm các tác vụ nền như trích xuất nội dung hoặc đánh chỉ mục.

Một workshop về presigned URL và S3 upload vì thế phù hợp hơn nhiều so với việc giữ các lab AWS rời rạc không liên hệ trực tiếp tới dự án.

### Nội dung workshop

**5.1:** [Tổng quan workshop](5.1-workshop-overview/)

**5.2:** [Điều kiện chuẩn bị](5.2-prerequiste/)

**5.3:** [Thiết kế luồng upload bảo mật với Amazon S3](5.3-s3-vpc/)

**5.4:** [Tích hợp API, metadata và vai trò người dùng](5.4-s3-onprem/)

**5.5:** [Bảo mật, vận hành và định hướng mở rộng AWS](5.5-policy/)

**5.6:** [Dọn dẹp tài nguyên và kiểm soát chi phí](5.6-cleanup/)

### Giá trị học được

Thông qua workshop này, tôi không chỉ hiểu rõ hơn một kỹ thuật cụ thể, mà còn hiểu cách một quyết định kiến trúc có thể ảnh hưởng tới trải nghiệm người dùng, hiệu năng backend và khả năng vận hành hệ thống trong tương lai. Đây cũng là một trong những phần giúp tôi nhìn rõ nhất mối liên hệ giữa vai trò frontend của mình với phần backend/AWS mà nhóm đang xây dựng.
