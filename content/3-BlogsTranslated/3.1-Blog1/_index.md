---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

<img src="/images/3-BlogsTranslated/blog1-doc-image.png" alt="Blog 1 Illustration" style="max-width: 90%; height: auto;">

The first blog I translated focused on a very practical product problem: how to keep a web or mobile application smooth even when network connectivity is unstable or temporarily unavailable. Instead of waiting for the server to respond before updating the interface, an offline-first architecture combined with optimistic UI allows users to see immediate feedback while synchronization happens in the background.

The AWS article presented a solution built with **AWS Amplify Gen 2**, **AWS AppSync**, **TanStack Query**, and **MongoDB Atlas**. I found this approach useful because it balances both user experience and data synchronization reliability.

### 1. Solution overview

The architecture described in the blog uses:

- **AWS Amplify Gen 2** for full-stack application setup and deployment.
- **AWS AppSync** to provide the GraphQL API used for synchronization.
- **TanStack Query** for client-side caching, optimistic updates, and rollback handling.
- **MongoDB Atlas** as the backend database.
- **AWS Lambda** for serverless processing and **Amazon Cognito** for user authentication.

One strong idea here is that the client does not stay passive. It actively manages local state and gives earlier feedback to the user.

### 2. How optimistic UI works

Instead of waiting for a server response before updating the interface, optimistic UI lets the application display the expected result immediately after the user takes action. In a to-do application example:

- The user creates a new task.
- The interface shows that task immediately.
- The request is then sent to AppSync to persist the data.
- If the request succeeds, the state remains synchronized.
- If the request fails or the connection is lost, the previous state is restored through rollback.

This reduces the feeling of delay and makes the application feel more responsive, especially under unstable connectivity.

### 3. Main processing flow

From the AWS article, I summarized the flow as:

1. The user creates or updates data.
2. TanStack Query updates the local cache and reflects the result immediately in the UI.
3. A GraphQL request is sent to AWS AppSync.
4. AppSync processes the request and stores the data in MongoDB Atlas.
5. If an error occurs, the cache is restored to the previous state.

The AWS example also mentioned a **First-Come, First-Served** conflict-handling approach to keep the synchronization behavior simpler.

### 4. What I learned from this blog

This article reminded me that user experience is not only about visual design. It also depends on how the system responds to user actions. From a frontend perspective in CloudDoc, offline-first and optimistic UI are highly relevant to flows such as:

- document upload,
- metadata editing,
- moderation status updates,
- and user profile changes.

Even if CloudDoc does not yet implement a full offline-first model, understanding this pattern helps me design more realistic and responsive interaction flows.

### 5. Connection to CloudDoc

- CloudDoc could apply optimistic UI ideas to improve responsiveness in upload and editing forms.
- If the system later needs better support for unstable connections, offline-first thinking would become very valuable.
- The AppSync-based synchronization model also suggests cleaner ways to organize client state in data-heavy applications.

### 6. Conclusion

Offline-first and optimistic UI are becoming important techniques for improving user experience in modern applications. With Amplify, AppSync, and TanStack Query, these patterns become easier to implement while still supporting reliable synchronization when connectivity returns.

**FCAJ group post link:** https://www.facebook.com/groups/awsstudygroupfcj/permalink/2190116435086650/
