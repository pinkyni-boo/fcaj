---
title: "Verify the environment"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.2.1. </b> "
---


#### Objective

This step verifies that the main components are working before document upload begins. The purpose is to make sure any later failure can be traced to workflow logic rather than a missing infrastructure prerequisite.

#### Verification Steps

Before uploading documents, please verify the following infrastructure conditions:

**Step 1:** Ensure the **Frontend** is reachable in the browser and verify the **CloudFront** distribution configuration.

<img src="/images/5-Workshop/AWS-Console/cloudfront-distribution.png" alt="CloudFront distribution for the frontend" style="max-width: 90%; height: auto;">

**Step 2:** Verify that the **S3 buckets** are visible in the AWS Console, and ensure they are ready for storage and access.

<img src="/images/5-Workshop/AWS-Console/frontend-buckets.png" alt="S3 buckets used by CloudDoc" style="max-width: 90%; height: auto;">

**Step 3:** Check that the **EC2 instance** is running the backend service properly and the **API backend** responds correctly.

<img src="/images/5-Workshop/AWS-Console/ec2-instances.png" alt="EC2 instance used for the backend API" style="max-width: 90%; height: auto;">

**Step 4:** Ensure the **RDS PostgreSQL** database is available and ready to store document metadata.

<img src="/images/5-Workshop/AWS-Console/rds-database.png" alt="RDS PostgreSQL instance for document metadata" style="max-width: 90%; height: auto;">

{{% notice info %}}
**Note:** Checking the infrastructure thoroughly at this stage makes troubleshooting much easier during later integration steps.
{{% /notice %}}
