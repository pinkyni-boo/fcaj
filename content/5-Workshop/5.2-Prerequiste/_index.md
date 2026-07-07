---
title: "Prerequisites"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---
### Required components

- A React frontend with an upload form and metadata fields.
- An Express backend with a presigned URL API and a metadata creation API.
- PostgreSQL for document-related structured data.
- A dedicated S3 bucket for uploaded documents.

### Technical setup

- Environment variables for S3, database access, and presigned URL expiration.
- Correct CORS configuration on S3.
- Limited IAM permissions for the backend.

### Test readiness

Before end-to-end testing, verify:

- The frontend can call the backend API.
- The backend can generate a valid upload URL.
- S3 receives the uploaded file.
- Metadata is stored correctly after upload.

### Why this preparation matters

Upload workflows often fail not because of UI logic, but because of small configuration issues such as CORS, IAM scope, or missing environment settings. That makes preparation a critical part of the design.
