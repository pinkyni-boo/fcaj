---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

This workshop is rewritten to match the **CloudDoc** project instead of keeping unrelated AWS lab material. Its main focus is a **secure document upload workflow on AWS**, where the frontend uploads files directly to Amazon S3 through presigned URLs while the backend manages metadata, access control, and related business logic.

I chose this topic because it clearly connects frontend, backend, and cloud architecture in one practical flow. In CloudDoc, changing the upload design changes the whole system direction: backend load is reduced, metadata becomes easier to manage, and the cloud architecture is used more effectively.

### Workshop goals

- Describe a practical upload workflow suitable for a document-management system.
- Explain why presigned URLs are a strong fit for CloudDoc.
- Show the relationship between the frontend upload form, backend APIs, and S3 storage.
- Clarify security, metadata, access control, and scalability considerations.

### Why this topic fits CloudDoc

CloudDoc handles learning documents, which means:

- File volume can grow significantly.
- Upload flow must be simple and reliable for users.
- Metadata must remain structured for search and moderation.
- The architecture should stay extensible for future background processing tasks.

That makes a presigned-URL and S3-focused workshop much more relevant than unrelated AWS lab steps.

### Workshop content

**5.1:** [Workshop overview](5.1-workshop-overview/)

**5.2:** [Prerequisites](5.2-prerequiste/)

**5.3:** [Designing a secure Amazon S3 upload flow](5.3-s3-vpc/)

**5.4:** [Integrating APIs, metadata, and user roles](5.4-s3-onprem/)

**5.5:** [Security, operations, and AWS expansion path](5.5-policy/)

**5.6:** [Cleanup and cost control](5.6-cleanup/)

### Learning value

This workshop helped me understand not just one technical trick, but how an architectural decision can influence user experience, backend performance, and future system operations. It also made the connection between my frontend role and the backend/AWS direction of the team much clearer.
