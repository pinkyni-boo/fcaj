---
title: "Cleanup and cost control"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---
### Purpose of the cleanup stage

After a demo or validation run, the team needs to clean up resources to avoid unnecessary cost. This section also demonstrates that the team understands the dependency order inside the CloudDoc architecture and can end the resource lifecycle responsibly.

### Recommended deletion order

The cleanup order below is chosen to respect infrastructure dependencies:

1. **ALB**
2. **EC2**
3. **RDS PostgreSQL**
4. **SQS, CloudWatch, and SNS**
5. **S3 Bucket**
6. **VPC**

If **CloudFront** is enabled for the static frontend, the distribution should be disabled or deleted before removing the static S3 bucket behind it.

### Step 1 - Delete the Application Load Balancer

- Open **EC2 > Load Balancers**.
- Select the CloudDoc ALB.
- Remove listeners or target groups first if needed by the dependency chain.
- Choose **Delete load balancer** and wait until the deletion is complete.

The ALB should be removed first so the backend instances are no longer attached to an active traffic layer.

### Step 2 - Stop and terminate EC2 instances

- Open **EC2 > Instances**.
- Verify which instances belong to the CloudDoc environment.
- Back up any required data before termination.
- Run **Terminate instance**.

In the IAM Role-based model, terminating EC2 also shuts down the backend runtime and removes compute-level temporary access.

### Step 3 - Delete RDS PostgreSQL

- Open **RDS > Databases**.
- Select the PostgreSQL database or cluster for CloudDoc.
- Decide whether a final snapshot is required:
  - keep a final snapshot if data must be preserved,
  - skip the final snapshot for short-lived demo environments if appropriate.
- Confirm **Delete**.

For a Multi-AZ configuration, wait until both the primary and standby resources are removed.

### Step 4 - Delete SQS, CloudWatch, and SNS resources

- Open **SQS** and delete the background-processing queue if it was created.
- Open **CloudWatch** and delete:
  - backend log groups,
  - custom dashboards,
  - the CPU `>= 80%` alarm,
  - related metric filters or agent configuration if applicable.
- Open **SNS** and delete the alert topic after confirming it is no longer needed.

This step prevents alarms, log retention, and queue cost from remaining after the core system has already been stopped.

### Step 5 - Delete the S3 bucket

- Open **S3** and inspect both the static bucket and the upload bucket if they are separated.
- Remove all objects, versions, delete markers, and unfinished multipart uploads.
- Recheck lifecycle rules if the bucket still appears non-empty.
- Run **Delete bucket**.

An S3 bucket must be fully emptied before deletion. This step is often missed if test uploads or frontend build artifacts are still stored.

### Step 6 - Delete the VPC

- Open **VPC** and verify that child resources have already been removed:
  - subnets,
  - route tables,
  - security groups,
  - internet gateway,
  - NAT resource,
  - endpoints.
- Delete the VPC only after those dependencies are gone.

Because VPC is the infrastructure wrapper, it should always be deleted last.

### Final verification checklist

Before considering the environment fully cleaned up, confirm that:

- no ALB remains active,
- no EC2 instances are still running,
- no billable RDS PostgreSQL resources remain,
- no unnecessary SQS queues, CloudWatch alarms, or SNS topics remain,
- S3 buckets are empty and deleted,
- the demo VPC no longer exists.

### Why this matters in the report

The cleanup section is important because it proves the team not only knows how to create AWS resources, but also how to retire them in the correct order, with dependency awareness and a **FinOps** mindset. That is one of the clearest signs that the workshop is practical rather than purely conceptual.
