---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
## A document management and learning-resource discovery platform designed with AWS deployment in mind

### 1. Executive summary
CloudDoc is a platform designed to help HUTECH students store, search, share, preview, and contribute academic materials such as slides, lecture notes, outlines, assignments, and exam resources. The goal is not simply to provide a place to upload files, but to build a structured, searchable, and moderated learning-resource library.

During this internship, my main contribution focused on frontend development, while I also supported the team in aligning UI workflows with backend integration, metadata design, and AWS-oriented deployment thinking. Because of that, this proposal reflects both the product perspective and the system-design perspective needed to move CloudDoc beyond a classroom demo.

The key idea behind the proposal is that CloudDoc should not be treated as a simple file-sharing website. Instead, it should be designed as a layered system where presentation, business logic, metadata management, and file storage are separated clearly enough to scale in future phases.

### 2. Problem statement
In many student environments, learning materials are scattered across personal drives, chat groups, temporary links, and loosely organized folders. This creates several practical issues:

- Students spend unnecessary time searching for the right file or the most reliable version.
- Document quality is hard to control because there is no moderation flow or shared metadata standard.
- Files are often duplicated, mislabeled, or lost when old links expire.
- New users have difficulty identifying which resources are useful and trustworthy.

**Current challenges**

If the entire upload and download flow is routed through the application server, the backend quickly becomes a bottleneck as file size and user traffic increase. In addition, when file storage and metadata are not separated, it becomes harder to scale search, preview, moderation, and access-control features.

Another important challenge is that many existing file-sharing setups only solve the store file problem, not the use the file effectively problem. Without structured metadata such as school, department, subject, uploader, approval status, and usage signals, document discovery becomes inefficient over time.

**Proposed solution**

CloudDoc is proposed with the following structure:

- A React frontend for search, upload, preview, and administration workflows.
- A Node.js/Express backend for business logic, access control, and presigned URL generation.
- PostgreSQL for structured metadata, approval states, uploader information, and document statistics.
- Amazon S3 for original file storage and direct upload support through presigned URLs.
- Extension-ready services such as CloudFront, SQS, CloudWatch, SNS, and Glacier for performance, asynchronous processing, observability, and storage optimization.

The most important design choice is to let the frontend upload files directly to S3 through presigned URLs while the backend focuses on metadata and business logic. This is a practical architecture for a document-centric platform expected to grow over time.

### 3. Solution architecture
The architecture below illustrates the AWS-oriented direction for CloudDoc across the content-delivery layer, application layer, data layer, and operational support layer:

<img src="/images/2-Proposal/aws-drawio-cloudoc.png" alt="CloudDoc AWS Architecture" style="max-width: 90%; height: auto;">

**Main component explanation**

- **Amazon CloudFront and Amazon S3 (Static):** deliver the static frontend efficiently to users while reducing latency and keeping the application layer focused on dynamic requests.
- **Internet Gateway and Application Load Balancer:** receive incoming traffic and route requests into the backend layer.
- **Amazon EC2:** runs the Express backend, generates presigned URLs, accepts metadata submissions, and handles the core business logic.
- **Amazon RDS PostgreSQL:** stores document metadata, account data, moderation status, and structured information required for search and management flows.
- **Amazon S3 (Upload):** stores uploaded documents and supports direct file transfer from the frontend.
- **Amazon SQS:** provides a future-ready path for asynchronous jobs such as document processing, scanning, extraction, or indexing.
- **Amazon CloudWatch and Amazon SNS:** support logging, monitoring, alerting, and operational visibility.
- **Amazon S3 Glacier:** provides long-term storage-cost optimization for infrequently accessed materials.

**Why this architecture matters**

This architecture shows that CloudDoc is not only a UI exercise. It is framed as a complete system with content delivery, application processing, structured metadata, object storage, and operational readiness. That perspective is important because it creates a realistic roadmap from internship demo to a more production-like platform.

### 4. Technical implementation
The practical internship scope stayed aligned with what the team could realistically complete in the current codebase:

- Building the React frontend for Home, Search, Upload, Preview, User Profile, and Admin Dashboard pages.
- Designing simulated login and role-based access for students and administrators.
- Standardizing document metadata for search, moderation, and management flows.
- Preparing the document upload flow around the presigned URL model.
- Supporting integration with the Express backend, PostgreSQL, and S3 for the demo stage.

