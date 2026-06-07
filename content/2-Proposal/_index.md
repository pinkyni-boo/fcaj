---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# CloudDoc Platform for HUTECH Students
## An Intelligent Learning Document Management and Retrieval System with AWS-based Full-text Search

### 1. Executive Summary
CloudDoc is designed to solve the problem of storing and searching learning materials such as slides, textbooks, and exam papers for HUTECH students. The system supports deep search inside document content using full-text search with millisecond-level response time, while also enabling secure direct file uploads to cloud storage. The platform combines Amazon S3, DynamoDB, OpenSearch, and an Amazon EC2 backend to deliver strong performance, while applying a FinOps mindset through automated storage lifecycle policies to optimize operating costs.

### 2. Problem Statement
**Current problem**

Student document sharing today is still largely manual, usually through scattered Google Drive links. Existing internal systems can often search only by file name. If the server has to scan the full content of PDF or Word files on demand, it creates linear processing overhead that can overload and slow down the system. In addition, storing old and rarely accessed files forever leads to wasted storage and unnecessary infrastructure cost.

**Solution**

CloudDoc uses Amazon EC2 as the central backend server running Node.js and Express to handle business logic, authorization, and communication with the React frontend. Original files are stored in Amazon S3 instead of local disk, while S3 Lifecycle Policies automatically move infrequently accessed files to S3 Glacier. To solve the search problem, a background processing flow extracts text from documents and pushes it into Amazon OpenSearch Service as an inverted index. Lightweight metadata such as file name, category, uploader, and download count is stored in Amazon DynamoDB. The upload process is optimized through S3 Presigned URLs, allowing browsers to send files directly to S3 without routing large payloads through EC2.

**Benefits and return on investment**

The solution creates a centralized learning portal that helps students find the right materials even when typing without accents or with minor spelling mistakes. From an infrastructure perspective, the system can reduce storage cost significantly by moving unused files to S3 Glacier after 30 days. Direct upload also reduces EC2 bandwidth pressure. Since the team uses HUTECH learning materials as seed data, input data collection cost is minimal.

### 3. Solution Architecture
The platform clearly separates the user interface layer from the compute and storage layer. Data is synchronized between a NoSQL metadata store and a dedicated search engine.

![CloudDoc Edge Architecture](/images/2-Proposal/edge_architecture.jpeg)

![CloudDoc Platform Architecture](/images/2-Proposal/platform_architecture.jpeg)

### AWS Services Used
- **Amazon EC2:** Hosts the Node.js backend, serves APIs, and runs text extraction tasks.
- **Amazon S3 and S3 Glacier:** Store physical document files and automatically move cold data to cheaper storage tiers.
- **Amazon DynamoDB:** Stores metadata such as file names, category structure, user information, and download counts.
- **Amazon OpenSearch Service:** Stores text indexes and powers fuzzy search functionality.

### Component Design
- **Frontend:** Built with React and Tailwind CSS, providing a 3-level filter chain of `University -> Major -> Subject` together with smart search.
- **Upload flow:** EC2 generates S3 Presigned URLs so the browser can upload files directly to S3.
- **Data synchronization:** The DynamoDB record ID is aligned with the OpenSearch `_id` field for fast cross-referencing.

### 4. Technical Implementation
**Implementation phases**

The project is split into two main tracks, Frontend UI/UX and Cloud Infrastructure, and developed through four phases:

1. **System design:** Draw the architecture diagram, design the UI/UX in Figma, and define the DynamoDB table structure.
2. **Platform setup:** Create the VPC, launch EC2, provision S3 buckets, and configure IAM permissions.
3. **Development and integration:** Build React components, implement the Node.js API for Presigned URLs, and create the text extraction flow that pushes content into OpenSearch.
4. **Testing and optimization:** Validate full-text search, verify S3 lifecycle behavior, measure latency, and clean up resources.

**Technical requirements**

- **Frontend:** Strong understanding of React state management, asynchronous flows with Promises and async/await, and document preview integration through iframe or `react-pdf`.
- **Cloud/Backend:** Knowledge of Node.js, AWS SDK, CORS, IAM policies, NoSQL synchronization, and OpenSearch inverted index concepts.

### 5. Timeline and Milestones
- **Month 1:** Study AWS services, shape the solution idea, design the architecture, and gather seed data such as slides and course outlines.
- **Month 2:** Build the web UI foundation, provision AWS resources including EC2, S3, and DynamoDB, and prepare the backend environment.
- **Month 3:** Complete the direct upload flow, integrate OpenSearch, test fuzzy search, package the step-by-step documentation, and record a demo video.

### 6. Budget Estimation
- **Amazon EC2 (t2.micro):** Within Free Tier, approximately $0.00/month.
- **Amazon S3 Standard and Glacier:** Estimated 10 GB of data, approximately $0.25/month.
- **Amazon DynamoDB:** Low read/write demand focused on metadata, expected to stay within Free Tier.
- **Amazon OpenSearch (t3.small.search):** Core service, approximately $15.00 to $25.00/month.
- **Data transfer:** Minimized through Presigned URLs, approximately $0.50/month.

**Estimated total cost:** around $25.75/month, with OpenSearch being the largest cost component.

### 7. Risk Assessment
**Risk matrix**

- **Server bandwidth bottleneck:** High impact, low probability.
- **Data synchronization failure:** High impact, medium probability.
- **Budget overrun due to 24/7 OpenSearch runtime:** Medium impact, medium probability.

**Mitigation strategies**

- **Data flow:** Validate that file size is under 20 MB in the browser before calling the API.
- **Synchronization:** Implement rollback or transaction-like recovery if DynamoDB writes succeed but OpenSearch indexing fails.
- **Cost control:** Configure AWS Budgets and CloudWatch Alarms to email alerts when spending reaches the warning threshold.

### 8. Expected Outcomes
**Technical outcome:** Successfully build a modern cloud-based web app that handles document upload and retrieval through full-text search.

**Long-term value:** Demonstrate the ability to design cost-efficient cloud infrastructure with safe data lifecycle management, and create a foundation that can later be replicated for other universities.
