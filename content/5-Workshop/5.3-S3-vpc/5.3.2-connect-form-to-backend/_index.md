---
title: "Validate object storage and metadata sync"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---


#### Objective

After the upload completes, this step verifies that both the physical object and the business metadata have been recorded correctly. If the file exists in S3 but the metadata is missing, the document cannot move into moderation and search.

#### Storage Verification Steps

After the upload completes, verify the following:

**Step 1:** Check if the **File has appeared in the S3 bucket**. A new object confirms the presigned URL upload flow was successful.

<img src="/images/5-Workshop/AWS-Console/s3-object-created.png" alt="Uploaded object visible in S3" style="max-width: 90%; height: auto;">

**Step 2:** Ensure the **Metadata has been written to the database**.

**Step 3:** Confirm the **Document is visible in the moderation area** for admins.

**Step 4:** The initial state of the document should be set to `pending`.
