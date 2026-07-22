---
title: "Connect API Gateway to Lambda"
date: 2026-07-21
weight: 3
chapter: false
pre: "<b>5.6.3 </b>"
---

API Gateway is integrated with Lambda so valid requests can be forwarded to the backend for processing.

#### Implementation steps

1. Create Lambda integration for API Gateway.
2. Attach the integration to ticket routes.
3. Verify that Lambda receives events from API Gateway.
4. Monitor Lambda logs when the frontend calls the API.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.3-Amazon-API-Gateway/lambda-integration.png"
alt="Lambda integration"
caption="Figure 5.6.3.1: API Gateway route integrated with Lambda."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.4-AWS-Lambda/lambda-code.png"
alt="Lambda code"
caption="Figure 5.6.3.2: Lambda function processing backend ticket logic."
>}}