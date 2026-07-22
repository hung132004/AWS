---
title: "Cấu hình xác thực với Amazon Cognito"
date: 2026-07-21
weight: 5
chapter: false
pre: "<b>5.5 </b>"
---

Amazon Cognito được sử dụng để quản lý đăng ký, đăng nhập, JWT token và phân quyền giữa người dùng thường với quản trị viên.

#### Nội dung triển khai

1. Tạo Cognito User Pool.
2. Cấu hình App Client và Hosted UI.
3. Tạo group `Users` và `Admins`.
4. Kiểm tra đăng nhập và JWT token ở frontend.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.2-Amazon-Cognito/user-pool-overview.png"
alt="Cognito User Pool"
caption="Hình 5.5.1: Tổng quan Cognito User Pool dùng cho hệ thống."
>}}