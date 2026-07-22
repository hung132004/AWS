---
title: "Bảo mật và IAM permissions"
date: 2026-07-21
weight: 10
chapter: false
pre: "<b>5.10 </b>"
---

AWS IAM được sử dụng để cấp quyền cho Lambda truy cập các dịch vụ cần thiết như DynamoDB, S3, SES và CloudWatch.

#### Các bước thực hiện

1. Tạo IAM Role cho Lambda.
2. Cấp quyền thao tác với bảng DynamoDB.
3. Cấp quyền đọc/ghi file trong S3 bucket đính kèm.
4. Cấp quyền ghi log vào CloudWatch.
5. Giữ quyền theo nguyên tắc least privilege.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.9-AWS-IAM/iam-roles.png"
alt="IAM Roles"
caption="Hình 5.10.1: IAM Role dùng cho Lambda backend."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.9-AWS-IAM/iam-dashboard.png"
alt="IAM Dashboard"
caption="Hình 5.10.2: IAM hỗ trợ quản lý quyền truy cập giữa các dịch vụ."
>}}