---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Campus IT Support Ticket Portal
## A Serverless Helpdesk System on AWS for Campus IT Support

---

### 1. Executive Summary

Campus IT Support Ticket Portal is a serverless helpdesk system for a school or university environment. The system allows students and staff to submit IT support requests, track ticket history and processing status, and receive notifications when a ticket is created or updated. It also provides an admin console for IT staff to receive, classify, update, add processing notes to, and delete tickets when needed.

The frontend is publicly deployed using **AWS Amplify Hosting** and connected to GitHub for automatic build and deployment. Users register and sign in through **Amazon Cognito Hosted UI**. The backend is built with **Amazon API Gateway**, **AWS Lambda**, **Amazon DynamoDB**, **Amazon S3**, **Amazon SES**, **Amazon CloudWatch**, and **AWS IAM**.

The project is more than a basic ticket CRUD system. It supports private file attachments using S3 Presigned URLs, asynchronous email notifications through Amazon SES, and real-time interface updates through DynamoDB Streams and WebSocket API.

---

### 2. Problem Statement

In a campus environment, IT support requests are often reported through separate channels such as messages, email, phone calls, or direct conversations. This creates several problems:

- Requests may be lost, duplicated, or handled without a clear processing history.
- Users cannot easily know the current status of their support requests.
- IT staff lack a centralized queue for classifying and prioritizing incidents.
- Supporting files such as error screenshots or related documents are often sent separately.
- Admins need a clearer view of total tickets, in-progress tickets, high-priority tickets, and resolved tickets.

Campus IT Support Ticket Portal solves these problems by providing a centralized system with two main roles:

- **Users:** sign up/sign in, submit tickets, upload attachments, look up tickets, view request history, and receive notifications.
- **Admins:** view dashboards, search/filter tickets, inspect details, update status, add processing notes, delete tickets, and receive alerts for High/Critical tickets.

---

### 3. Solution Architecture

#### Overall Architecture Diagram

{{< project-image
src="images/5-Workshop/5.2-System-Architecture/Architecture.jpg"
alt="Campus IT Support Ticket Portal Architecture"
caption="Figure 2.1: Overall architecture of the Campus IT Support Ticket Portal."
>}}

#### Architecture Description

Users and administrators access the frontend hosted on **AWS Amplify Hosting**. When authentication is required, the browser is redirected to **Amazon Cognito Hosted UI**. After successful authentication, Cognito issues JWT tokens to the frontend.

The frontend sends the JWT token in requests to **Amazon API Gateway HTTP API**. API Gateway uses a **JWT Authorizer** to validate the token before forwarding the request to **CampusSupportTicketService Lambda**. Lambda processes ticket business logic, checks User/Admin permissions, stores data in **DynamoDB CampusSupportTickets**, and generates **S3 Presigned URLs** for uploading or downloading attachments from a private bucket.

When a ticket is created or updated, **DynamoDB Streams** triggers **CampusSupportNotificationService**. This Lambda function sends emails through **Amazon SES** and publishes real-time events through **API Gateway WebSocket API**. WebSocket connection information is managed by **CampusSupportWebSocketService** and stored in **DynamoDB CampusSupportConnections**.

---

### 4. AWS Services Used

| Service | Role in the system |
| --- | --- |
| **AWS Amplify Hosting** | Hosts the frontend and automatically builds/deploys from GitHub |
| **Amazon Cognito Hosted UI** | Manages user sign-up, sign-in, sign-out, and sessions |
| **Cognito Groups** | Separates user permissions through `Users` and `Admins` groups |
| **API Gateway HTTP API** | Provides endpoints for creating, reading, updating, and deleting tickets |
| **API Gateway JWT Authorizer** | Validates Cognito JWT tokens before allowing API access |
| **API Gateway WebSocket API** | Sends real-time updates to User/Admin browsers |
| **AWS Lambda** | Processes ticket logic, notifications, WebSocket events, and authorization checks |
| **Amazon DynamoDB** | Stores ticket data and WebSocket connection records |
| **DynamoDB Streams** | Detects ticket creation/update events and triggers notifications |
| **Amazon S3** | Stores attachment files in a private bucket |
| **S3 Presigned URL** | Allows temporary upload/download access without making the bucket public |
| **Amazon SES** | Sends confirmation, high-priority alert, and status-update emails |
| **Amazon CloudWatch** | Stores Lambda/API logs and supports debugging and monitoring |
| **AWS IAM** | Grants least-privilege permissions between Lambda and other AWS services |

---

### 5. Main Features

#### User Features

