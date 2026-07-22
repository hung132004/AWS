---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

#### Tổng quan project

Workshop này ghi lại quá trình triển khai **Campus IT Support Ticket Portal**, một hệ thống web helpdesk serverless dùng để tiếp nhận và quản lý yêu cầu hỗ trợ kỹ thuật trong môi trường trường học.

**Website đã triển khai:** [https://main.d37atxjbyyp60m.amplifyapp.com/](https://main.d37atxjbyyp60m.amplifyapp.com/)

Hệ thống sau khi triển khai cho phép người dùng đăng ký, đăng nhập, gửi ticket hỗ trợ, upload file đính kèm, theo dõi lịch sử ticket và nhận cập nhật trạng thái. Quản trị viên có thể xem toàn bộ ticket, tìm kiếm và lọc yêu cầu, cập nhật trạng thái, thêm ghi chú xử lý, xóa ticket và nhận cảnh báo khi có ticket ưu tiên cao.

Frontend được triển khai công khai bằng **AWS Amplify Hosting** và được kết nối với GitHub để tự động build/deploy khi có thay đổi mã nguồn.

#### Kiến trúc

Hệ thống sử dụng kiến trúc serverless trên AWS. Frontend tích hợp với **Amazon Cognito** để xác thực người dùng và gửi các request đã xác thực đến **Amazon API Gateway**. API Gateway kiểm tra Cognito JWT token trước khi chuyển request đến các hàm **AWS Lambda**.

Lambda xử lý nghiệp vụ ticket, kiểm tra quyền truy cập, xử lý tệp đính kèm và tích hợp với **Amazon DynamoDB** cùng **Amazon S3**. Hệ thống cũng sử dụng **Amazon SES**, **Amazon CloudWatch**, **AWS IAM** và các thành phần cập nhật thời gian thực như DynamoDB Streams và WebSocket API.

{{< project-image
src="images/5-Workshop/5.2-System-Architecture/architecture.jpg"
alt="Kiến trúc Campus IT Support Ticket Portal"
caption="Kiến trúc Campus IT Support Ticket Portal"
>}}

#### Các dịch vụ AWS sử dụng

| Dịch vụ | Vai trò trong workshop |
| --- | --- |
| AWS Amplify Hosting | Host frontend và tự động deploy thay đổi từ GitHub |
| Amazon Cognito | Xử lý đăng ký, đăng nhập, đăng xuất, JWT token và group `Users`/`Admins` |
| Amazon API Gateway | Cung cấp HTTP API và WebSocket API để frontend giao tiếp với backend |
| AWS Lambda | Xử lý nghiệp vụ ticket, kiểm tra quyền, thông báo và sự kiện WebSocket |
| Amazon DynamoDB | Lưu dữ liệu ticket và thông tin kết nối WebSocket |
| Amazon S3 | Lưu file đính kèm của ticket trong bucket riêng tư |
| Amazon SES | Gửi email xác nhận ticket, cảnh báo và thông báo thay đổi trạng thái |
| Amazon CloudWatch | Lưu log Lambda/API và hỗ trợ debug, giám sát hệ thống |
| AWS IAM | Cấp quyền least privilege giữa Lambda và các dịch vụ AWS khác |

#### Nội dung triển khai

1. [Tổng quan dự án](5.1-project-overview/)
2. [Tổng quan kiến trúc](5.2-system-architecture/)
3. [Điều kiện chuẩn bị](5.3-prerequisites/)
4. [Triển khai frontend với AWS Amplify](5.4-deploy-frontend-with-aws-amplify/)
5. [Cấu hình xác thực với Amazon Cognito](5.5-configure-authentication-with-amazon-cognito/)
6. [Xây dựng backend API với API Gateway và Lambda](5.6-build-backend-api-with-api-gateway-and-lambda/)
7. [Lưu dữ liệu ticket với DynamoDB](5.7-store-ticket-data-with-dynamodb/)
8. [Lưu file đính kèm với Amazon S3](5.8-store-attachments-with-amazon-s3/)
9. [Cấu hình thông báo và giám sát](5.9-configure-notification-and-monitoring/)
10. [Bảo mật và IAM permissions](5.10-security-and-iam-permissions/)
11. [Kiểm thử hệ thống](5.11-testing-the-system/)
12. [Ảnh chụp hệ thống và kết quả](5.12-system-screenshots-and-result/)
13. [Kiểm tra tài nguyên và chi phí](5.13-cleanup/)