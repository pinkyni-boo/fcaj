---
title: "Frontend project setup and CloudDoc system architecture design"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---
### Week 8 Objectives:

* Finalize and approve the cloud infrastructure architecture diagram following a Multi-AZ AWS design as the technical blueprint for the project.
* Initialize the Frontend web application with ReactJS, set up the development environment, and build the core functional interfaces including Upload, Search, and Filtering for CloudDoc.
* Combine self-driven development with in-office learning sessions to align implementation direction and refine the UI based on mentor feedback.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | Finalize the cloud architecture diagram (AWS Architecture):<br>- Design the detailed connection flow across VPC, ALB, EC2, RDS PostgreSQL, S3, SQS, and CloudWatch.<br>- Review the data flow to ensure high availability and private subnet security. | 08/06/2026 | 08/06/2026 |  |
| 2 | Participate in in-office learning while initializing the Frontend project and global state:<br>- Discuss UI direction, user flow, and source code organization with the mentor and team members.<br>- Initialize the ReactJS codebase and integrate Tailwind CSS.<br>- Set up the React Context API (AppContext) for global state management such as authentication and notifications. | 09/06/2026 | 09/06/2026 |  |
| 3 | Develop the Upload module UI:<br>- Design the Upload form with drag-and-drop support.<br>- Build metadata input fields and a real-time style upload progress bar. | 10/06/2026 | 10/06/2026 |  |
| 4 | Develop the Search and Discovery module:<br>- Build an intuitive search bar.<br>- Implement the logic for a dynamic three-level filter chain where University -> Major -> Subject changes based on previous selections. | 11/06/2026 | 11/06/2026 |  |
| 5 | Integrate document preview and basic authorization:<br>- Integrate iframe or `react-pdf` for direct PDF/Docx preview in the web interface.<br>- Configure role-based routing to hide the Upload feature from guest users. | 12/06/2026 | 12/06/2026 |  |


### Week 8 Achievements:

* Successfully finalized the AWS CloudDoc architecture diagram and aligned it with the mentor's optimization and security expectations.
* Made good use of the in-office learning session to validate implementation direction and refine the UI plan with mentor feedback.
* Set up the frontend source code foundation with ReactJS and Tailwind CSS, with smooth global state handling through Context API.
* Completed the Upload form with drag-and-drop support and a professional upload progress indicator.
* Successfully implemented the dynamic three-level category filter and keyword search bar.
* Embedded an online document preview experience that allows users to read PDF files directly with low latency.

