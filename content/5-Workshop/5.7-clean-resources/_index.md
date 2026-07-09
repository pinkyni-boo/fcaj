---
title: "Clean resources"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---


#### Objective

After the workshop is validated, temporary resources should be removed to avoid unnecessary AWS cost and to show responsible operational practice. In AWS projects, clean-up is an important part of the resource lifecycle rather than an optional afterthought.

#### Clean-up steps

**Step 1:** Remove test data from the **S3 bucket** after preserving the screenshots needed for the report.

<img src="/images/5-Workshop/AWS-Console/cleanup-s3-bucket.png" alt="S3 bucket cleanup result" style="max-width: 90%; height: auto;">

**Step 2:** Stop or terminate the **EC2 instance** if the environment is only for demonstration purposes to avoid ongoing charges.

<img src="/images/5-Workshop/AWS-Console/cleanup-ec2.png" alt="EC2 termination during backend cleanup" style="max-width: 90%; height: auto;">

**Step 3:** Review observability resources such as log groups or alarms and decide whether to keep or remove them.

**Step 4:** Check resource dependencies before deletion to avoid leaving unused components behind.
