---
title: "Cập nhật dữ liệu"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---


#### Mục tiêu

Sau khi tài liệu được duyệt, dữ liệu không chỉ đổi ở một nơi duy nhất mà phải được đồng bộ giữa backend, cơ sở dữ liệu và giao diện hiển thị. Mục này giải thích vì sao bước cập nhật dữ liệu là cần thiết trong một hệ thống có nhiều màn hình, nhiều trạng thái và có quy trình moderation như CloudDoc.

#### Các bước cập nhật

**Bước 1:** Đổi trạng thái tài liệu từ `pending` sang `approved`.

**Bước 2:** Đồng bộ dữ liệu ở dashboard quản trị để cập nhật trạng thái hiển thị.

**Bước 3:** Truy cập trang tìm kiếm và đảm bảo dữ liệu mới nhất đã được đồng bộ, hiển thị đúng kết quả tài liệu vừa được duyệt.

<img src="/images/5-Workshop/AWS-Console/search-result.png" alt="Kết quả tìm kiếm đã hiển thị tài liệu sau khi được phê duyệt" style="max-width: 90%; height: auto;">

**Bước 4:** Cho phép preview và download với tài liệu đã duyệt để người dùng có thể thao tác bình thường.

#### Kết quả mong đợi

Tài liệu được hiển thị nhất quán trên mọi màn hình và phản ánh đúng dữ liệu hiện có trong hệ thống, từ trạng thái moderation cho đến quyền xem trước và tải xuống.
