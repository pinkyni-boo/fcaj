---
title: "Workshop overview"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---
### Goal

This workshop explains the CloudDoc document flow from both a technical and practical perspective. The goal is not only to upload files to the cloud, but also to keep the user experience smooth, the backend light, and the architecture extensible.

### Problem

CloudDoc must satisfy three requirements at the same time:

- Users need a simple upload experience.
- The system should avoid routing large files through the backend.
- Metadata must remain structured for search, preview, and moderation.

### Why upload design matters

In small applications, file upload is often implemented in the simplest possible way. But for a document platform, that choice directly affects performance, maintainability, and architectural quality. That is why this workshop focuses on upload flow as a system-design decision, not just a coding task.

### Approach

The most suitable approach is for the backend to generate a **presigned URL**, then let the frontend upload directly to **Amazon S3**. After the upload succeeds, the frontend submits metadata to the backend and stores it in **PostgreSQL**.
