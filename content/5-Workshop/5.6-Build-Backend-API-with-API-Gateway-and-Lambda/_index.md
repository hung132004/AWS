---
title: "Build Backend API with API Gateway and Lambda"
date: 2026-07-21
weight: 6
chapter: false
pre: "<b>5.6 </b>"
---

The backend uses **Amazon API Gateway** to receive requests from the frontend and **AWS Lambda** to process ticket logic.

#### Implementation content

1. Create HTTP API routes for ticket features.
2. Configure JWT Authorizer to protect APIs.
3. Connect API Gateway with backend Lambda.
4. Test requests from frontend to backend.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.3-Amazon-API-Gateway/api-overview.png"
alt="API Gateway overview"
caption="Figure 5.6.1: API Gateway used as the API layer."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.4-AWS-Lambda/lambda-functions.png"
alt="AWS Lambda functions"
caption="Figure 5.6.2: Lambda functions used by the backend."
>}}