---
title: "Tạo HTTP API Routes"
date: 2026-07-21
weight: 1
chapter: false
pre: "<b>5.6.1 </b>"
---

Tôi tạo các route API phục vụ chức năng quản lý ticket.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.3-Amazon-API-Gateway/routes.png"
alt="API Gateway routes"
caption="Hình 5.6.1.1: Các route API Gateway đã triển khai."
>}}

#### Các route chính

- `POST /tickets`: tạo ticket mới.
- `GET /tickets`: lấy danh sách ticket.
- `GET /tickets/{ticketId}`: tra cứu một ticket.
- `PATCH /tickets/{ticketId}`: cập nhật trạng thái và ghi chú.
- `DELETE /tickets/{ticketId}`: xóa ticket.