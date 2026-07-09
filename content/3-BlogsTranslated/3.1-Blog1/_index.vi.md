---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

<img src="/images/3-BlogsTranslated/blog1-doc-image.png" alt="Minh họa Blog 1" style="max-width: 90%; height: auto;">

Blog đầu tiên tôi chọn dịch xoay quanh bài toán rất thực tế: làm sao để ứng dụng web hoặc mobile vẫn mang lại trải nghiệm mượt mà khi kết nối mạng chập chờn hoặc tạm thời bị mất. Thay vì chờ server phản hồi rồi mới cập nhật giao diện, kiến trúc offline-first kết hợp với optimistic UI cho phép người dùng thấy kết quả gần như ngay lập tức, sau đó hệ thống mới đồng bộ dữ liệu ở phía sau.

Bài viết từ AWS giới thiệu cách kết hợp **AWS Amplify Gen 2**, **AWS AppSync**, **TanStack Query** và **MongoDB Atlas** để xây dựng mô hình này. Đây là một hướng tiếp cận đáng chú ý vì nó giải quyết đồng thời cả hai mục tiêu: nâng cao trải nghiệm người dùng và giữ được khả năng đồng bộ dữ liệu khi mạng được khôi phục.

### 1. Tổng quan giải pháp

Kiến trúc được mô tả trong bài sử dụng:

- **AWS Amplify Gen 2** để xây dựng và triển khai ứng dụng full-stack nhanh hơn.
- **AWS AppSync** để cung cấp GraphQL API phục vụ đồng bộ dữ liệu.
- **TanStack Query** để quản lý cache phía client, optimistic updates và rollback khi cần.
- **MongoDB Atlas** làm cơ sở dữ liệu backend.
- Bên cạnh đó còn có **AWS Lambda** cho xử lý serverless và **Amazon Cognito** cho xác thực người dùng.

Điểm đáng chú ý là phần client không còn đóng vai trò chỉ hiển thị dữ liệu thụ động, mà chủ động quản lý trạng thái và đưa ra phản hồi sớm hơn cho người dùng.

### 2. Optimistic UI hoạt động như thế nào?

Thay vì chờ phản hồi từ server rồi mới cập nhật giao diện, optimistic UI cho phép ứng dụng hiển thị kết quả dự kiến ngay sau khi người dùng thao tác. Ví dụ trong ứng dụng to-do:

- Người dùng tạo một công việc mới.
- Giao diện hiển thị công việc đó ngay lập tức trong danh sách.
- Request được gửi đến AppSync để lưu dữ liệu thật.
- Nếu request thành công, dữ liệu được đồng bộ như bình thường.
- Nếu request thất bại hoặc mất kết nối, trạng thái cũ được khôi phục thông qua cơ chế rollback.

Cách tiếp cận này giúp giảm cảm giác chờ đợi và làm cho ứng dụng phản hồi tự nhiên hơn, đặc biệt trong bối cảnh mạng yếu hoặc không ổn định.

### 3. Luồng xử lý chính

Từ nội dung bài viết, tôi tóm tắt luồng hoạt động như sau:

1. Người dùng thực hiện thao tác tạo hoặc cập nhật dữ liệu.
2. TanStack Query cập nhật cache cục bộ và phản ánh thay đổi ngay trên giao diện.
3. Request GraphQL được gửi tới AWS AppSync.
4. AppSync xử lý và lưu dữ liệu xuống MongoDB Atlas.
5. Nếu xảy ra lỗi, cache được phục hồi về trạng thái trước đó.

Trong ví dụ của AWS, cơ chế xử lý xung đột được triển khai theo hướng **First-Come, First-Served**, giúp đơn giản hóa việc giải quyết các cập nhật cạnh tranh.

### 4. Điều tôi học được từ bài blog

Bài viết này làm tôi chú ý hơn tới việc trải nghiệm người dùng không chỉ đến từ giao diện đẹp, mà còn đến từ cách dữ liệu được phản hồi. Với vai trò làm frontend cho CloudDoc, tôi thấy tư duy offline-first và optimistic UI rất hữu ích trong các màn hình như:

- Upload tài liệu.
- Chỉnh sửa metadata.
- Lưu trạng thái kiểm duyệt.
- Cập nhật thông tin hồ sơ người dùng.

Ngay cả khi CloudDoc chưa triển khai offline-first đầy đủ, việc hiểu mô hình này giúp tôi thiết kế luồng giao diện hợp lý hơn, nhất là ở những thao tác cần phản hồi nhanh.

### 5. Liên hệ với CloudDoc

- CloudDoc có thể học từ mô hình optimistic UI để cải thiện cảm giác phản hồi ở các form upload hoặc cập nhật dữ liệu.
- Nếu sau này hệ thống có thêm tính năng làm việc tạm khi mạng yếu, tư duy offline-first sẽ rất đáng tham khảo.
- Việc dùng AppSync và lớp đồng bộ dữ liệu cũng gợi ra cách tổ chức client state rõ ràng hơn cho các ứng dụng có nhiều trạng thái động.

### 6. Kết luận

Offline-first và optimistic UI đang trở thành những kỹ thuật quan trọng để cải thiện trải nghiệm người dùng trong các ứng dụng hiện đại. Với Amplify, AppSync và TanStack Query, việc triển khai các tính năng này trở nên dễ tiếp cận hơn mà vẫn giữ được khả năng đồng bộ dữ liệu khi mạng được khôi phục.

**Link bài đăng trong nhóm FCAJ:** https://www.facebook.com/groups/awsstudygroupfcj/permalink/2190116435086650/
