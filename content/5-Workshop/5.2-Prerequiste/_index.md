---
title: "Prerequisite"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---


#### Objective

This section confirms that the environment is ready before the upload and end-to-end workflow begins. Without this preparation, issues such as incorrect endpoints, invalid CORS configuration, unresponsive EC2 instances, or unavailable database resources would weaken the later validation steps.

#### Items to verify

- the web interface is reachable,
- the backend API responds correctly,
- the S3 bucket exists and accepts the intended upload flow,
- the PostgreSQL database is available,
- and sample documents are ready for testing.

#### Subsections

1. [Verify the environment](5.2.1-verify-frontend-readiness/)
2. [Prepare source data and configuration](5.2.2-prepare-source-data/)
