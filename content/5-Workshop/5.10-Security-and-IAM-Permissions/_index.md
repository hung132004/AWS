---
title: "Security and IAM Permissions"
date: 2026-07-21
weight: 10
chapter: false
pre: "<b>5.10 </b>"
---

AWS IAM is used to grant Lambda access to required services such as DynamoDB, S3, SES, and CloudWatch.

#### Implementation steps

1. Create IAM Role for Lambda.
2. Grant permissions to access DynamoDB tables.
3. Grant permissions to read/write attachment files in S3.
4. Grant permissions to write logs to CloudWatch.
5. Keep permissions aligned with the least-privilege principle.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.9-AWS-IAM/iam-roles.png"
alt="IAM Roles"
caption="Figure 5.10.1: IAM Role used by backend Lambda."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.9-AWS-IAM/iam-dashboard.png"
alt="IAM Dashboard"
caption="Figure 5.10.2: IAM manages access permissions between AWS services."
>}}