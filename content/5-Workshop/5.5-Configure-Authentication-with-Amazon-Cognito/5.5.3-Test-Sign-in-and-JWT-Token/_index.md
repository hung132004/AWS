---
title: "Test Sign-in and JWT Token"
date: 2026-07-21
weight: 3
chapter: false
pre: "<b>5.5.3 </b>"
---

After configuring Cognito, I tested the sign-in flow through Hosted UI and confirmed that the frontend could receive a JWT token.

#### Implementation steps

1. Configure the App Client for the frontend.
2. Validate Hosted UI and callback URL settings.
3. Sign in using a test account.
4. Send API requests with the JWT token to API Gateway.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.2-Amazon-Cognito/app-client.png"
alt="Cognito App Client"
caption="Figure 5.5.3.1: App Client used to connect the frontend with Cognito."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.2-Amazon-Cognito/hosted-ui.png"
alt="Cognito Hosted UI"
caption="Figure 5.5.3.2: Hosted UI used for sign-in testing."
>}}