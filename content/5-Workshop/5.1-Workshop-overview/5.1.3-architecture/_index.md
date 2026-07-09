---
title: "Architecture"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.1.3. </b> "
---


#### Objective

This section makes the workshop architecture explicit inside the workshop itself so the reader can understand how each implementation step maps to the AWS design.

#### Reference architecture

The diagram below summarizes the CloudDoc deployment direction used throughout this workshop:

<img src="/images/2-Proposal/aws-drawio-cloudoc.png" alt="CloudDoc AWS Architecture" style="max-width: 90%; height: auto;">

#### Layered explanation

1. **CloudFront and S3 static hosting** deliver the frontend efficiently to end users.
2. **EC2** runs the backend API that validates requests, generates presigned URLs, and coordinates document state.
3. **RDS PostgreSQL** stores metadata, moderation state, and searchable document information.
4. **S3 object storage** keeps uploaded files outside the application server so file transfer can scale more safely.
5. **CloudWatch** provides logs, metrics, and alarms for operational visibility.

#### Why this architecture matters for the workshop

Each workshop section corresponds to one part of this design:

1. The prerequisite section verifies that CloudFront, S3, EC2, and RDS are ready.
2. The upload section proves that the browser can send files directly to S3 through a backend-generated presigned URL.
3. The validation and moderation sections confirm that metadata and document state stay synchronized.
4. The observability and cleanup sections show that the environment is monitored and can be cleaned up responsibly.

By placing the architecture here, the workshop shows not only isolated AWS screenshots but also the full system relationship behind the implementation flow.
