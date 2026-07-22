---
title: "Sharing and Feedback"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

## Internship Reflection

The internship program provided me with valuable exposure to cloud computing technologies and modern software development practices. Before starting the project, I spent time understanding the AWS ecosystem, including cloud concepts, security principles, networking, storage, compute services, and deployment workflows. Step by step, I gained confidence in using AWS services and understanding how they cooperate to build a complete application.

My primary task during the internship was to design and implement the **Campus IT Support Ticket Portal**, a serverless web application that allows students and staff to submit IT support requests while providing administrators with tools to monitor and manage tickets efficiently. Instead of focusing only on programming, I also learned how to analyze requirements, design system architecture, configure cloud resources, and verify that each component worked correctly with the others.

The application was developed using a serverless architecture, which reduced infrastructure management and allowed each AWS service to perform a dedicated responsibility. The frontend was deployed using **AWS Amplify Hosting**, while user authentication and authorization were handled by **Amazon Cognito**. Client requests were processed through **Amazon API Gateway**, business logic was implemented with **AWS Lambda**, and application data was stored in **Amazon DynamoDB**. File attachments were uploaded to **Amazon S3**, email notifications were delivered through **Amazon SES**, and system monitoring was performed using **Amazon CloudWatch**. Security and service permissions were managed through **AWS IAM**.

Working with this architecture helped me understand that developing a cloud application requires much more than connecting services together. Every component must be configured correctly, secured with appropriate permissions, tested thoroughly, and monitored continuously to ensure reliability. I also realized the importance of designing a clear data flow before implementation because changes made to one service often affect several other components.

## Skills and Knowledge Acquired

Throughout the internship, I improved both my technical knowledge and practical development skills.

- Learned how to deploy and update static web applications using AWS Amplify Hosting.
- Understood user authentication, authorization, and JWT token validation with Amazon Cognito.
- Gained experience configuring HTTP APIs and integrating them with AWS Lambda through Amazon API Gateway.
- Implemented CRUD operations for ticket management using Lambda functions.
- Learned how DynamoDB stores NoSQL data efficiently and how to organize application records.
- Practiced uploading, retrieving, and managing files securely with Amazon S3.
- Implemented email notification workflows using Amazon SES.
- Used Amazon CloudWatch to monitor application logs, identify runtime errors, and troubleshoot backend services.
- Applied IAM roles and policies to control communication between AWS services while following security best practices.
- Improved GitHub version control, documentation writing with Hugo, and deployment management throughout the project.

## Challenges Encountered

Although the project architecture was well planned, several challenges appeared during implementation. One of the biggest difficulties was integrating multiple AWS services into a single workflow. Authentication, API Gateway, Lambda functions, DynamoDB, and S3 all depended on correct configurations, making troubleshooting more complex whenever one component failed.

Permission management was another challenge. Incorrect IAM policies occasionally prevented Lambda functions from accessing DynamoDB, S3, or SES. Solving these problems required careful review of execution roles, resource policies, and AWS documentation to identify missing permissions without granting unnecessary access.

Debugging serverless applications also required a different approach compared to traditional applications. Since there was no dedicated server, I relied heavily on CloudWatch Logs to trace requests, inspect Lambda execution results, verify API Gateway responses, and identify configuration issues. This experience significantly improved my ability to analyze distributed systems.

Another challenge involved maintaining project documentation. As the architecture evolved and new features were added, diagrams, workshop documentation, implementation guides, and weekly reports also needed continuous updates. Keeping all documents synchronized required careful planning and attention to detail.

## Personal Evaluation

Overall, I believe the internship greatly enhanced my understanding of cloud computing and serverless application development. The combination of self-study, practical implementation, and mentor guidance helped me strengthen both my technical foundation and my ability to solve real-world problems independently.

Beyond technical skills, I also improved several professional competencies, including time management, technical communication, documentation writing, and project organization. Learning to divide large tasks into smaller milestones made the development process more efficient and easier to manage.

The internship also showed me the importance of continuous learning. AWS provides a wide range of services, and each project introduces new technologies and best practices. This experience motivated me to continue exploring cloud-native development and improve my knowledge of scalable and secure application design.

## Future Improvements

If I continue developing this project, I would like to enhance several areas to make the system more practical and feature-rich.

- Develop a more comprehensive analytics dashboard with charts and reports.
- Improve the ticket filtering system by adding advanced search options and multiple conditions.
- Implement role-based activity logs to record administrator operations.
- Enhance notification features by supporting additional communication channels.
- Strengthen security through more detailed IAM policies and additional validation mechanisms.
- Optimize system performance and reduce operational costs by reviewing resource configurations and usage patterns.
- Expand the documentation with deployment guides, troubleshooting examples, and maintenance procedures.

## Final Thoughts

Completing this internship has been an important milestone in my learning journey. It allowed me to apply academic knowledge in a practical environment while gaining experience with cloud technologies that are widely used in industry. More importantly, I developed a better understanding of how modern applications are designed, deployed, secured, and maintained using AWS services.

The knowledge and experience gained throughout this internship have increased my confidence in building cloud-based applications and prepared me for future opportunities in software engineering and cloud computing. I sincerely appreciate the support and guidance provided by the mentors throughout the program, and I believe the lessons learned during this internship will continue to benefit my academic studies and professional career.