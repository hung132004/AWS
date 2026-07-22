---
title: "Create HTTP API Routes"
date: 2026-07-21
weight: 1
chapter: false
pre: "<b>5.6.1 </b>"
---

I created API routes for ticket-management functions.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.3-Amazon-API-Gateway/routes.png"
alt="API Gateway routes"
caption="Figure 5.6.1.1: Implemented API Gateway routes."
>}}

#### Main routes

- `POST /tickets`: create a new ticket.
- `GET /tickets`: get ticket list.
- `GET /tickets/{ticketId}`: look up one ticket.
- `PATCH /tickets/{ticketId}`: update status and notes.
- `DELETE /tickets/{ticketId}`: delete a ticket.