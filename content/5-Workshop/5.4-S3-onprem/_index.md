---
title: "API integration, metadata, and user roles"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---
### Backend integration

The backend needs at least these APIs:

- `POST /api/documents/presign-upload`
- `POST /api/documents`
- `POST /api/documents/:id/presign-download`

These three APIs are enough to support upload, metadata persistence, and document download or preview.

### Real code snippets from CloudDoc

To show that this workshop matches the actual project codebase, the two snippets below are taken directly from `clouddoc`.

**Snippet 1 - Frontend requests a presigned upload URL and sends the file directly to S3**

Source: `frontend/src/context/AppContext.jsx`

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

This snippet reflects the exact workflow described in the workshop: the frontend requests a `presigned URL`, uploads the file to S3 with `PUT`, and only then stores metadata through the backend API.

**Snippet 2 - Express backend generates the presigned upload URL**

Source: `backend/src/documents.routes.js`

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

On the backend side, this API validates the input, generates a safe `S3 key`, creates a short-lived upload URL, and returns the exact data the frontend needs.

### Metadata to store

- Document title
- School, department, and subject
- Uploader
- Approval status
- S3 key or S3 URL
- Download count, created date, and updated date

### User roles

- **Guest:** can only search and view approved documents.
- **Student:** can upload documents and track their own contributions.
- **Administrator:** can approve, reject, and monitor documents in the admin dashboard.

### Why this section matters

If the system only uploads files successfully but has no metadata model and no clear role model, it is still not truly usable. Users will struggle to find documents, administrators will not control content properly, and the backend will not have enough information to support real workflows. That is why APIs and metadata form the bridge between technical storage and product value.
