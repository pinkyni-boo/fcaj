---
title: "Triển khai luồng upload và lưu trữ tài liệu"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---


#### Mục tiêu

Phần này mô tả bước triển khai quan trọng nhất của workshop: đưa một tài liệu từ giao diện web vào hệ thống CloudDoc bằng cách sử dụng presigned URL và Amazon S3. Đây là đoạn nối giữa trải nghiệm người dùng ở frontend và logic nghiệp vụ ở backend, đồng thời cũng là bằng chứng rõ nhất cho việc dự án đã được triển khai end-to-end chứ không chỉ dừng ở mockup giao diện.

#### Thành phần chính

- Form upload trên frontend.
- API tạo presigned upload URL.
- Bucket S3 dành cho file tài liệu.
- Cơ chế lưu metadata vào cơ sở dữ liệu.

#### Luồng xử lý tiêu biểu

Trong kiến trúc này, backend không nhận trực tiếp toàn bộ file binary. Thay vào đó, backend xác thực yêu cầu, sinh khóa lưu trữ và presigned URL, sau đó frontend mới gửi file trực tiếp lên S3. Cách làm này giúp giảm tải cho server, đơn giản hóa đường truyền file và phù hợp hơn với yêu cầu mở rộng của một nền tảng lưu trữ tài liệu.

#### Code snippet

```jsx
const upload = await presignUpload({
  fileName: file.name,
  fileType,
  contentType: file.type || "application/octet-stream",
  fileSizeBytes: file.size,
})

await uploadFileToS3(upload.uploadUrl, file)
```

```js
documentsRouter.post("/presign-upload", async (req, res) => {
  const input = presignUploadSchema.parse(req.body)
  const key = createDocumentKey(input)
  const uploadUrl = await createPresignedUploadUrl({ key, contentType: input.contentType })
  res.status(201).json({ data: { key, uploadUrl, method: "PUT" } })
})
```

#### Các bước thực hiện luồng upload

**Bước 1:** Người dùng truy cập trang chủ, điền thông tin và chọn file cần upload trên form giao diện.

<img src="/images/5-Workshop/AWS-Console/frontend-upload-form.png" alt="Biểu mẫu upload tài liệu trên giao diện CloudDoc" style="max-width: 90%; height: auto;">

**Bước 2:** Hệ thống tiến hành lấy presigned URL từ backend và tải trực tiếp file từ trình duyệt lên S3.

<img src="/images/5-Workshop/AWS-Console/frontend-upload-progress.png" alt="Trạng thái đang upload file từ trình duyệt lên S3" style="max-width: 90%; height: auto;">

**Bước 3:** Sau khi upload S3 và lưu metadata thành công, hệ thống hiển thị thông báo thành công cho người dùng.

<img src="/images/5-Workshop/AWS-Console/frontend-upload-success.png" alt="Thông báo upload thành công sau khi hệ thống hoàn tất bước gửi file" style="max-width: 90%; height: auto;">

#### Các bước thực hiện

1. [Khởi tạo luồng upload](5.3.1-build-upload-interaction/)
2. [Kiểm tra lưu trữ và đồng bộ dữ liệu](5.3.2-connect-form-to-backend/)
