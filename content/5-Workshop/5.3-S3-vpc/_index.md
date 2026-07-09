---
title: "Implement upload and storage flow"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---


#### Objective

This section covers the most important implementation step in the workshop: moving a document from the web interface into CloudDoc by using a presigned upload flow and Amazon S3. It connects the user-facing upload experience with backend business logic and serves as the clearest proof that the project is implemented end-to-end rather than described only at a conceptual level.

#### Core components

- the upload form in the frontend,
- the API that creates presigned upload URLs,
- the S3 bucket that stores document objects,
- and the metadata persistence layer in the database.

#### Representative code

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

#### Upload execution steps

**Step 1:** The user fills in the form and selects a file to upload via the CloudDoc interface.

<img src="/images/5-Workshop/AWS-Console/frontend-upload-form.png" alt="Upload form in CloudDoc" style="max-width: 90%; height: auto;">

**Step 2:** The application retrieves a presigned URL and uploads the file directly from the browser to Amazon S3.

<img src="/images/5-Workshop/AWS-Console/frontend-upload-progress.png" alt="Upload in progress from browser to S3" style="max-width: 90%; height: auto;">

**Step 3:** A success notification is shown once the file upload to S3 and metadata save are completed.

<img src="/images/5-Workshop/AWS-Console/frontend-upload-success.png" alt="Successful upload notification" style="max-width: 90%; height: auto;">

#### Subsections

1. [Initiate the upload flow](5.3.1-build-upload-interaction/)
2. [Validate object storage and metadata sync](5.3.2-connect-form-to-backend/)
