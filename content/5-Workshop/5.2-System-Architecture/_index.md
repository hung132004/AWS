---
title: "System Architecture"
date: 2026-07-21
weight: 2
chapter: false
pre: "<b>5.2 </b>"
---

## 1. Architecture Overview

The **Campus IT Support Ticket Portal** is implemented using a serverless architecture on Amazon Web Services.

This architecture does not require the operation of a traditional backend server. Functions such as user authentication, API processing, ticket storage, attachment storage, email notifications, and real-time updates are implemented using managed AWS services.

The frontend is deployed through **AWS Amplify Hosting**. Users register and sign in through **Amazon Cognito Hosted UI**. After successful authentication, Cognito issues JWT tokens to the frontend.

The frontend includes the JWT token in requests sent to **Amazon API Gateway**. API Gateway uses a JWT Authorizer to validate the user before forwarding the request to the appropriate **AWS Lambda** function.

Lambda processes the application logic, interacts with **Amazon DynamoDB** to store ticket data, and uses **Amazon S3** to store attachments.

The system also uses **DynamoDB Streams**, a notification Lambda function, **Amazon SES**, and **API Gateway WebSocket API** to deliver email notifications and real-time updates.

---

## 2. Overall Architecture Diagram

The following diagram presents the main components and data flows of the system.

{{< project-image
src="images/5-Workshop/5.2-System-Architecture/Architecture.jpg"
alt="Campus IT Support Ticket Portal Architecture"
caption="Figure 5.2.1: Overall architecture of the Campus IT Support Ticket Portal."
>}}

---

## 3. Main Components

### 3.1 Users and Administrators

The system supports two primary user groups:

- **User:** a student or staff member who submits IT support requests and tracks their status.
- **Admin:** an IT support team member who receives, classifies, updates, and deletes tickets.

Both user groups access the system through a web browser over HTTPS.

### 3.2 AWS Amplify Hosting

AWS Amplify Hosting is used to host and distribute the system frontend.

Amplify is connected to GitHub and automatically performs the build and deployment process whenever source code is pushed to the repository.

The frontend is developed using Hugo, HTML, CSS, and JavaScript.

### 3.3 Amazon Cognito

Amazon Cognito provides:

- Account registration.
- User authentication.
- Sign-out.
- Session management.
- Authorization through Cognito Groups.
- JWT token issuance.

The system uses two primary groups:

- `Users`
- `Admins`

The JWT token contains user and group information and is sent by the frontend to API Gateway for authenticated requests.

### 3.4 Amazon API Gateway

Amazon API Gateway provides two API types:

- **HTTP API:** supports ticket create, read, update, and delete operations.
- **WebSocket API:** maintains real-time connections between browsers and the backend.

The HTTP API uses a JWT Authorizer to validate tokens issued by Amazon Cognito.

After successful validation, API Gateway forwards the request to the appropriate Lambda function.

### 3.5 AWS Lambda

The system uses multiple Lambda functions to separate responsibilities.

#### CampusSupportTicketService

This Lambda function handles:

- Ticket creation.
- Ticket listing.
- Individual ticket lookup.
- Status updates.
- Processing-note updates.
- Ticket deletion.
- User and Admin permission checks.
- Presigned URL generation for file upload and download.

#### CampusSupportNotificationService

This Lambda function is triggered by DynamoDB Streams to:

- Send confirmation emails when tickets are created.
- Send alerts for High and Critical tickets.
- Send emails when ticket status or processing notes change.
- Publish real-time events through the WebSocket API.

#### CampusSupportWebSocketService

This Lambda function handles:

- The `$connect` event.
- The `$disconnect` event.
- Cognito token validation during connection establishment.
- Storage and removal of `connectionId` values.

### 3.6 Amazon DynamoDB

The system uses two main DynamoDB tables.

#### CampusSupportTickets

This table stores:

- Ticket ID.
- Requester name.
- Email address.
- Issue category.
- Priority.
- Issue description.
- Status.
- Processing notes.
- Attachment information.
- Creation and update timestamps.

#### CampusSupportConnections

This table stores active WebSocket connections, including:

- `connectionId`
- User ID or email.
- Authorization group.
- Connection timestamp.

### 3.7 Amazon S3

Amazon S3 stores ticket attachments, including:

- PNG files.
- JPG files.
- WebP files.
- PDF documents.

The bucket is private.

Users do not access the bucket directly. Lambda generates **S3 Presigned URLs** that allow file upload or download for a limited period.

### 3.8 Amazon SES

Amazon SES is used to send:

- Confirmation emails after ticket creation.
- Alert emails to the IT support team.
- Notifications when ticket status changes.
- Notifications when an administrator adds processing notes.

