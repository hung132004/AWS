---
title: "Xây dựng backend API với API Gateway và Lambda"
date: 2026-07-21
weight: 6
chapter: false
pre: "<b>5.6 </b>"
---

Backend của hệ thống sử dụng **Amazon API Gateway** để nhận request từ frontend và **AWS Lambda** để xử lý nghiệp vụ ticket.

#### Nội dung triển khai

1. Tạo HTTP API routes cho chức năng ticket.
2. Cấu hình JWT Authorizer để bảo vệ API.
3. Kết nối API Gateway với Lambda backend.
4. Kiểm tra request từ frontend đến backend.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.3-Amazon-API-Gateway/api-overview.png"
alt="API Gateway overview"
caption="Hình 5.6.1: API Gateway dùng làm lớp API trung gian."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.4-AWS-Lambda/lambda-functions.png"
alt="AWS Lambda functions"
caption="Hình 5.6.2: Các Lambda function dùng cho backend."
>}}