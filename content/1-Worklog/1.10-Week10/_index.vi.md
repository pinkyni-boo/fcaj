---
title: "Hoàn thiện luồng người dùng, phân quyền và kiểm duyệt tài liệu"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---
### Mục tiêu tuần 10:

- Hoàn thiện các chức năng liên quan đến đăng nhập mô phỏng, phân quyền người dùng và trải nghiệm đóng góp tài liệu.
- Xây dựng luồng kiểm duyệt tài liệu phù hợp với bài toán sinh viên đăng tải và quản trị viên xét duyệt.
- Tạo nền tảng cho dashboard quản trị và các thao tác quản lý tài liệu sau này.

### Các công việc triển khai trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | Thiết kế lại flow đăng nhập nhanh theo vai trò sinh viên và quản trị viên để phục vụ demo hệ thống. | 22/06/2026 | 22/06/2026 |  |
| 2 | Hoàn thiện trang upload tài liệu với metadata bắt buộc, kéo thả tệp và thông báo tiến trình tải lên. | 23/06/2026 | 23/06/2026 |  |
| 3 | Bổ sung logic phân quyền route: khách chỉ xem tài liệu, người dùng đăng nhập mới được đóng góp, admin có khu vực riêng. | 24/06/2026 | 24/06/2026 |  |
| 4 | Xây dựng mô hình trạng thái tài liệu gồm pending, approved và rejected để hỗ trợ quy trình duyệt. | 25/06/2026 | 25/06/2026 |  |
| 5 | Thảo luận với nhóm backend về dữ liệu cần trao đổi giữa frontend và API cho upload, lưu metadata và duyệt tài liệu. | 26/06/2026 | 26/06/2026 |  |

### Kết quả đạt được trong tuần 10:

- Luồng người dùng của CloudDoc trở nên rõ ràng hơn, thể hiện đúng vai trò sinh viên và quản trị viên.
- Màn hình upload và quy trình kiểm duyệt được mô hình hóa đầy đủ để sẵn sàng tích hợp backend.
- Frontend và backend thống nhất tốt hơn về cấu trúc dữ liệu tài liệu, trạng thái duyệt và các endpoint cần thiết.
