---
title: "Introduction"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---


#### Objective

This section introduces the workshop scope and the problem that CloudDoc is solving. Before moving into implementation steps, the reader needs a clear view of the document lifecycle, the reason the project separates frontend, backend, storage, and database responsibilities, and the AWS services that support the full workflow.

#### Problem context

In practice, a learning document platform needs more than a successful file upload. It must track document state, support moderation before publication, and provide stable access for end users. If every file passed through the application server, the system would consume more compute resources and become harder to scale cost-effectively. For that reason, CloudDoc uses a flow where the frontend requests upload instructions from the backend and then sends the file directly to Amazon S3.

#### Workshop flow

1. A user fills in document metadata and selects a file in the web interface.
2. The backend validates the request and generates a presigned upload URL.
3. The browser uploads the file directly to S3.
4. Metadata is stored in the database with an initial `pending` state.
5. An administrator reviews and approves the document.
6. The approved document appears in search, preview, and download features.

#### Subsections

1. [What is CloudDoc?](5.1.1-what-is-clouddoc/)
2. [Services](5.1.2-services-used/)
3. [Architecture](5.1.3-architecture/)