SES currently operates in the Sandbox environment, so sender and recipient addresses must be verified.

### 3.9 Amazon CloudWatch

Amazon CloudWatch stores logs and supports monitoring for:

- AWS Lambda.
- API Gateway.
- DynamoDB Streams.
- WebSocket API.

CloudWatch helps inspect errors, execution duration, failed requests, and system events.

### 3.10 AWS IAM

AWS IAM provides permissions to the Lambda functions.

Each Lambda function receives only the permissions it requires, such as:

- Reading and writing DynamoDB data.
- Uploading and downloading files from S3.
- Sending emails through SES.
- Sending messages through the WebSocket Management API.
- Writing logs to CloudWatch.

This permission model follows the **principle of least privilege**.

---

## 4. User Authentication Flow

The authentication process operates as follows:

1. The user accesses the frontend hosted on AWS Amplify.
2. The user selects the sign-in or registration function.
3. The browser is redirected to Amazon Cognito Hosted UI.
4. Cognito authenticates the account.
5. After successful authentication, Cognito redirects the user back to the frontend.
6. The frontend receives JWT tokens.
7. The tokens are stored for the authenticated session.
8. The frontend includes the token in requests sent to API Gateway.
9. The JWT Authorizer validates the token.
10. Valid requests are forwarded to Lambda.

If a token is invalid or expired, API Gateway rejects the request before the Lambda function is invoked.

---

## 5. Ticket Creation Flow

The ticket creation process operates as follows:

1. The user enters issue information through the frontend.
2. When an attachment is selected, the frontend requests an upload URL from the backend.
3. API Gateway validates the JWT token.
4. CampusSupportTicketService generates an Amazon S3 presigned URL.
5. The frontend uploads the file directly to S3 using the presigned URL.
6. The frontend sends the ticket information and attachment metadata to the HTTP API.
7. API Gateway forwards the request to CampusSupportTicketService.
8. Lambda validates the data and user permissions.
9. The ticket is stored in the CampusSupportTickets table.
10. The API returns a ticket ID to the frontend.
11. DynamoDB Streams publishes an `INSERT` event.
12. CampusSupportNotificationService sends a confirmation email.
13. The notification Lambda publishes an event through the WebSocket API.
14. User and Admin interfaces update without requiring a page reload.

---

## 6. Ticket Update Flow

The ticket update process operates as follows:

1. An administrator signs in using an account in the Admins group.
2. The administrator selects a ticket.
3. The administrator updates the ticket status or processing notes.
4. The frontend sends a `PATCH` request to API Gateway.
5. The JWT Authorizer validates the token.
6. Lambda performs an additional Cognito Group check.
7. If the authenticated account belongs to the Admins group, Lambda updates the ticket in DynamoDB.
8. DynamoDB Streams publishes a `MODIFY` event.
9. CampusSupportNotificationService compares the old and new ticket data.
10. A notification email is sent to the ticket requester.
11. A WebSocket event is sent to connected browsers.
12. The interface updates in real time.

---

## 7. Real-Time Notification Flow

The browser establishes a connection to the WebSocket API at the `production` stage.

The connection process is as follows:

1. The frontend sends a Cognito token during the `$connect` process.
2. CampusSupportWebSocketService validates the token.
3. When the token is valid, the `connectionId` is stored in CampusSupportConnections.
4. When a ticket is created or updated, the notification Lambda reads the active connection records.
5. Lambda sends an event through the WebSocket Management API.
6. The frontend receives the event and updates the interface.
7. When the user closes the page or loses the connection, the `$disconnect` event is triggered.
8. Invalid connection records are removed from DynamoDB.

---

## 8. Security Architecture

The system applies multiple security layers:

- HTTPS protects data transmitted between browsers and AWS services.
- Amazon Cognito authenticates users.
- The JWT Authorizer protects HTTP API routes.
- Cognito Groups distinguish User and Admin permissions.
- Lambda validates authorization before performing administrative operations.
- The S3 bucket remains private.
- Presigned URLs remain valid only for a limited period.
- IAM roles follow the principle of least privilege.
- CloudWatch logs support troubleshooting and incident investigation.

---

## 9. Serverless Architecture Characteristics

The serverless architecture provides several benefits:

- No backend servers need to be configured or maintained.
- AWS services can scale automatically according to request volume.
- Costs are based primarily on actual usage.
- Authentication, storage, email, and WebSocket services can be integrated easily.
- Operational workloads are reduced.
- The architecture is suitable for a campus IT support system.
- The system can be expanded in the future.

The next section presents the AWS services used in the project in greater detail.