This also means that not every AWS component in the architecture was fully implemented during the internship. Services such as SQS, CloudWatch, SNS, and Glacier currently represent a justified future direction rather than a fully completed delivery. Making that distinction explicit keeps the proposal honest and technically credible.

### 5. Roadmap and milestones
**Phase 1: Core product stabilization**

- Finalize search, upload, preview, and navigation experience.
- Improve moderation flow and metadata consistency.
- Complete the admin-facing management experience.

**Phase 2: Real cloud integration**

- Strengthen frontend integration with Express and PostgreSQL.
- Complete the direct-to-S3 upload workflow through presigned URLs.
- Improve environment setup and end-to-end testing reliability.

**Phase 3: System expansion**

- Add background processing for heavier or asynchronous tasks.
- Improve monitoring, alerting, and logging for deployment readiness.
- Apply storage lifecycle optimization for older, less frequently accessed documents.

### 6. Budget estimate
The image below summarizes the estimated monthly cost of the CloudDoc architecture in a near-production setup. The estimate is based on an AWS Pricing Calculator snapshot exported on **June 17, 2026**:

<img src="/images/2-Proposal/aws-monthly-cost-cloudoc.jpg" alt="CloudDoc AWS Monthly Cost" style="max-width: 90%; height: auto;">

| Item | Estimated monthly cost (USD) | Notes |
| --- | ---: | --- |
| RDS PostgreSQL Multi-AZ | 85.50 | The largest cost component because availability is prioritized |
| EC2 Server (t4g.micro x2) | 19.51 | Two application instances across two AZs |
| Application Load Balancer | 18.98 | Shared entry point and traffic distribution |
| NAT Instance (t4g.nano) | 4.64 | Outbound support for private subnet resources |
| CloudWatch | 4.01 | Basic metrics, logs, and alarms |
| Other (SNS, CloudFront) | 0.89 | Small supporting service cost |
| **Total** | **133.53** | Reference estimate for the target architecture |

This cost profile is more suitable for a production-oriented architecture or a full demo environment than for a minimal student lab. For internship or dev/test environments, the team can reduce cost by:

- Using a smaller single-AZ setup before higher availability is needed.
- Stopping or downsizing EC2 instances outside active development windows.
- Applying S3 lifecycle policies to move cold files to Glacier.
- Enabling detailed CloudWatch logging only where it creates real value.
- Using IAM Roles and an S3 Gateway Endpoint instead of hard-coded access keys.

### 7. Risk assessment
| Risk | Impact | Mitigation |
| --- | --- | --- |
| Misalignment between frontend, backend, and the presigned URL upload flow | Upload failures and inconsistent data flow | Standardize API contracts and validate the upload path end-to-end before demo |
| Inconsistent metadata or weak moderation | Poor search experience and noisy content quality | Define mandatory metadata fields and add an approval workflow for administrators |
| Weak AWS permission design | Data exposure or over-privileged access | Apply IAM Roles, the Principle of Least Privilege, and avoid hard-coded keys in source code |
| High cost if the full architecture is kept for dev usage | Budget waste before real usage exists | Separate dev/demo environments and review cost regularly |
| Limited operational visibility during incidents | Slow diagnosis and unstable troubleshooting | Add metrics, logs, CloudWatch alarms, and SNS notifications for critical components |
| Internship scope is smaller than the full target architecture | Readers may assume the team over-claimed implementation | Clearly mark what was completed and what remains a future-ready design direction |

### 8. Expected outcomes
CloudDoc provides value at three levels:

- **For end users:** students get a centralized and more trustworthy place to find and contribute learning resources.
- **For the development team:** the project combines frontend, backend, metadata modeling, and AWS system thinking in a single product.
- **For learning outcomes:** the platform connects UI/UX work, practical product thinking, and cloud architecture design in a very applied way.

From my personal perspective, the proposal also reflects an important shift in mindset: moving from building a nice interface to designing an experience that must work together with data flow, security, cost, and system operations. That was one of the most meaningful learning outcomes of this internship.
