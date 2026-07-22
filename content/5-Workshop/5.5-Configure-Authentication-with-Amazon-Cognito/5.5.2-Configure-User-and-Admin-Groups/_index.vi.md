---
title: "Cấu hình User và Admin Groups"
date: 2026-07-21
weight: 2
chapter: false
pre: "<b>5.5.2 </b>"
---

Hệ thống sử dụng Cognito Groups để phân quyền giữa người dùng thường và quản trị viên.

#### Các bước thực hiện

1. Tạo group `Users` cho người dùng gửi ticket.
2. Tạo group `Admins` cho đội ngũ IT quản lý ticket.
3. Gán tài khoản test vào group phù hợp.
4. Lambda backend đọc thông tin group từ JWT để kiểm tra quyền.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.2-Amazon-Cognito/user-groups.png"
alt="Cognito User Groups"
caption="Hình 5.5.2.1: Groups Users và Admins dùng để phân quyền."
>}}