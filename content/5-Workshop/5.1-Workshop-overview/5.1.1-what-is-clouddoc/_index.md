---
title: "What is CloudDoc?"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1.1. </b> "
---


#### Definition

CloudDoc is a student document sharing system where a document is not published immediately after upload. Instead, it moves through storage, metadata persistence, moderation, and state synchronization before it becomes visible to end users. This model fits user-generated learning platforms because it improves content quality control and makes the document collection manageable.

#### Problem statement

The project needs to solve several concerns at the same time:

- users should be able to upload documents easily from the web interface,
- the backend should not become a bottleneck for large file transfers,
- metadata must be stored in a structured form for search and moderation,
- document state must be tracked across the full lifecycle,
- and AWS resources must be observable and cleanly removable after validation.

#### Why this workflow matters

An upload-only feature would solve only the first step of the problem. The real value of CloudDoc comes from turning a newly uploaded file into a managed, reviewable, searchable, and distributable document. For that reason, this workshop goes beyond S3 upload and includes moderation, visible state updates, preview, download, and monitoring.

#### Document lifecycle

1. `pending`: the document has been uploaded and is waiting for review.
2. `approved`: the administrator has approved the document.
3. `available`: the document can be shown in search, preview, and download features.
