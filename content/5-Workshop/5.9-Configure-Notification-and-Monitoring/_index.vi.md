---
title: "Cấu hình thông báo và giám sát"
date: 2026-07-21
weight: 9
chapter: false
pre: "<b>5.9 </b>"
---

Hệ thống sử dụng **Amazon SES** để gửi email thông báo và **Amazon CloudWatch** để theo dõi log, lỗi và hoạt động của backend.

#### Nội dung triển khai

1. Cấu hình SES identity để gửi email kiểm thử.
2. Lambda gửi email khi ticket được tạo hoặc cập nhật.
3. CloudWatch Logs ghi lại request, lỗi và kết quả xử lý của Lambda.
4. Kiểm tra log khi frontend gọi API.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.7-Amazon-SES/ses-dashboard.png"
alt="Amazon SES"
caption="Hình 5.9.1: Amazon SES dùng cho chức năng gửi email."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.8-Amazon-CloudWatch/cloudwatch-dashboard.png"
alt="Amazon CloudWatch"
caption="Hình 5.9.2: CloudWatch dùng để giám sát log và hoạt động backend."
>}}