---
title: "Blog 1"
date: 2024-01-01
chapter: false
---

# Learning AWS from account setup, IAM, and cost control

When I first started learning AWS, I thought the hardest part would be deploying a system successfully on the cloud. However, after a few early practice sessions, I realized that the first thing to do well is actually something very basic: creating an account correctly, understanding the region I am using, knowing where to check costs, and avoiding overly broad permissions for resources.

The first thing I did was log in to the AWS Management Console and get familiar with the interface. At first, I was quite confused because the console contains many services, and each service has its own dashboard and naming conventions. I had to try finding services such as EC2, S3, IAM, Billing, and CloudWatch to become familiar with their locations. One small habit that helped me avoid mistakes later was always checking the region in the top-right corner before creating any resource. There were times when I could not find a resource, and only later realized that I was viewing the wrong region.

After getting familiar with the console, I began paying more attention to the Billing Dashboard. This is something I believe students learning AWS should check regularly. When working locally, misconfigurations usually only waste time to fix. On the cloud, however, if resources are created and then forgotten, costs can accumulate quickly. Therefore, I developed the habit of checking Billing, Free Tier, and the list of resources I created after each practice session.

During the learning process, I noticed that some services are especially prone to generating fees if not managed carefully, such as EC2 instances, NAT Gateways, Load Balancers, Route 53 domains, or long-term storage. I have not used all of these in my final project, but knowing about them in advance helped me be more careful when following workshops or tutorials. To me, cost control is no longer a secondary concern; it is part of responsible cloud learning.

The next part I studied was IAM. At first, IAM felt dry because it contains many similar concepts: user, group, role, and policy. I spent time understanding the difference between a user (the identity of a person or application), a group (used to manage permissions for multiple users), a role (often used by services), and a policy (the document that defines what actions are allowed). Once I understood these concepts, I saw why AWS strongly emphasizes the principle of least privilege.

In practice, there were moments when I wanted to grant broad permissions to make things faster. However, when I connected this to the Ticket Portal project, I realized that this was not a good approach. For example, if a Lambda function only needs to read and write tickets in a DynamoDB table, it should not have full Administrator privileges. If the function only uploads attachment files to a specific S3 bucket, the role should be limited to that bucket. Learning IAM early helped me see security as part of design, not as a last-minute step at the end of the project.

I also practiced creating EC2 instances to understand traditional compute on AWS. When creating an instance, I had to choose the AMI, instance type, key pair, security group, and network. These steps helped me understand how a virtual server on AWS is configured. Although my final project used serverless services more heavily, EC2 remains an important topic because it provides the foundation for comparing it with Lambda.

One small mistake I encountered while learning EC2 was misconfiguring the security group, which prevented me from accessing the instance as expected. From that experience, I understood that creating a resource is not enough; network rules, ports, inbound traffic, and access permissions all directly affect the outcome of the practice. Mistakes like this helped me remember the lesson much better than simply reading documentation.

In addition to foundational services, I also briefly explored Amazon Bedrock. I did not use Bedrock as the main service in my project, but this helped me see that AWS is not only about infrastructure such as servers, storage, or databases. AWS also offers many managed services at a higher level that support modern applications and AI-driven use cases.

After this early stage, the main lesson I learned is that learning AWS should not begin by using too many services at once. First, we need to learn how to use an account safely, check costs, understand IAM, and operate confidently in the console. These things may seem simple, but if ignored, they can easily lead to hard-to-manage issues in larger projects.

To me, this stage is like building the foundation. Once I became comfortable with the console, learned to check Billing, and understood the basics of IAM, I felt much more confident moving on to core services such as EC2, S3, VPC, RDS, and then serverless services for the Campus IT Support Ticket Portal project.

### References
- https://docs.aws.amazon.com/whitepapers/latest/aws-overview/getting-started-with-aws.html
- https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html
- https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html

