---
title: "Deploy Frontend with AWS Amplify"
date: 2026-07-21
weight: 4
chapter: false
pre: "<b>5.4 </b>"
---

The system frontend is deployed with **AWS Amplify Hosting**. Amplify is connected to GitHub so the frontend can be built and deployed automatically whenever the source code changes.

#### Implementation steps

1. Open AWS Amplify Console and create a new application.
2. Connect Amplify to the project GitHub repository.
3. Select the main branch for deployment.
4. Review build settings and start deployment.
5. After deployment succeeds, open the default Amplify domain to validate the website.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.1-AWS-Amplify-Hosting/amplify-hosting.png"
alt="AWS Amplify Hosting"
caption="Figure 5.4.1: Frontend application configured on AWS Amplify Hosting."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.1-AWS-Amplify-Hosting/deployment-success.png"
alt="Amplify deployment success"
caption="Figure 5.4.2: Amplify build and frontend deployment completed successfully."
>}}

#### Result

The website is publicly available at: [https://main.d37atxjbyyp60m.amplifyapp.com/](https://main.d37atxjbyyp60m.amplifyapp.com/)