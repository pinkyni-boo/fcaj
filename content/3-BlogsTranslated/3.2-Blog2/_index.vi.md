---
title: "Blog 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

<img src="/images/3-BlogsTranslated/blog2-doc-image.png" alt="Minh họa Blog 2" style="max-width: 90%; height: auto;">

Blog thứ hai tôi chọn dịch nói về một nhu cầu đang ngày càng phổ biến trong doanh nghiệp: làm sao để người dùng có thể hỏi đáp bằng ngôn ngữ tự nhiên trên chính kho tài liệu nội bộ của tổ chức, thay vì phải tự đi tìm từng file hoặc từng thư mục. AWS giới thiệu một cách tiếp cận sử dụng **Amazon Q Business**, **AWS Amplify Gen 2** và **AWS CDK** để xây dựng mô hình này khá nhanh mà vẫn có kiểm soát quyền truy cập.

Đây là bài viết khiến tôi quan tâm nhiều vì nó liên quan trực tiếp đến bài toán khai thác tri thức từ tài liệu, vốn cũng là một hướng phát triển tiềm năng cho CloudDoc nếu hệ thống được mở rộng sau này.

### 1. Tổng quan giải pháp

Kiến trúc trong bài sử dụng:

- **Amazon Q Business** để cung cấp khả năng hỏi đáp dựa trên dữ liệu nội bộ.
- **AWS Amplify Gen 2** để xây dựng và triển khai ứng dụng web.
- **AWS CDK** để quản lý hạ tầng dưới dạng mã nguồn.
- **Amazon Cognito** và **IAM Identity Center** để xác thực và phân quyền.
- **Amazon S3** để lưu trữ tài liệu phục vụ quá trình lập chỉ mục dữ liệu.

Điểm tôi thấy đáng chú ý là mô hình này không yêu cầu phải tự xây dựng toàn bộ nền tảng AI từ đầu. Thay vào đó, doanh nghiệp có thể tận dụng các dịch vụ được AWS cung cấp sẵn và tập trung hơn vào luồng sử dụng thực tế.

### 2. Kiến trúc hoạt động

Luồng chính của hệ thống được mô tả như sau:

1. Người dùng đăng nhập vào ứng dụng thông qua Cognito.
2. Tài liệu nội bộ được lưu trên Amazon S3.
3. Amazon Q Business được cấp quyền truy cập và lập chỉ mục dữ liệu từ S3.
4. Giao diện chat được nhúng trực tiếp vào ứng dụng web.
5. Người dùng đặt câu hỏi và nhận câu trả lời dựa trên dữ liệu doanh nghiệp, kèm nguồn tham chiếu.

Từ góc nhìn sản phẩm, điều này rất quan trọng vì nó biến kho tài liệu tĩnh thành một hệ thống có thể hỗ trợ tra cứu chủ động hơn.

### 3. Điểm nổi bật của bài blog

Có ba điểm tôi ghi nhận rõ nhất:

- **Hạ tầng được quản lý bằng AWS CDK:** giảm cấu hình thủ công và giúp tái sử dụng tốt hơn giữa các môi trường.
- **AI được gắn với dữ liệu nội bộ thật:** thay vì chỉ là chatbot chung chung, hệ thống trả lời dựa trên tài liệu doanh nghiệp đã được lập chỉ mục.
- **Quyền truy cập được kiểm soát:** vì bài toán dữ liệu nội bộ luôn gắn với bảo mật, nên việc đi cùng Cognito và IAM Identity Center là rất cần thiết.

### 4. Điều tôi học được từ bài blog

Sau khi dịch bài này, tôi nhận ra rằng giá trị của AI trong ứng dụng không chỉ nằm ở phần sinh câu trả lời, mà còn nằm ở phần tổ chức dữ liệu đủ tốt để AI có thể trả lời đúng ngữ cảnh. Điều này liên hệ rất mạnh tới CloudDoc, vì nếu metadata tài liệu không chuẩn, cấu trúc lưu trữ không rõ ràng và quyền truy cập không được quản lý tốt, thì một tính năng AI về sau cũng khó hoạt động hiệu quả.

### 5. Liên hệ với CloudDoc

- Nếu CloudDoc phát triển thêm trong tương lai, Amazon Q Business hoặc một mô hình hỏi đáp tương tự có thể trở thành hướng mở rộng phù hợp.
- Metadata tài liệu và cấu trúc phân loại trong CloudDoc chính là nền tảng để các chức năng AI có thể hoạt động tốt.
- Việc kết hợp giao diện ứng dụng với tri thức nội bộ là hướng rất đáng tham khảo cho bài toán tra cứu học liệu thông minh.

### 6. Kết luận

Việc tích hợp trợ lý AI vào các ứng dụng nội bộ đang trở thành nhu cầu phổ biến ở nhiều tổ chức. Kiến trúc sử dụng Amazon Q Business, Amplify và CDK là một cách tiếp cận đáng tham khảo cho các hệ thống cần khai thác tri thức từ tài liệu một cách an toàn, có kiểm soát và có khả năng mở rộng.

**Link bài đăng trong nhóm FCAJ:** https://www.facebook.com/share/p/1BkgmtmwUw/
