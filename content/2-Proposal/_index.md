---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# Project Proposal: CloudDoc Platform for HUTECH Students
## An Intelligent Learning Document Management and Retrieval System with a High-Availability AWS Architecture

### 1. Executive Summary
CloudDoc is designed to solve the problem of storing, managing, and searching learning materials such as slides, textbooks, and exam papers for HUTECH students. The platform delivers fast deep-content search while also protecting data through an isolated network architecture built around private subnets.

The solution uses a modern AWS stack including an Application Load Balancer, Multi-AZ Amazon EC2 instances, Amazon RDS PostgreSQL, Amazon SQS, Amazon S3, CloudWatch, and SNS to achieve strong performance, high availability, and asynchronous processing. It also follows a FinOps mindset by automating storage lifecycle management from Amazon S3 to S3 Glacier for long-term cost optimization.

### 2. Problem Statement
**Current problem**

Internal student document-sharing platforms are often deployed on single-server architectures, which makes them vulnerable to downtime during peak traffic periods such as exam season. Processing large PDF or Word files directly on the application server creates CPU bottlenecks and weakens the user experience. In addition, using a heavyweight external search stack for a school-level project is not always efficient, while keeping old documents in hot storage forever increases infrastructure costs unnecessarily.

**Solution**

CloudDoc applies a decoupled and highly available architecture:

- Users access the platform through an Application Load Balancer in a public subnet.
- Amazon EC2 application servers and Amazon RDS PostgreSQL are isolated inside private subnets for stronger security.
- Clients upload files directly to Amazon S3 using Presigned URLs instead of sending heavy files through the application server.
- New S3 upload events are pushed into Amazon SQS so background EC2 workers can extract document text asynchronously.
- Business data, metadata, and search data are stored centrally in Amazon RDS PostgreSQL, which also provides built-in full-text search capability.
- CloudWatch and SNS are used to monitor system health and send alerts when resource usage crosses risk thresholds.

**Benefits and return on investment**

The solution creates a centralized academic material portal that is fast, secure, and easy to scale. Automatically moving less frequently accessed files to S3 Glacier helps reduce storage cost. Direct upload to S3 lowers bandwidth and CPU pressure on EC2. Using PostgreSQL full-text search instead of a separate dedicated search cluster also helps keep infrastructure spending under control in the early stage of the project.

### 3. Solution Architecture
The platform is designed with a clear separation between the web access flow and the background processing flow, while also ensuring high availability through deployment across multiple Availability Zones.

![CloudDoc AWS Architecture](/images/2-Proposal/clouddoc-architecture.png)

### AWS Services Used
- **VPC, Internet Gateway, and ALB:** Provide the secure network boundary and receive incoming Internet traffic.
- **Amazon EC2 (Multi-AZ):** Run the Node.js application, serve APIs, generate Presigned URLs, and execute background jobs.
- **Amazon RDS PostgreSQL:** Store metadata, business data, and support full-text search.
- **Amazon S3 and S3 Glacier:** Store original document files and archive less frequently used files to cold storage.
- **Amazon SQS:** Decouple file upload from document text extraction processing.
- **Amazon CloudWatch and Amazon SNS:** Monitor infrastructure health and deliver notifications when resource usage exceeds thresholds.

### Component Design
- **Frontend:** Built with React and Tailwind CSS, providing Upload, Search, Filter, and Document Preview interfaces.
- **Application Layer:** EC2 app servers receive requests from the ALB, handle user logic, and issue Presigned URLs.
- **Background Processing:** EC2 workers receive messages from SQS and process text extraction jobs.
- **Storage Layer:** Original files are stored in S3, metadata is stored in RDS PostgreSQL, and old files are moved to Glacier.
- **Monitoring Layer:** CloudWatch collects metrics and SNS sends warning emails when incidents occur.

### 4. Technical Implementation
**Implementation phases**

1. **Design and planning:** Finalize the AWS architecture diagram, complete UI/UX design, and standardize the PostgreSQL schema.
2. **Network and resource provisioning:** Configure the VPC, public and private subnets, security groups, ALB, EC2, RDS, and SQS.
3. **Development and integration:** Build the React frontend, Node.js backend APIs, the Presigned URL upload flow, background worker processing, and PostgreSQL full-text search.
4. **Monitoring and optimization:** Configure CloudWatch alarms, SNS notifications, load testing, S3 lifecycle policies, and overall system tuning.

**Technical requirements**

- **Frontend:** React Context API, asynchronous API handling with Fetch or Axios, form validation, and embedded document preview.
- **Backend/Cloud:** Node.js, AWS SDK, S3 Presigned URL handling, SQS, RDS PostgreSQL, full-text search, IAM, security groups, and core AWS networking knowledge.

### 5. Timeline and Milestones
- **Month 1:** Gather requirements, design the system architecture, and prepare the initial UI/UX mockups in Figma.
- **Month 2:** Provision VPC, ALB, EC2, RDS PostgreSQL, and S3, then implement the direct upload flow.
- **Month 3:** Integrate SQS workers, full-text search, CloudWatch, SNS, end-to-end testing, and demo video preparation.

### 6. Budget Estimation
- **Amazon EC2 (2 small Multi-AZ instances):** Optimized for educational use and potentially partially covered by Free Tier in the early stage.
- **Amazon RDS PostgreSQL:** Can be provisioned with a small instance size to keep demo-stage costs low.
- **Application Load Balancer:** Expected to be one of the main ongoing infrastructure costs due to the high-availability design.
- **Amazon S3 and S3 Glacier:** Low cost and well optimized through lifecycle policies.
- **Amazon SQS, CloudWatch, and SNS:** Minimal cost at the current expected usage scale.

**Estimated monthly cost:** around 20 to 25 USD per month, mainly driven by ALB and RDS.

### 7. Risk Assessment
| Risk | Impact | Probability | Mitigation Strategy |
| --- | --- | --- | --- |
| Local infrastructure failure | Very high | Low | Use Multi-AZ deployment for redundancy |
| EC2 overload during traffic spikes | High | Medium | Use ALB together with CloudWatch monitoring |
| Bandwidth bottleneck from large file uploads | Medium | High | Use Presigned URLs and enforce upload size limits |
| Background processing data loss | High | Low | Decouple processing with Amazon SQS |

### 8. Expected Outcomes
**Technical outcome:** Successfully build a CloudDoc platform on a modern AWS architecture with high availability, strong security, and effective document content search.

**Long-term value:** The system gives HUTECH students a centralized and efficient way to retrieve study materials, while also demonstrating the development team’s ability to design and implement professional cloud architecture.
