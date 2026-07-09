---
title: "Services"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.1.2. </b> "
---


#### Core services

The CloudDoc workshop uses the following AWS services:

- **Amazon S3** for document files and frontend static assets.
- **Amazon CloudFront** for web distribution.
- **Amazon EC2** for the backend API.
- **Amazon RDS PostgreSQL** for metadata and document state.
- **Amazon CloudWatch** for logs, metrics, and alarms.

#### Role in the architecture

1. S3 separates file storage from the application server.
2. EC2 handles business rules, validation, and presigned URL generation.
3. RDS stores structured data for moderation, search, and state synchronization.
4. CloudFront improves frontend delivery for browser-based access.
5. CloudWatch provides operational visibility and alerting.

#### Security and operations note

The report should explicitly highlight two technical points: the **principle of least privilege** for AWS access and the use of CloudWatch logs, metrics, and alarms to demonstrate that the environment is monitored, not just deployed.
