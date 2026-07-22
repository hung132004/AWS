---
title: "Kiểm tra đăng nhập và JWT Token"
date: 2026-07-21
weight: 3
chapter: false
pre: "<b>5.5.3 </b>"
---

Sau khi cấu hình Cognito, tôi kiểm tra luồng đăng nhập bằng Hosted UI và xác nhận frontend có thể nhận JWT token.

#### Các bước thực hiện

1. Cấu hình App Client cho frontend.
2. Kiểm tra Hosted UI và callback URL.
3. Đăng nhập bằng tài khoản test.
4. Gửi request API kèm JWT token đến API Gateway.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.2-Amazon-Cognito/app-client.png"
alt="Cognito App Client"
caption="Hình 5.5.3.1: App Client dùng để kết nối frontend với Cognito."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.2-Amazon-Cognito/hosted-ui.png"
alt="Cognito Hosted UI"
caption="Hình 5.5.3.2: Hosted UI dùng để kiểm tra đăng nhập."
>}}