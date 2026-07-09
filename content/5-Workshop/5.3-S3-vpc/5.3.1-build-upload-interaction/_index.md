---
title: "Initiate the upload flow"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---


#### Objective

The goal of this step is to turn a valid user action in the web interface into a real object upload to Amazon S3. At this stage, both the frontend experience and the contract between frontend and backend must behave consistently.

#### Steps

1. The user selects a file and enters document metadata.
2. The frontend requests a presigned upload URL from the backend.
3. The backend validates the input and creates a storage key.
4. The frontend uploads the file directly to S3 with `PUT`.
5. The application stores metadata after the object upload succeeds.
