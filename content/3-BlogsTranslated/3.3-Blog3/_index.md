---
title: "Blog 3"
date: 2024-01-01
chapter: false
---

# Learning Serverless, Authentication, Monitoring, and Security on AWS

After practicing the core AWS services, I began moving toward the serverless part to support the Campus IT Support Ticket Portal project. This was the stage where I learned the most, because the services were no longer isolated; they had to work together as a complete flow: the frontend called an API, the API validated the token, the backend handled the logic, data was stored in a database, files were stored in storage, and errors were monitored through logs.

The first service I became familiar with was AWS Lambda. At first, I needed some time to change my way of thinking. In traditional server-based architecture, the backend usually runs continuously. With Lambda, a function only runs when a request or event occurs. This is very suitable for actions such as creating a ticket, updating ticket status, retrieving a list of tickets, or processing attachment files.

When writing logic for Lambda, I realized that a function should not handle too many tasks. A more manageable function has a clear flow: it receives a request, validates the input, performs the business logic, calls DynamoDB or S3 if needed, and then returns a response. If too much logic is mixed together, debugging becomes much harder, especially when issues only appear in CloudWatch Logs.

API Gateway was the next service I practiced. This is where the frontend communicates with the backend. I created routes for functions such as sending tickets, getting the ticket list, updating status, or deleting tickets. While configuring the API, I had to pay attention to HTTP methods, CORS, and how routes invoke Lambda. On one occasion, the frontend called the API but ran into a CORS error, which helped me understand that even if the frontend works, the API must also be ready for browser-based access.

Authentication took much more time than I expected. I used Amazon Cognito to manage sign-up, sign-in, and user/admin permissions. At first, JWT tokens were difficult to visualize because they involve multiple steps: the user signs in, Cognito returns a token, the frontend stores it and sends it when calling the API, and API Gateway uses a JWT Authorizer to validate the token before allowing the request to proceed.

After understanding that flow, I saw that Cognito makes the project much clearer. Regular users mainly need to create tickets and view their own tickets. Admins need broader permissions to view the ticket list, update status, add handling notes, or delete tickets. This helped me distinguish more clearly between authentication and authorization. Authentication answers the question “who is the user?”, while authorization answers “what is this user allowed to do?”.

For ticket data, I used DynamoDB. Unlike RDS, DynamoDB forced me to think ahead about how the application would query the data. In the Ticket Portal project, the main operations are creating tickets, retrieving tickets by user, allowing admins to view the list, updating status, and deleting tickets. Once these access patterns were clear, designing the item structure and keys in DynamoDB became much easier.

S3 was used for attachment files. I did not want to store files directly in the database because that would make ticket data heavy and harder to manage. A better approach was to store the files in S3 while keeping DynamoDB records focused on metadata such as the file name or object key. That way, the ticket data remained lightweight while the system still knew which file belonged to which ticket.

Monitoring was a very practical part of the project. When the backend failed, it was nearly impossible to debug without checking the logs. CloudWatch Logs helped me verify whether Lambda was being invoked, whether the request body was correct, and whether the error came from input validation, IAM permissions, DynamoDB, or S3. One time, the issue was not in the main code but in the Lambda role permissions, and I only discovered it after reading the logs.

Security also required multiple rounds of review. I checked the IAM role of Lambda, access permissions for DynamoDB and the S3 bucket, CORS settings, and which routes required tokens. Although the project was student-level rather than production-level, I still wanted the system to have a reasonable permission structure: users should not be able to perform admin actions, the bucket should not be public by accident, and the backend should not use overly broad permissions.

One small but important practice at the end of the process was cleanup and checking Billing. After creating or testing resources, I reviewed what was still running. This helped avoid unnecessary costs and also showed me which resources were truly part of the project.

The main lesson I learned from this stage is that serverless does not mean simpler thinking. It removes the need to manage servers, but it requires a clear understanding of how each service is responsible for a specific part of the system. API Gateway acts as the API entry point, Lambda handles the logic, Cognito manages identity, DynamoDB stores data, S3 stores files, CloudWatch supports observability, and IAM enforces permissions.

After connecting these pieces together, I better understood how a cloud application works end-to-end. This stage also helped me write workshops more clearly, because each deployment step had a specific reason instead of being performed only as a tutorial exercise: deploy the frontend, configure sign-in, create the API, write the backend, store data, test user/admin flows, inspect logs, and clean up resources.

### References
- AWS Lambda Developer Guide: https://docs.aws.amazon.com/lambda/latest/dg/welcome.html
- Amazon API Gateway REST API documentation: https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-rest-api.html
- Amazon Cognito Developer Guide: https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html
- What is Amazon DynamoDB?: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html
- Sending Lambda logs to CloudWatch Logs: https://docs.aws.amazon.com/lambda/latest/dg/monitoring-cloudwatchlogs.html

