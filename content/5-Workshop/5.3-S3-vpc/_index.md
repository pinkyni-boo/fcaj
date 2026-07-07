---
title: "Designing a secure Amazon S3 upload flow"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---
### Proposed flow

1. The user selects a file and enters metadata in CloudDoc.
2. The frontend requests a presigned upload URL from the backend.
3. The backend returns a short-lived URL and S3 key.
4. The frontend uploads the file directly to S3.
5. The frontend then sends metadata to the backend for persistence.

### Why presigned URLs

- They reduce backend load.
- They improve security through time-limited access.
- They scale better as file volume increases.

### Important considerations

- Validate file size and type.
- Use structured S3 keys.
- Avoid storing metadata if the real upload failed.

### Architectural value

This pattern clearly separates storage from business logic and is one of the strongest cloud-aligned decisions in the CloudDoc design.
