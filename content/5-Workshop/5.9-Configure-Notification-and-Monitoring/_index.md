---
title: "Configure Notification and Monitoring"
date: 2026-07-21
weight: 9
chapter: false
pre: "<b>5.9 </b>"
---

The system uses **Amazon SES** for email notifications and **Amazon CloudWatch** for logs, error tracking, and backend monitoring.

#### Implementation content

1. Configure SES identity for test email sending.
2. Lambda sends emails when tickets are created or updated.
3. CloudWatch Logs records requests, errors, and Lambda processing results.
4. Validate logs when the frontend calls APIs.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.7-Amazon-SES/ses-dashboard.png"
alt="Amazon SES"
caption="Figure 5.9.1: Amazon SES used for email notification."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.8-Amazon-CloudWatch/cloudwatch-dashboard.png"
alt="Amazon CloudWatch"
caption="Figure 5.9.2: CloudWatch used for backend logs and monitoring."
>}}