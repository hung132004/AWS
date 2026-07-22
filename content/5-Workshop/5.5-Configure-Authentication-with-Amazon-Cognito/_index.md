---
title: "Configure Authentication with Amazon Cognito"
date: 2026-07-21
weight: 5
chapter: false
pre: "<b>5.5 </b>"
---

Amazon Cognito is used to manage registration, sign-in, JWT tokens, and authorization between normal users and administrators.

#### Implementation content

1. Create a Cognito User Pool.
2. Configure App Client and Hosted UI.
3. Create `Users` and `Admins` groups.
4. Test sign-in and JWT token usage in the frontend.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.2-Amazon-Cognito/user-pool-overview.png"
alt="Cognito User Pool"
caption="Figure 5.5.1: Cognito User Pool overview used by the system."
>}}