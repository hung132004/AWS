---
title: "Kết nối API Gateway với Lambda"
date: 2026-07-21
weight: 3
chapter: false
pre: "<b>5.6.3 </b>"
---

API Gateway được tích hợp với Lambda để chuyển request hợp lệ đến backend xử lý.

#### Các bước thực hiện

1. Tạo Lambda integration cho API Gateway.
2. Gắn integration vào các route ticket.
3. Kiểm tra Lambda nhận event từ API Gateway.
4. Theo dõi log Lambda khi frontend gọi API.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.3-Amazon-API-Gateway/lambda-integration.png"
alt="Lambda integration"
caption="Hình 5.6.3.1: API Gateway route được tích hợp với Lambda."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.4-AWS-Lambda/lambda-code.png"
alt="Lambda code"
caption="Hình 5.6.3.2: Lambda xử lý logic backend của hệ thống ticket."
>}}