---
title: "Practicing Core AWS Services: EC2, S3, VPC, and Databases"
date: 2026-07-02
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

After becoming more familiar with my AWS account and the console, I moved on to practicing core AWS services. This was the stage where AWS started to feel less like a list of separate services and more like a set of building blocks that could be connected into a real system. The services I focused on most were EC2, S3, VPC, security groups, IAM, and databases such as RDS/Aurora.

I started with EC2 because it helped me picture the idea of compute in the cloud most clearly. When launching an instance, I had to choose an AMI, instance type, key pair, network, and security group. At first, these looked like simple configuration steps, but after practicing more, I understood that each choice affects how the instance works. The AMI defines the operating system, the instance type defines the compute resources, and the security group decides what traffic the instance can receive.

One lesson I learned from EC2 is that creating cloud resources is fast, but managing them carefully is the real responsibility. After testing, I needed to check whether the instance was still running, whether it had a public IP, and whether the security group had ports opened too broadly. These small checks helped me build the habit of reviewing resources after each lab session.

Next, I practiced Amazon S3. At first, I thought S3 was just a place to upload files. After working with it more carefully, I saw that S3 is also about data organization and access control. I practiced creating buckets, uploading objects, checking object keys, enabling or disabling public access, and seeing how bucket policies or IAM permissions affect access.

S3 helped me understand an important rule: data should not be public unless there is a clear reason. In my Ticket Portal project, an attachment could be an error screenshot or a document submitted by a user. Those files should not be available to everyone. A better approach is to store the files in S3 while the application controls access through backend logic and IAM roles.

VPC was much harder for me than EC2 and S3. Concepts such as subnets, route tables, internet gateways, and security groups were easy to mix up at first. I had to read the material more than once and practice step by step to understand how traffic moves. When a resource could not connect, I could not just check one place. I had to look at the subnet, route table, security group, and where the resource was placed in the network.

Practicing VPC helped me understand why network design affects security. Not every resource should be exposed to the internet. If a database only serves the backend, it should be protected in an appropriate network scope instead of being made public unnecessarily. Even though my final project used many serverless services, VPC knowledge still helped me understand how AWS organizes networking and how to think about system design in real scenarios.

I also practiced Amazon RDS and Aurora to understand relational databases on AWS. Compared with manually installing a database on a server, RDS reduces many operational tasks. However, that does not mean users can ignore configuration. I still had to think about the database engine, instance size, backup, networking, and security. This helped me understand that a managed service reduces repetitive operations, but it does not replace design thinking.

When comparing RDS with DynamoDB, I started to understand that database choice depends on how the application accesses data. RDS is suitable for relational data, SQL queries, and operations that need joins. DynamoDB is more suitable for clear access patterns, high scalability, and serverless applications. For a ticket system, operations such as creating tickets, listing tickets, updating status, and deleting tickets are predictable, so DynamoDB became a reasonable choice for my final project.

During this stage, I also continued practicing with AWS Study Group workshops. The most useful part was creating resources myself, configuring them, testing them, making mistakes, and fixing them. Some mistakes were simple, such as using the wrong region, missing a security group rule, or lacking an IAM permission, but those mistakes made the services much easier to understand. If I had only read documentation, I do not think I would have remembered the details as well.

After practicing these core services, I had a clearer view of the layers in a cloud system. EC2 helped me understand compute, S3 helped me understand storage, VPC helped me understand networking, RDS/Aurora helped me understand relational databases, and IAM and Billing reminded me that security and cost always go together with deployment.

This stage gave me a stronger foundation for learning serverless. Once I understood traditional compute, storage, networking, and databases, it became easier to imagine how API Gateway, Lambda, Cognito, DynamoDB, S3, and CloudWatch could work together as a complete application.

Published blog post link: [AWS Study Group Facebook](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2219703182127975/)

## References

- [Amazon EC2 User Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
- [What is Amazon S3?](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
- [What is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [Amazon Aurora User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html)