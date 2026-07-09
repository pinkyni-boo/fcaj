---
title: "Blog 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

The third blog I translated focused on a practical security and operations concern: when building server-side rendering applications such as **Next.js** or **Nuxt** on AWS, how can the server-side code access AWS resources safely without storing `Access Key` or `Secret Key` values in source code or environment variables?

AWS introduced **IAM Compute Roles** for **AWS Amplify Hosting** to solve this problem. I found this topic especially important because it connects directly to real cloud security practices.

### 1. What IAM Compute Roles are

IAM Compute Roles allow an **IAM Role** to be attached directly to the runtime environment of an SSR application hosted on Amplify. As a result, server-side code can access AWS services through temporary permissions, in a way similar to **EC2 Instance Profiles** or **Lambda Execution Roles**.

The main benefits are:

- no hard-coded access keys,
- better permission control per environment,
- and stronger alignment with the **Principle of Least Privilege**.

### 2. Common use cases

According to the AWS article, IAM Compute Roles are useful when:

- accessing **AWS Secrets Manager** or **Systems Manager Parameter Store**,
- connecting to **Amazon RDS** or **Amazon DynamoDB** without embedding credentials,
- calling AWS service APIs from server-side application code,
- and using different permission scopes for development, staging, and production.

### 3. Example implementation

In the AWS example, a **Next.js** application was configured to access a private **Amazon S3 bucket**. The main flow included:

1. creating an IAM Role with read access to S3,
2. allowing Amplify Hosting to use that role,
3. deploying the Next.js application to Amplify,
4. and using the AWS SDK inside an API Route to access S3 data.

With IAM Compute Roles, the application can authenticate against AWS without storing sensitive credentials in code.

### 4. What I learned from this blog

This blog helped me understand that cloud security is not only about network rules or private subnets. It also depends on how an application receives permission to access resources. From the CloudDoc perspective, this is a very important lesson because once the system moves closer to real deployment, credential management and permission design must be handled properly from the beginning.

### 5. Connection to CloudDoc

- CloudDoc should favor **IAM Roles** instead of hard-coded access keys when deployed on AWS.
- Features such as file upload, presigned URL generation, and private resource access should follow a secure permission model.
- This article also supports the FCAJ evaluation checklist around security and **least privilege**.

### 6. Conclusion

IAM Compute Roles simplify AWS permission management for SSR applications hosted on Amplify. It is a very useful feature for systems that need server-side access to AWS resources while still maintaining strong security and permission-governance practices.

**FCAJ group post link:** https://www.facebook.com/share/p/1PEvrCKJsS/
