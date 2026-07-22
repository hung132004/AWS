---
title: "Configure User and Admin Groups"
date: 2026-07-21
weight: 2
chapter: false
pre: "<b>5.5.2 </b>"
---

The system uses Cognito Groups to separate normal users and administrators.

#### Implementation steps

1. Create the `Users` group for ticket submitters.
2. Create the `Admins` group for IT administrators.
3. Assign test accounts to the correct group.
4. Backend Lambda reads group information from JWT claims for permission checks.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.2-Amazon-Cognito/user-groups.png"
alt="Cognito User Groups"
caption="Figure 5.5.2.1: Users and Admins groups for authorization."
>}}