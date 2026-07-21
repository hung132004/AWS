---
title: "Blog 2"
date: 2024-01-01
chapter: false
---

# Practicing AWS core services: EC2, S3, VPC, and databases

After becoming more familiar with the AWS account and the console interface, I moved on to practicing core services. This was the stage where I began to see that AWS was no longer just a list of separate services, but a set of building blocks that could be combined to create a system. The services I focused on most were EC2, S3, VPC, Security Groups, IAM, and databases such as RDS and Aurora.

I started with EC2 because it is the service that best helps visualize the concept of compute in the cloud. When creating an instance, I had to choose an AMI, instance type, key pair, network, and security group. At first, these choices seemed like just configuration steps, but after practicing more, I understood that each choice affects how the instance works. The AMI determines the operating system, the instance type determines the resources, and the security group determines which traffic is allowed to reach the instance.

One thing I learned from EC2 is that creating resources is very fast, but managing them properly is the part that requires caution. After testing, I had to check whether the instance was still running, whether it had a public IP, and whether the security group was opening too many ports. These are small steps, but they helped me build the habit of reviewing resources after each practice session.

Next, I studied Amazon S3. At first, I thought S3 was just a place to upload files, but after working with it more, I realized that S3 is closely related to how data is organized and how permissions are managed. I practiced creating buckets, uploading objects, checking object keys, enabling or disabling public access, and observing how bucket policies or IAM permissions affected access.

The S3 part helped me understand an important principle: data should not be made public unless it is truly necessary. In the Ticket Portal project, attachment files for tickets could include screenshots or documents uploaded by users. These files should not be accessible to everyone. A more appropriate approach is to store them in S3 while controlling access through the backend and IAM roles.

VPC was the part I found more difficult than EC2 or S3. Concepts such as subnets, route tables, internet gateways, and security groups were initially easy to confuse. I had to read the material several times and follow each step carefully to understand how traffic flows. When a resource could not connect, I could not just look at one place; I had to check the subnet, route table, security group, and the way the resource was placed in the network.

Thanks to VPC practice, I understood more clearly why network design affects security. Not every resource should be exposed to the internet. If a database only serves the backend, it should be protected within an appropriate scope rather than being made public unnecessarily. Although my final project used many serverless services, VPC knowledge still helped me understand how AWS organizes the networking environment and how to think when designing real systems.

I also practiced with Amazon RDS and Aurora to understand relational databases on AWS. Compared to installing a database on a server manually, RDS reduces a lot of operational work, but that does not mean users no longer need to pay attention to configuration. I still had to consider the database engine, instance size, backups, networking, and security. This helped me understand that managed services do not replace design thinking; they reduce repetitive operations.

When comparing RDS with DynamoDB, I began to understand more clearly that the choice of database should depend on how the application accesses data. RDS is suitable for relational data, SQL queries, and operations that require joins. DynamoDB is better suited for clear access patterns, high speed, and serverless models. For the ticket system, operations such as creating tickets, listing them, updating status, and deleting tickets are quite clear, so DynamoDB was a reasonable choice for the final project.

During this phase, I also continued working through workshops with the AWS Study Group. The most useful part was being able to create resources, configure them, test them, and then fix errors. Some errors were very simple, such as choosing the wrong region, missing a security group rule, or an IAM role lacking permissions, but those mistakes helped me understand the services much more deeply. If I had only read the documentation, I believe I would not have remembered it as well.

After practicing core services, I had a clearer view of the layers in a cloud system. EC2 helped me understand compute, S3 helped me understand storage, VPC helped me understand networking, and RDS/Aurora helped me understand relational databases. IAM and Billing reminded me that security and cost are always part of the deployment process.

This stage laid a solid foundation for moving into serverless development. Once I understood traditional compute, storage, networking, and databases, it became much easier to see why services such as API Gateway, Lambda, Cognito, DynamoDB, S3, and CloudWatch can be combined into a complete application.

### References
- Amazon EC2 User Guide: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html
- What is Amazon S3?: https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html
- What is Amazon VPC?: https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
- Amazon RDS User Guide: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html
- Amazon Aurora User Guide: https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html

