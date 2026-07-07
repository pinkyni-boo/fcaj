---
title: "Sự kiện 1: AWS Vietnam Community Day tháng 5 - AI, CloudFront và Multi-Agent Systems"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

### Thông tin sự kiện

| Mục | Nội dung |
| --- | --- |
| Tên sự kiện | AWS Vietnam Community Day tháng 5/2026 trong khuôn khổ học tập và chia sẻ công nghệ của FCAJ |
| Thời gian | **23/05/2026** |
| Địa điểm | **Tòa Bitexco, văn phòng AWS, TP. Hồ Chí Minh** |
| Vai trò tham gia | Người tham dự, ghi chú nội dung, tổng hợp kiến thức và liên hệ với dự án CloudDoc |
| Hình thức tham gia | Tham gia chuỗi chia sẻ kỹ thuật và tổng hợp lại các ý chính từ phần trình bày của diễn giả |

### Nội dung chính của buổi sự kiện

Event 1 là một buổi Community Day có lượng kiến thức khá dày và mang màu sắc rất “enterprise”. Nội dung xuyên suốt của buổi chia sẻ tập trung vào cách các doanh nghiệp đang tiếp cận AI, tổ chức kiến trúc hệ thống hiện đại và kiểm soát chất lượng đầu ra khi đưa các công nghệ mới vào môi trường thực tế. Thay vì chỉ nói riêng từng công cụ, diễn giả liên tục đặt công nghệ vào bối cảnh vận hành thật: dữ liệu phải đủ tốt thì AI mới hữu ích, kiến trúc phải đủ rõ thì hệ thống mới dễ mở rộng, và những quyết định về hạ tầng luôn phải đi cùng câu chuyện chi phí, giám sát và độ tin cậy.

Một điểm tôi thấy nổi bật trong sự kiện là cách diễn giả nói về AI theo hướng rất thực tế. AI không được xem như một lớp “thông minh” tự hoạt động tốt nếu thiếu dữ liệu đầu vào, mà phải được nuôi bằng đúng context, đúng constraints và đúng mục tiêu. Từ đó, buổi chia sẻ mở rộng sang tư duy tổ chức hệ thống multi-agent, giải thích vì sao với các bài toán phức tạp và nhiều chiều, việc chia vai trò cho từng thành phần phân tích sẽ hợp lý hơn một mô hình agent đơn lẻ.

Bên cạnh câu chuyện AI, sự kiện cũng nói khá sâu về lớp phân phối nội dung và vận hành hệ thống web, đặc biệt là vai trò của CloudFront. Điều tôi ghi nhận không chỉ là lợi ích về tốc độ, mà còn là cách CloudFront ảnh hưởng tới bảo mật, khả năng chịu tải và tính dễ dự báo của chi phí. Phần này giúp tôi nhìn rõ hơn rằng frontend không chỉ là giao diện người dùng, mà còn gắn trực tiếp với câu chuyện delivery architecture ở phía sau.

Ngoài ra, một nội dung rất đáng nhớ khác của buổi này là góc nhìn về độ ổn định của LLM. Diễn giả nhấn mạnh rằng ngay cả khi dùng các thiết lập tưởng như “deterministic”, đầu ra của mô hình vẫn có thể thay đổi bởi nhiều yếu tố ở tầng hạ tầng và tính toán. Điều đó giúp tôi hiểu rằng khi đưa AI vào sản phẩm hoặc workflow thật, không thể chỉ tin vào prompt hay model, mà còn phải thiết kế thêm validation, guardrails và cơ chế quan sát.

### Điều tôi học được sau sự kiện

Sau khi tham gia Event 1, tôi rút ra ba lớp bài học rõ ràng. Thứ nhất, với AI và dữ liệu, vấn đề quan trọng nhất không phải là “dùng model nào”, mà là mình đã chuẩn bị context đủ tốt hay chưa. Thứ hai, với kiến trúc hệ thống, càng thiết kế rõ vai trò từng lớp thì càng dễ mở rộng và dễ kiểm soát khi quy mô tăng lên. Thứ ba, với vận hành thực tế, hiệu năng, chi phí và observability luôn phải được nghĩ cùng lúc, không thể tách riêng.

Những điều này tác động khá trực tiếp tới cách tôi nhìn dự án CloudDoc. Trước đây tôi thường tập trung nhiều hơn vào luồng giao diện và cảm giác sử dụng, nhưng sau sự kiện này tôi để ý nhiều hơn tới metadata, delivery layer, monitoring và khả năng mở rộng về sau. Tôi nhận ra rằng nếu CloudDoc muốn phát triển thêm các tính năng thông minh trong tương lai, thì nền tảng dữ liệu và kiến trúc hiện tại phải đủ sạch và đủ rõ ngay từ đầu.

### Liên hệ với CloudDoc

Sự kiện này giúp tôi liên hệ CloudDoc ở ba điểm rất rõ. Thứ nhất, metadata tài liệu của CloudDoc không chỉ phục vụ tìm kiếm hiện tại mà còn có thể trở thành nền tảng cho các tính năng AI sau này. Thứ hai, phần chia sẻ về CloudFront củng cố thêm quyết định triển khai frontend theo hướng tĩnh qua S3 và CDN thay vì để backend gánh phần phân phối nội dung. Thứ ba, góc nhìn về độ ổn định của AI và kiến trúc multi-agent nhắc tôi rằng bất kỳ lớp xử lý thông minh nào về sau cũng cần đi kèm giám sát, kiểm soát và khả năng giải thích.

### Đánh giá cá nhân

Điều tôi đánh giá cao nhất ở Event 1 là buổi này không dừng ở việc cập nhật công nghệ mới, mà giúp tôi nối được nhiều mảng kiến thức vốn hay bị học rời rạc. AI, dữ liệu, kiến trúc, cost và vận hành đều được đặt trong cùng một bức tranh. Vì vậy, đây không chỉ là một buổi nghe chia sẻ, mà thực sự là một sự kiện giúp tôi thay đổi cách nhìn CloudDoc từ một sản phẩm giao diện thành một hệ thống cần được thiết kế bài bản hơn ở phía sau.
