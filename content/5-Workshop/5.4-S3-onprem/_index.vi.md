---
title: "Tích hợp API, metadata và vai trò người dùng"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---
### Tích hợp backend

Phía backend cần tối thiểu các API sau:

- `POST /api/documents/presign-upload`
- `POST /api/documents`
- `POST /api/documents/:id/presign-download`

Ba API này đủ để tạo thành luồng upload, lưu metadata và tải hoặc xem tài liệu.

### Code snippet thật từ CloudDoc

Để chứng minh workshop bám sát codebase đang làm, dưới đây là hai đoạn code thật lấy trực tiếp từ dự án `clouddoc`.

**Snippet 1 - Frontend xin presigned URL và tải file trực tiếp lên S3**

Nguồn: `frontend/src/context/AppContext.jsx`

```jsx
const addDocument = async (doc, file) => {
  if (!file) {
    throw new Error("File is required when API mode is enabled")
  }

  const fileType = doc.fileType || file.name.split(".").pop()
  const upload = await presignUpload({
    fileName: file.name,
    fileType,
    contentType: file.type || "application/octet-stream",
    fileSizeBytes: file.size,
  })

  await uploadFileToS3(upload.uploadUrl, file)

  const created = await createDocument({
    title: doc.title,
    school: doc.school,
    department: doc.department,
    subject: doc.subject,
    fileType,
    fileSizeBytes: file.size,
    s3Key: upload.key,
    uploaderName: doc.uploader,
    contentIndex: doc.contentIndex,
  })

  setDocuments(prev => [created, ...prev])
  return created
}
```

Đoạn code này thể hiện đúng luồng workshop đã mô tả: frontend không đẩy file xuyên qua backend, mà xin `presigned URL`, `PUT` file lên S3, rồi mới lưu metadata vào PostgreSQL thông qua API tạo document.

**Snippet 2 - Backend Express sinh presigned URL**

Nguồn: `backend/src/documents.routes.js`

```js
documentsRouter.post("/presign-upload", async (req, res) => {
  const input = presignUploadSchema.parse(req.body)
  const key = createDocumentKey(input)
  const uploadUrl = await createPresignedUploadUrl({
    key,
    contentType: input.contentType,
  })

  res.status(201).json({
    data: {
      key,
      uploadUrl,
      method: "PUT",
      expiresIn: Number(process.env.S3_PRESIGN_EXPIRES_SECONDS || 300),
    },
  })
})
```

Ở phía backend, API này chịu trách nhiệm kiểm tra input, sinh `S3 key` an toàn, tạo URL có thời hạn ngắn và trả về đúng thông tin mà frontend cần để upload trực tiếp lên S3.

### Metadata cần lưu

- Tiêu đề tài liệu
- Trường, ngành, môn học
- Người đăng
- Trạng thái duyệt
- S3 key hoặc S3 URL
- Số lượt tải, ngày tạo và ngày cập nhật

### Vai trò người dùng

- **Khách:** chỉ tra cứu và xem các tài liệu đã được duyệt.
- **Sinh viên:** có thể tải lên tài liệu và theo dõi nội dung đã đóng góp.
- **Quản trị viên:** duyệt, từ chối hoặc theo dõi tài liệu trong dashboard quản trị.

### Tại sao phần này quan trọng

Nếu chỉ upload file thành công mà không có metadata và role model rõ ràng, hệ thống vẫn chưa thực sự usable. Người dùng sẽ không tìm thấy tài liệu đúng cách, quản trị viên không kiểm soát được nội dung và backend không đủ thông tin để triển khai các nghiệp vụ cần thiết. Vì vậy, API và metadata chính là cầu nối giữa lưu trữ kỹ thuật và giá trị sản phẩm thực tế.
