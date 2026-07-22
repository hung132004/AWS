---
title: "Configure JWT Authorizer"
date: 2026-07-21
weight: 2
chapter: false
pre: "<b>5.6.2 </b>"
---

JWT Authorizer is configured so API Gateway only accepts valid requests from users authenticated through Cognito.

#### Implementation steps

1. Create a JWT Authorizer in API Gateway.
2. Configure issuer information from Cognito User Pool.
3. Attach the authorizer to protected routes.
4. Test requests with and without a valid token.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.3-Amazon-API-Gateway/jwt-authorizer.png"
alt="JWT Authorizer"
caption="Figure 5.6.2.1: JWT Authorizer used to authenticate API requests."
>}}