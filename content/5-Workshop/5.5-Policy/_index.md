---
title: "Client integration and observability"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---


#### Objective

After a document is approved, users need a natural application flow for preview and download. At the same time, a complete workshop should also demonstrate operational visibility, not just deployment. This section therefore combines client integration with AWS observability.

#### Integration and Observability Steps

**Step 1:** The frontend loads document information from the backend, securely distributed via **CloudFront**.

<img src="/images/5-Workshop/AWS-Console/cloudfront-details.png" alt="CloudFront distribution details for the frontend" style="max-width: 90%; height: auto;">

**Step 2:** The backend issues safe access URLs. Users can seamlessly **preview and download** the approved documents.

<img src="/images/5-Workshop/AWS-Console/preview-download.png" alt="Preview and download screen for an approved document" style="max-width: 90%; height: auto;">

**Step 3:** **CloudWatch** collects backend logs and runtime metrics to ensure proper operational visibility.

<img src="/images/5-Workshop/AWS-Console/cloudwatch-logs-metrics.jpg" alt="CloudWatch log groups and metrics for the backend" style="max-width: 90%; height: auto;">

**Step 4:** A **CloudWatch alarm** demonstrates proactive monitoring to track runtime anomalies.

<img src="/images/5-Workshop/AWS-Console/cloudwatch-alarm.jpg" alt="CloudWatch alarm for backend monitoring" style="max-width: 90%; height: auto;">
