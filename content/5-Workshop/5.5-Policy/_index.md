---
title: "Security, operations, and AWS extension direction"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---
### Basic security

- Only the backend should generate presigned URLs.
- S3 permissions should be limited to the correct bucket and the correct actions.
- The database should only be reachable from the backend, not exposed publicly.
- The EC2-attached IAM Role should follow the **Principle of Least Privilege**.
- `Access Key` and `Secret Key` values should not be hard-coded in `.env`; the backend should receive temporary permissions through **IAM Roles** and **IMDSv2**.

### Operations

- Track upload failures, CORS issues, and backend response errors.
- Log presigned URL generation, metadata persistence, and download activity.
- Prepare a monitoring dashboard so integration issues can be spotted faster.
- Configure the **CloudWatch Agent** to collect backend logs, queue-processing logs, and operational metrics.
- Create a **CloudWatch Alarm** for CPU `>= 80%` for `2` consecutive periods, with each period set to `5 minutes`.
- Send notifications through an **Amazon SNS Topic** so the team receives email alerts when the system reaches the `IN ALARM` state.

### Extension direction

As CloudDoc grows, the architecture can be extended with:

- **SQS** for background tasks such as extraction, scanning, or indexing.
- **CloudWatch and SNS** for monitoring and alerts.
- **Lifecycle Policy and Glacier** for long-term storage cost optimization.

### Why this matters for the evaluation checklist

This section is important because it proves the workshop is not only about uploading a file successfully. A stronger solution also needs:

- a secure IAM Role-based access model,
- log and metric visibility,
- automatic alerting when resources exceed thresholds,
- and long-term cost-control thinking.

### Practical meaning

This part shows that a good workshop is not only about making a feature work. A suitable solution must also consider access control, error detection, observability, and future scalability. That is what makes this workshop more aligned with the practical spirit of FCAJ and the CloudDoc project.
