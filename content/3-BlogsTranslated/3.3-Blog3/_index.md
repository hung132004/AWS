---
title: "Learning Serverless, Authentication, Monitoring, and Security on AWS"
date: 2026-07-03
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

After practicing core AWS services, I moved into serverless tasks for my Campus IT Support Ticket Portal project. This was the stage where I learned the most, because the services were no longer separate pieces. They had to connect into one complete flow: the frontend calls an API, the API validates a token, the backend processes the logic, data is stored in a database, files are stored in object storage, and errors are checked through logs.

The first service I worked with was AWS Lambda. At first, I needed some time to change the way I thought about backend applications. With a traditional server, the backend usually runs continuously. With Lambda, a function runs only when there is a request or an event. This model fits features such as creating a ticket, updating ticket status, listing tickets, or processing attachment information.

While writing Lambda logic, I realized that a function should not try to do too many things at once. A function is easier to control when the flow is clear: receive the request, validate the input, process the business logic, call DynamoDB or S3 if needed, and return a response. If too much logic is mixed together, debugging becomes difficult, especially when the only useful clue is in CloudWatch Logs.

API Gateway was the next part I practiced. It is the layer where the frontend communicates with backend logic. I created routes for the main system features, such as submitting a ticket, listing tickets, updating status, and deleting a ticket. When configuring the API, I had to pay attention to HTTP methods, CORS, and how each route invokes Lambda. At one point, the frontend could not call the API because of a CORS issue, and that helped me understand that a working backend endpoint is not always ready for browser-based frontend calls.

Authentication took more time than I expected. I used Amazon Cognito to manage sign-up, sign-in, and user/admin separation. At first, the JWT token flow was hard to picture because it goes through several steps: the user signs in, Cognito returns a token, the frontend stores and sends the token when calling the API, and API Gateway uses a JWT Authorizer to validate the request before passing it to Lambda.

After I understood that flow, Cognito made the project structure clearer. A normal user only needs to submit tickets and view their own tickets. An admin needs broader access to list tickets, update status, add handling notes, or delete tickets. This helped me distinguish authentication from authorization more clearly. Authentication answers “who is this user?”, while authorization answers “what is this user allowed to do?”.

For ticket data, I used DynamoDB. Unlike RDS, DynamoDB made me think first about how the application would query data. In the Ticket Portal, the main operations include creating a ticket, getting tickets for a user, allowing admins to list tickets, updating status, and deleting tickets. Once these access patterns were clear, designing the table items and keys became easier to reason about.

S3 was used for attachment storage. I did not want to store files directly inside the database because that would make ticket records heavy and harder to manage. A better approach is to store the file in S3 and keep only metadata, such as the file name or object key, in DynamoDB. This keeps the ticket data cleaner while still allowing the system to connect each ticket with its attachment.

Monitoring felt very practical while working on the project. When the backend failed, guessing was not useful. CloudWatch Logs helped me check whether Lambda was invoked, whether the request body was correct, and whether the error came from input validation, IAM permissions, DynamoDB, or S3. One issue I faced was not in the main code but in the Lambda role permissions, and I only found it after reading the logs.

Security was another part I had to review several times. I checked the Lambda IAM role, access to DynamoDB, permissions for the S3 bucket, CORS settings, and which routes required a token. For a student project, it may not be production-level, but I still wanted the permission structure to make sense: users should not perform admin actions, buckets should not be public without reason, and backend functions should not use overly broad permissions.

A small but important task near the end was cleanup and Billing checking. After creating or testing resources, I reviewed what was still active. This helped prevent unnecessary cost and also helped me understand which resources truly belonged to the project.

The main lesson I took from this stage is that serverless does not mean the system is automatically simple. It reduces server management, but it still requires understanding the responsibility of each service. API Gateway is the API entry point, Lambda handles logic, Cognito manages identity, DynamoDB stores data, S3 stores files, CloudWatch helps observe errors, and IAM controls permissions.

After connecting these parts together, I understood more clearly how a cloud application works end to end. This also helped me write the workshop more clearly, because each deployment step had a reason behind it: deploy the frontend, configure authentication, create APIs, write backend logic, store data, test user/admin flows, read logs, and clean up resources.

Published blog post link: [AWS Study Group Facebook](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2219706598794300/)

## References

- [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [Amazon API Gateway REST API documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-rest-api.html)
- [Amazon Cognito Developer Guide](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)
- [What is Amazon DynamoDB?](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
- [Sending Lambda logs to CloudWatch Logs](https://docs.aws.amazon.com/lambda/latest/dg/monitoring-cloudwatchlogs.html)