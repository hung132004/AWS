---
title: "Lưu dữ liệu ticket với DynamoDB"
date: 2026-07-21
weight: 7
chapter: false
pre: "<b>5.7 </b>"
---

Amazon DynamoDB được sử dụng để lưu dữ liệu ticket và thông tin kết nối WebSocket của hệ thống.

#### Các bước thực hiện

1. Tạo bảng `CampusSupportTickets` để lưu ticket.
2. Thiết kế các thuộc tính như `ticketId`, `userId`, `email`, `category`, `priority`, `status`, `adminNote`, `createdAt` và `updatedAt`.
3. Lambda ghi dữ liệu vào DynamoDB khi người dùng tạo ticket.
4. Admin đọc, cập nhật hoặc xóa ticket thông qua API.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.5-Amazon-DynamoDB/ticket-table-overview.png"
alt="DynamoDB ticket table"
caption="Hình 5.7.1: Bảng DynamoDB dùng để lưu dữ liệu ticket."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.5-Amazon-DynamoDB/ticket-items.png"
alt="DynamoDB ticket items"
caption="Hình 5.7.2: Dữ liệu ticket mẫu được lưu trong DynamoDB."
>}}