- Sign up, sign in, and sign out using Amazon Cognito.
- Submit IT support requests by category such as WiFi, account, software, or device.
- Select priority level and describe the issue.
- Attach PDF, PNG, JPG, or WebP files.
- Receive a ticket ID after submission.
- Look up a ticket by ID.
- View submitted request history.
- Receive confirmation emails and real-time status updates.

#### Admin Features

- View dashboard counts for total, in-progress, high-priority, and resolved tickets.
- Search and filter tickets by status, priority, or issue category.
- View ticket details and attachments.
- Update ticket status and processing notes.
- Delete tickets within the demo scope.
- Receive alert emails for High or Critical tickets.
- See ticket list updates without reloading the page.

---

### 6. Implemented API

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.3-Amazon-API-Gateway/routes.png"
alt="Implemented API Gateway routes"
caption="Figure 2.2: API Gateway routes used for ticket-management functions."
>}}

All routes are protected by JWT. Administrative actions are additionally checked by Lambda using Cognito Group information.

---

### 7. Main Data Model

#### CampusSupportTickets Table

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.5-Amazon-DynamoDB/ticket-table-overview.png"
alt="DynamoDB CampusSupportTickets table"
caption="Figure 2.3: Overview of the DynamoDB table used to store ticket data."
>}}

#### CampusSupportConnections Table

This table stores active WebSocket `connectionId` values so that the notification Lambda can send update events to connected browsers.

---

### 8. Testing Plan

| Test case | Expected result |
| --- | --- |
| User signs up and signs in | Cognito authenticates successfully and the account belongs to Users group |
| User submits a valid ticket | Ticket is stored in DynamoDB and a ticket ID is returned |
| User uploads an attachment | File is uploaded to S3 through a Presigned URL |
| User looks up a ticket | Correct ticket information is returned |
| Admin views dashboard | Ticket list and summary counts are displayed correctly |
| Admin updates ticket status | DynamoDB is updated and a MODIFY event is generated |
| Admin deletes a ticket | Ticket is removed from DynamoDB |
| Ticket is created | SES sends confirmation email to verified address |
| High/Critical ticket is created | SES sends alert email to IT support team |
| Ticket changes | WebSocket sends an event and UI updates without reload |
| Missing JWT request | API Gateway rejects the request |
| Normal user calls admin action | Lambda denies the operation |
| Backend error occurs | CloudWatch Logs records the error for debugging |

---

### 9. Budget Estimation

| Service | Estimated Cost/Month | Notes |
| --- | --- | --- |
| AWS Amplify Hosting | ~$0-2 | Small frontend traffic |
| Amazon Cognito | ~$0 | Demo users fit within free tier |
| API Gateway HTTP/WebSocket API | ~$0-2 | Depends on requests and realtime connections |
| AWS Lambda | ~$0-1 | Runs by request/event |
| Amazon DynamoDB | ~$0-2 | Small ticket dataset with on-demand usage |
| Amazon S3 | ~$0-1 | Small attachment files |
| Amazon SES | ~$0-1 | Low demo email volume |
| Amazon CloudWatch | ~$0-1 | Basic Lambda/API logs |
| **Total** | **~$0-10/month** | Depends on traffic, file storage, and email volume |

---

### 10. Risks and Limitations

| Risk/Limitation | Impact | Mitigation |
| --- | --- | --- |
| SES remains in Sandbox | Emails can only be sent to verified addresses | Request production access for real deployment |
| Incorrect Cognito group configuration | User/Admin permissions may be wrong | Validate group claims in Lambda |
| IAM role is too broad | Security risk increases | Apply least-privilege permissions |
| S3 bucket is accidentally public | Attachments may be exposed | Keep bucket private and use Presigned URLs |
| CORS is misconfigured | Frontend cannot call API | Configure CORS for the Amplify domain |
| WebSocket connection expires | UI may not receive real-time updates | Remove invalid connection IDs and reconnect when needed |
| Resources are not cleaned up | Unexpected cost may occur | Monitor Billing Dashboard and document cleanup steps |

---

### 11. Expected Outcomes

The project aims to deliver a complete serverless helpdesk system at a demo/portfolio junior cloud project level with the following outcomes:

- Frontend deployed publicly with AWS Amplify Hosting.
- User/Admin authentication and authorization through Amazon Cognito.
- API protected by JWT Authorizer.
- Lambda handles ticket business logic and permission checks.
- DynamoDB stores tickets and WebSocket connections.
- S3 stores private attachments using Presigned URLs.
- SES sends confirmation and notification emails.
- WebSocket supports real-time UI updates.
- CloudWatch supports error observation and debugging.
- IAM applies least-privilege access for Lambda functions.

The main value of the project is that it simulates a realistic campus IT support workflow using a practical serverless architecture on AWS.