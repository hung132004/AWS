---
title: "Learning AWS from Account Setup, IAM, and Cost Control"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

When I first started learning AWS, I thought the hardest part would be deploying a system on the cloud. After the first few practice sessions, I realized that the first things I needed to do well were much more basic: setting up the account correctly, knowing which region I was using, checking where billing information was shown, and avoiding overly broad permissions.

My first step was signing in to the AWS Management Console and getting used to the interface. At the beginning, the console felt confusing because there were many services, and each service had its own dashboard and terminology. I tried searching for services such as EC2, S3, IAM, Billing, and CloudWatch until I became more familiar with where they were located. One small habit that helped me later was checking the region in the top-right corner before creating resources. There were times when I could not find a resource, and the reason was simply that I was looking in the wrong region.

After getting used to the console, I started paying more attention to the Billing Dashboard. I think this is something every student learning AWS should check regularly. In a local environment, a wrong configuration usually costs time. In the cloud, creating resources and forgetting to remove them can create real charges. Because of that, I built a habit of checking Billing, Free Tier usage, and the list of resources I created after each practice session.

During the learning process, I noticed that some services can generate cost easily if they are not managed carefully, such as EC2 instances, NAT Gateways, Load Balancers, Route 53 domains, or long-term stored data. I did not use all of these services in my final project, but knowing about them early made me more careful when following workshops or documentation. For me, cost control became part of learning cloud responsibly, not just an extra administrative task.

The next topic I studied was IAM. At first, IAM felt a bit dry because many concepts sounded similar: users, groups, roles, and policies. It took me some time to understand that a user represents a person or identity, a group helps manage permissions for multiple users, a role is often used by AWS services, and a policy describes what actions are allowed. Once I understood these concepts, the principle of least privilege made much more sense.

While practicing, there were moments when I wanted to grant broad permissions just to make things work faster. However, when I connected this to my Ticket Portal project, I saw why that was not a good approach. For example, if a Lambda function only needs to read and write ticket data in DynamoDB, it should not have Administrator access. If Lambda only uploads attachments to one S3 bucket, its role should be limited to that bucket and the required actions. Learning IAM early helped me see security as part of the design, not something to add at the end.

I also practiced creating EC2 instances to understand traditional compute on AWS. When launching an instance, I had to choose an AMI, instance type, key pair, security group, and network settings. These steps helped me understand how a virtual server is configured in AWS. Even though my final project used more serverless services, EC2 was still worth learning because it gave me a foundation for comparing traditional compute with Lambda.

One small issue I faced while learning EC2 was an incorrect security group configuration, which prevented me from accessing the instance as expected. From that issue, I learned that creating a resource does not mean it is ready to use immediately. Network rules, ports, inbound traffic, and access permissions all affect the result. Small mistakes like this helped me remember the lesson better than only reading documentation.

Besides the foundation services, I also explored Amazon Bedrock briefly. I did not use Bedrock as a core service in my project, but it helped me see that AWS is not only about infrastructure such as servers, storage, and databases. AWS also provides higher-level managed services for modern application development and AI.

After this first stage, my main takeaway was that learning AWS should not start by rushing through many services at once. It is better to first understand how to use the account safely, check costs, understand IAM, and navigate the console. These tasks may sound simple, but skipping them can lead to confusing problems later when working on a bigger project.

For me, this stage became the foundation of the rest of the internship. After becoming more comfortable with the console, Billing, and IAM, I was more confident moving into core services such as EC2, S3, VPC, RDS, and later serverless services for the Campus IT Support Ticket Portal project.

Published blog post link: [AWS Study Group Facebook](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2219698898795070/)

## References

- [Getting started with AWS](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/getting-started-with-aws.html)
- [AWS Management Console](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html)
- [AWS Billing and Cost Management](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html)
- [Security best practices in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Amazon EC2 User Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)