---
title: "Store Ticket Data with DynamoDB"
date: 2026-07-21
weight: 7
chapter: false
pre: "<b>5.7 </b>"
---

Amazon DynamoDB is used to store ticket data and WebSocket connection information.

#### Implementation steps

1. Create the `CampusSupportTickets` table for ticket data.
2. Design attributes such as `ticketId`, `userId`, `email`, `category`, `priority`, `status`, `adminNote`, `createdAt`, and `updatedAt`.
3. Lambda writes ticket data to DynamoDB when users submit tickets.
4. Admins read, update, or delete tickets through the API.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.5-Amazon-DynamoDB/ticket-table-overview.png"
alt="DynamoDB ticket table"
caption="Figure 5.7.1: DynamoDB table used to store ticket data."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.5-Amazon-DynamoDB/ticket-items.png"
alt="DynamoDB ticket items"
caption="Figure 5.7.2: Sample ticket records stored in DynamoDB."
>}}