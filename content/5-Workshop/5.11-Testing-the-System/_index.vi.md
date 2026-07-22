---
title: "Kiểm thử hệ thống"
date: 2026-07-21
weight: 11
chapter: false
pre: "<b>5.11 </b>"
---

Sau khi triển khai các dịch vụ, tôi kiểm thử hệ thống theo hai luồng chính: người dùng gửi ticket và quản trị viên xử lý ticket.

#### Các bước kiểm thử

1. Truy cập website đã deploy trên Amplify.
2. Đăng ký hoặc đăng nhập bằng Cognito.
3. Gửi ticket mới kèm nhóm sự cố, mức ưu tiên và mô tả lỗi.
4. Kiểm tra ticket được lưu trong DynamoDB.
5. Upload file đính kèm và kiểm tra object trong S3.
6. Đăng nhập tài khoản Admin để xem, lọc, cập nhật và xóa ticket.
7. Kiểm tra CloudWatch Logs khi các API được gọi.

{{< project-image
src="images/5-Workshop/5.1-Project-Overview/user-homepage.png"
alt="User testing"
caption="Hình 5.11.1: Kiểm thử luồng người dùng gửi và theo dõi ticket."
>}}

{{< project-image
src="images/5-Workshop/5.1-Project-Overview/admin-dashboard.png"
alt="Admin testing"
caption="Hình 5.11.2: Kiểm thử dashboard quản trị viên."
>}}