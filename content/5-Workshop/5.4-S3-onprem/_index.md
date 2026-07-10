---
title: "Test the system end-to-end"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---


#### Objective

This section proves that a document truly moves through the full CloudDoc workflow, from user submission to moderation approval and final visibility in the user-facing interface. This is the strongest end-to-end evidence in the workshop.

#### Demo evidence

The full recorded demo is available here for review: [CloudDoc demo video](https://drive.google.com/drive/folders/1-mvKrbzs08WWHUT0-whSGeNwgtwd4Uid?usp=sharing).

#### Test sequence

**Step 1:** Confirm the uploaded document appears in the admin moderation dashboard with a `pending` state.

<img src="/images/5-Workshop/AWS-Console/admin-approve-dashboard.png" alt="Admin dashboard with pending document" style="max-width: 90%; height: auto;">

**Step 2:** Approve the document from the administrator view and check the success response (toast notification).

<img src="/images/5-Workshop/AWS-Console/admin-approve-toast.png" alt="Approval success notification" style="max-width: 90%; height: auto;">

**Step 3:** Open the search page again and confirm that the document is visible. You can continue with preview or download access to verify that the state change is reflected in the user interface.

<img src="/images/5-Workshop/AWS-Console/search-result.png" alt="Approved document in search results" style="max-width: 90%; height: auto;">
