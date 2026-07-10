---
title: "Phát triển giao diện cốt lõi và dữ liệu mô phỏng cho CloudDoc"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
### Mục tiêu tuần 9:

- Hoàn thiện các màn hình người dùng cốt lõi để CloudDoc có thể demo được luồng tra cứu và đóng góp tài liệu.
- Chuẩn hóa cấu trúc dữ liệu mô phỏng để frontend có thể phát triển độc lập khi backend AWS chưa hoàn tất.
- Làm rõ logic hiển thị giữa danh sách tài liệu, chi tiết tài liệu và bộ lọc theo trường, ngành, môn học.

### Các công việc triển khai trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | Rà soát wireframe và tách các khu vực chính của CloudDoc gồm trang chủ, trang tìm kiếm và khu vực upload. | 15/06/2026 | 15/06/2026 |  |
| 2 | Xây dựng bộ mock data cho tài liệu học tập: tiêu đề, môn học, trường, ngành, người đăng, số lượt tải và trạng thái duyệt. | 16/06/2026 | 16/06/2026 |  |
| 3 | Hoàn thiện giao diện trang chủ và danh sách tài liệu nổi bật, kết nối thanh tìm kiếm với route tra cứu. | 17/06/2026 | 17/06/2026 |  |
| 4 | Phát triển trang tìm kiếm với bộ lọc nhiều tầng và hiển thị kết quả theo thẻ tài liệu. | 18/06/2026 | 18/06/2026 |  |
| 5 | Kiểm thử luồng điều hướng giữa Home, Search và Preview để đảm bảo demo xuyên suốt. | 19/06/2026 | 19/06/2026 |  |

### Kết quả đạt được trong tuần 9:

- Hình thành được bộ khung giao diện cốt lõi của CloudDoc để nhóm có thể demo rõ giá trị sản phẩm.
- Chuẩn hóa mock data đủ gần với bài toán thực tế, giúp việc tích hợp API sau này thuận lợi hơn.
- Hoàn thiện được luồng người dùng từ tìm kiếm tài liệu đến xem trước tài liệu ở mức frontend.
