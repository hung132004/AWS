---
title: "Testing the System"
date: 2026-07-21
weight: 11
chapter: false
pre: "<b>5.11 </b>"
---

After deploying the services, I tested the system through two main flows: user ticket submission and administrator ticket processing.

#### Testing steps

1. Open the deployed website on Amplify.
2. Register or sign in through Cognito.
3. Submit a new ticket with category, priority, and issue description.
4. Verify that the ticket is stored in DynamoDB.
5. Upload an attachment and verify the object in S3.
6. Sign in as Admin to view, filter, update, and delete tickets.
7. Check CloudWatch Logs when APIs are called.

{{< project-image
src="images/5-Workshop/5.1-Project-Overview/user-homepage.png"
alt="User testing"
caption="Figure 5.11.1: Testing the user ticket submission flow."
>}}

{{< project-image
src="images/5-Workshop/5.1-Project-Overview/admin-dashboard.png"
alt="Admin testing"
caption="Figure 5.11.2: Testing the administrator dashboard."
>}}