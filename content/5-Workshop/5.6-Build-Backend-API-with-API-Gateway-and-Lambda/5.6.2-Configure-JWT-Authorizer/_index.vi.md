---
title: "Cấu hình JWT Authorizer"
date: 2026-07-21
weight: 2
chapter: false
pre: "<b>5.6.2 </b>"
---

JWT Authorizer được cấu hình để API Gateway chỉ chấp nhận request hợp lệ từ người dùng đã đăng nhập qua Cognito.

#### Các bước thực hiện

1. Tạo JWT Authorizer trong API Gateway.
2. Khai báo issuer từ Cognito User Pool.
3. Gắn authorizer vào các route cần bảo vệ.
4. Kiểm tra request không có token và request có token hợp lệ.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.3-Amazon-API-Gateway/jwt-authorizer.png"
alt="JWT Authorizer"
caption="Hình 5.6.2.1: JWT Authorizer dùng để xác thực request API."
>}}