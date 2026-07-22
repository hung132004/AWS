---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

#### Project overview

This workshop documents the implementation process of **Campus IT Support Ticket Portal**, a serverless helpdesk web system for receiving and managing IT support requests in a campus environment.

**Deployed website:** [https://main.d37atxjbyyp60m.amplifyapp.com/](https://main.d37atxjbyyp60m.amplifyapp.com/)

The completed system allows users to register, sign in, submit support tickets, upload attachments, track ticket history, and receive status updates. Administrators can view all tickets, search and filter requests, update ticket status, add processing notes, delete tickets, and receive alerts for high-priority issues.

The frontend is deployed publicly through **AWS Amplify Hosting** and is integrated with GitHub for automatic build and deployment.

#### Architecture

The system uses a serverless architecture on AWS. The frontend communicates with **Amazon Cognito** for authentication and sends authenticated requests to **Amazon API Gateway**. API Gateway validates Cognito JWT tokens before invoking **AWS Lambda** functions.

Lambda handles ticket operations, authorization checks, attachment processing, and integration with **Amazon DynamoDB** and **Amazon S3**. The system also uses **Amazon SES**, **Amazon CloudWatch**, **AWS IAM**, and real-time notification components such as DynamoDB Streams and WebSocket API.

{{< project-image
src="images/5-Workshop/5.2-System-Architecture/architecture.jpg"
alt="Campus IT Support Ticket Portal Architecture"
caption="Campus IT Support Ticket Portal Architecture"
>}}

#### AWS services used

| Service | Purpose in this workshop |
| --- | --- |
| AWS Amplify Hosting | Hosts the frontend and deploys updates automatically from GitHub |
| Amazon Cognito | Handles sign-up, sign-in, sign-out, JWT tokens, and `Users`/`Admins` groups |
| Amazon API Gateway | Provides HTTP API and WebSocket API endpoints for frontend-backend communication |
| AWS Lambda | Processes ticket operations, permission checks, notifications, and WebSocket events |
| Amazon DynamoDB | Stores ticket data and WebSocket connection records |
| Amazon S3 | Stores ticket attachment files in a private bucket |
| Amazon SES | Sends ticket confirmation, alert, and status-update emails |
| Amazon CloudWatch | Stores Lambda/API logs and supports debugging and monitoring |
| AWS IAM | Grants least-privilege permissions between Lambda and other AWS services |

#### Implementation content

1. [Project Overview](5.1-project-overview/)
2. [Architecture Overview](5.2-system-architecture/)
3. [Prerequisites](5.3-prerequisites/)
4. [Deploy Frontend with AWS Amplify](5.4-deploy-frontend-with-aws-amplify/)
5. [Configure Authentication with Amazon Cognito](5.5-configure-authentication-with-amazon-cognito/)
6. [Build Backend API with API Gateway and Lambda](5.6-build-backend-api-with-api-gateway-and-lambda/)
7. [Store Ticket Data with DynamoDB](5.7-store-ticket-data-with-dynamodb/)
8. [Store Attachments with Amazon S3](5.8-store-attachments-with-amazon-s3/)
9. [Configure Notification and Monitoring](5.9-configure-notification-and-monitoring/)
10. [Security and IAM Permissions](5.10-security-and-iam-permissions/)
11. [Testing the System](5.11-testing-the-system/)
12. [System Screenshots and Result](5.12-system-screenshots-and-result/)
13. [Resource and Cost Check](5.13-cleanup/)