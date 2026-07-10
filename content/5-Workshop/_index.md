---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---


# Building CloudDoc on AWS

#### Workshop overview

CloudDoc is a student-oriented document sharing platform. Users submit documents from a web interface, the backend handles business rules, Amazon S3 stores document files, the database stores metadata, and administrators approve submissions before they become publicly available. Section 5 is written as an end-to-end workshop so the reader can follow one complete document lifecycle instead of seeing isolated AWS services without context.

The workshop walks through the full implementation path: preparing the environment, uploading a document, validating that the object is stored correctly in AWS, testing the moderation workflow, synchronizing the visible application state, and finally cleaning up temporary resources to avoid unnecessary cost. This structure helps the report demonstrate design, implementation, validation, and operations together.

#### Objectives

After reading this workshop, the reader should be able to:

- understand the role of each component in CloudDoc,
- follow the document upload and approval flow from start to finish,
- map the AWS Console screenshots to the exact implementation steps,
- review representative frontend and backend integration snippets,
- and see that the project includes monitoring, validation, and resource clean-up.

#### Expected result

The final outcome is a system where users can upload documents successfully, administrators can approve documents in the moderation area, approved documents appear in search results, end users can preview or download them, and the environment is monitored with CloudWatch logs, metrics, and alarms.

#### Demo video

Reviewers can watch the recorded CloudDoc demo here: [CloudDoc demo video](https://drive.google.com/drive/folders/1-mvKrbzs08WWHUT0-whSGeNwgtwd4Uid?usp=sharing).

#### Workshop structure

1. [Introduction](5.1-workshop-overview/)
2. [Prerequisite](5.2-prerequiste/)
3. [Implement upload and storage flow](5.3-s3-vpc/)
4. [Test the system end-to-end](5.4-s3-onprem/)
5. [Client integration and observability](5.5-policy/)
6. [Update data](5.6-cleanup/)
7. [Clean resources](5.7-clean-resources/)
