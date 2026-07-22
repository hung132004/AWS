---
title: "Kiến trúc hệ thống"
date: 2026-07-21
weight: 2
chapter: false
pre: "<b>5.2 </b>"
---

# Kiến trúc hệ thống

## 1. Tổng quan kiến trúc

**Campus IT Support Ticket Portal** được xây dựng theo kiến trúc serverless trên nền tảng Amazon Web Services.

Kiến trúc này không yêu cầu vận hành máy chủ backend truyền thống. Các chức năng như xác thực người dùng, xử lý API, lưu ticket, lưu tệp đính kèm, gửi email và cập nhật thời gian thực được triển khai bằng các dịch vụ AWS được quản lý.

Frontend của hệ thống được triển khai trên **AWS Amplify Hosting**. Người dùng đăng ký và đăng nhập thông qua **Amazon Cognito Hosted UI**. Sau khi xác thực thành công, Cognito cấp JWT token cho frontend.

Frontend gửi JWT token trong các request tới **Amazon API Gateway**. API Gateway sử dụng JWT Authorizer để xác thực người dùng trước khi chuyển request đến các hàm **AWS Lambda**.

Lambda thực hiện logic nghiệp vụ, thao tác với **Amazon DynamoDB** để lưu dữ liệu ticket và sử dụng **Amazon S3** để lưu tệp đính kèm.

Hệ thống sử dụng **DynamoDB Streams**, Lambda thông báo, **Amazon SES** và **API Gateway WebSocket API** để gửi email và cập nhật dữ liệu theo thời gian thực.

---

## 2. Sơ đồ kiến trúc tổng thể

Sơ đồ sau thể hiện các thành phần chính và luồng trao đổi dữ liệu trong hệ thống.

{{< project-image
src="images/5-Workshop/5.2-System-Architecture/Architecture.jpg"
alt="Sơ đồ kiến trúc Campus IT Support Ticket Portal"
caption="Hình 5.2.1: Kiến trúc tổng thể của Campus IT Support Ticket Portal."
>}}
---

## 3. Các thành phần chính

### 3.1 Người dùng và quản trị viên

Hệ thống phục vụ hai nhóm người dùng:

- **User:** sinh viên hoặc nhân viên gửi yêu cầu hỗ trợ IT và theo dõi trạng thái xử lý.
- **Admin:** thành viên đội ngũ IT tiếp nhận, phân loại, cập nhật và xóa ticket.

Cả hai nhóm truy cập hệ thống qua trình duyệt bằng kết nối HTTPS.

### 3.2 AWS Amplify Hosting

AWS Amplify Hosting được sử dụng để lưu trữ và phân phối frontend của hệ thống.

Amplify được kết nối với GitHub và tự động thực hiện quy trình build, deploy mỗi khi mã nguồn được push lên repository.

Frontend bao gồm các thành phần được xây dựng bằng Hugo, HTML, CSS và JavaScript.

### 3.3 Amazon Cognito

Amazon Cognito cung cấp chức năng:

- Đăng ký tài khoản.
- Đăng nhập.
- Đăng xuất.
- Quản lý phiên người dùng.
- Phân quyền bằng Cognito Groups.
- Cấp JWT token cho frontend.

Hệ thống sử dụng hai nhóm chính:

- `Users`
- `Admins`

JWT token chứa thông tin người dùng và nhóm quyền, được frontend gửi tới API Gateway trong mỗi request cần xác thực.

### 3.4 Amazon API Gateway

Amazon API Gateway cung cấp hai loại API:

- **HTTP API:** xử lý các thao tác tạo, đọc, cập nhật và xóa ticket.
- **WebSocket API:** duy trì kết nối thời gian thực giữa trình duyệt và backend.

HTTP API sử dụng JWT Authorizer để kiểm tra token do Amazon Cognito phát hành.

Sau khi token hợp lệ, request được chuyển đến Lambda tương ứng.

### 3.5 AWS Lambda

Hệ thống sử dụng nhiều Lambda function để phân tách trách nhiệm:

#### CampusSupportTicketService

Lambda này xử lý:

- Tạo ticket.
- Lấy danh sách ticket.
- Tra cứu ticket.
- Cập nhật trạng thái.
- Cập nhật ghi chú.
- Xóa ticket.
- Kiểm tra quyền User hoặc Admin.
- Tạo presigned URL để upload và tải tệp.

#### CampusSupportNotificationService

Lambda này được kích hoạt từ DynamoDB Streams để:

- Gửi email xác nhận khi ticket được tạo.
- Gửi cảnh báo khi có ticket High hoặc Critical.
- Gửi email khi trạng thái hoặc ghi chú thay đổi.
- Phát sự kiện cập nhật qua WebSocket API.

#### CampusSupportWebSocketService

Lambda này xử lý:

- Sự kiện `$connect`.
- Sự kiện `$disconnect`.
- Xác thực Cognito token khi thiết lập kết nối.
- Lưu và xóa `connectionId`.

### 3.6 Amazon DynamoDB

Hệ thống sử dụng hai bảng DynamoDB chính.

#### CampusSupportTickets

Bảng này lưu:

- Mã ticket.
- Họ tên người gửi.
- Email.
- Nhóm sự cố.
- Mức độ ưu tiên.
- Mô tả sự cố.
- Trạng thái.
- Ghi chú xử lý.
- Thông tin tệp đính kèm.
- Thời gian tạo và cập nhật.

#### CampusSupportConnections

Bảng này lưu các kết nối WebSocket đang hoạt động, bao gồm:

- `connectionId`
- User ID hoặc email.
- Nhóm quyền.
- Thời gian kết nối.

### 3.7 Amazon S3

Amazon S3 được sử dụng để lưu tệp đính kèm của ticket, bao gồm:

- PNG.
- JPG.
- WebP.
- PDF.

Bucket được cấu hình ở chế độ riêng tư.

Người dùng không truy cập trực tiếp vào bucket. Lambda tạo **S3 Presigned URL** để cho phép upload hoặc tải tệp trong một khoảng thời gian giới hạn.

### 3.8 Amazon SES

Amazon SES được sử dụng để gửi:

- Email xác nhận khi tạo ticket.
- Email cảnh báo cho đội ngũ IT.
- Email thông báo khi trạng thái ticket thay đổi.
- Email thông báo khi quản trị viên thêm ghi chú xử lý.

SES hiện hoạt động trong môi trường Sandbox, do đó địa chỉ gửi và nhận cần được xác minh.

### 3.9 Amazon CloudWatch

Amazon CloudWatch lưu log và hỗ trợ theo dõi hoạt động của:

- AWS Lambda.
- API Gateway.
- DynamoDB Streams.
- WebSocket API.

CloudWatch giúp kiểm tra lỗi, thời gian thực thi, request thất bại và các sự kiện phát sinh trong hệ thống.

### 3.10 AWS IAM

AWS IAM được sử dụng để cấp quyền cho các Lambda function.

Mỗi Lambda chỉ được cấp các quyền cần thiết, ví dụ:

- Đọc và ghi DynamoDB.
- Upload và tải tệp từ S3.
- Gửi email bằng SES.
- Gửi dữ liệu qua WebSocket Management API.
- Ghi log vào CloudWatch.

Cách phân quyền này áp dụng nguyên tắc **Least Privilege** nhằm hạn chế quyền truy cập không cần thiết.

---

## 4. Luồng xác thực người dùng

Luồng đăng nhập hoạt động như sau:

1. Người dùng truy cập frontend trên AWS Amplify Hosting.
2. Người dùng chọn đăng nhập hoặc đăng ký.
3. Trình duyệt được chuyển tới Amazon Cognito Hosted UI.
4. Cognito xác thực tài khoản.
5. Sau khi đăng nhập thành công, Cognito chuyển người dùng trở lại frontend.
6. Frontend nhận JWT token.
7. Token được lưu trong phiên đăng nhập.
8. Frontend gửi token trong header của các request tới API Gateway.
9. JWT Authorizer kiểm tra token.
10. Request hợp lệ được chuyển tới Lambda.

Nếu token không hợp lệ hoặc đã hết hạn, API Gateway từ chối request trước khi Lambda được gọi.

---

## 5. Luồng tạo ticket

Quá trình tạo ticket diễn ra như sau:

1. Người dùng nhập thông tin sự cố trên frontend.
2. Nếu có tệp đính kèm, frontend yêu cầu URL upload từ backend.
3. API Gateway xác thực JWT token.
4. CampusSupportTicketService tạo presigned URL cho Amazon S3.
5. Frontend upload tệp trực tiếp lên S3 bằng presigned URL.
6. Frontend gửi thông tin ticket và metadata của tệp tới HTTP API.
7. API Gateway chuyển request tới CampusSupportTicketService.
8. Lambda kiểm tra dữ liệu và quyền người dùng.
9. Ticket được lưu vào bảng CampusSupportTickets.
10. API trả mã ticket cho frontend.
11. DynamoDB Streams phát sự kiện `INSERT`.
12. CampusSupportNotificationService gửi email xác nhận.
13. Notification Lambda gửi sự kiện qua WebSocket API.
14. Giao diện User và Admin được cập nhật mà không cần tải lại trang.

---

## 6. Luồng cập nhật ticket

Quá trình cập nhật ticket diễn ra như sau:

1. Quản trị viên đăng nhập bằng tài khoản thuộc nhóm Admins.
2. Admin chọn ticket cần xử lý.
3. Admin cập nhật trạng thái hoặc ghi chú.
4. Frontend gửi request `PATCH` tới API Gateway.
5. JWT Authorizer kiểm tra token.
6. Lambda kiểm tra thêm Cognito Group.
7. Nếu người dùng thuộc nhóm Admins, Lambda cập nhật ticket trong DynamoDB.
8. DynamoDB Streams phát sự kiện `MODIFY`.
9. CampusSupportNotificationService so sánh dữ liệu trước và sau khi cập nhật.
10. Email thông báo được gửi cho người tạo ticket.
11. Sự kiện WebSocket được gửi tới các trình duyệt đang kết nối.
12. Giao diện được cập nhật theo thời gian thực.

---

## 7. Luồng thông báo thời gian thực

Trình duyệt thiết lập kết nối với WebSocket API tại stage `production`.

Khi kết nối:

1. Frontend gửi Cognito token trong quá trình `$connect`.
2. CampusSupportWebSocketService xác thực token.
3. Nếu token hợp lệ, `connectionId` được lưu trong bảng CampusSupportConnections.
4. Khi ticket được tạo hoặc cập nhật, Notification Lambda đọc danh sách connection đang hoạt động.
5. Lambda gửi sự kiện thông qua WebSocket Management API.
6. Frontend nhận sự kiện và cập nhật giao diện.
7. Khi người dùng đóng trang hoặc mất kết nối, `$disconnect` được kích hoạt.
8. `connectionId` không còn hợp lệ được xóa khỏi DynamoDB.

---

## 8. Kiến trúc bảo mật

Hệ thống sử dụng nhiều lớp bảo mật:

- HTTPS bảo vệ dữ liệu truyền giữa trình duyệt và các dịch vụ AWS.
- Amazon Cognito xác thực người dùng.
- JWT Authorizer bảo vệ các HTTP API.
- Cognito Groups phân biệt quyền User và Admin.
- Lambda kiểm tra quyền trước khi thực hiện thao tác quản trị.
- S3 bucket được đặt ở chế độ private.
- Presigned URL chỉ có hiệu lực trong thời gian giới hạn.
- IAM Role áp dụng nguyên tắc Least Privilege.
- CloudWatch lưu log để hỗ trợ phát hiện và kiểm tra lỗi.

---

## 9. Đặc điểm serverless

Kiến trúc serverless mang lại các lợi ích:

- Không cần cấu hình hoặc duy trì máy chủ backend.
- AWS tự động mở rộng theo số lượng request.
- Chỉ phát sinh chi phí dựa trên mức sử dụng.
- Dễ tích hợp xác thực, lưu trữ, email và WebSocket.
- Giảm khối lượng công việc vận hành.
- Phù hợp với hệ thống hỗ trợ IT quy mô trường học.
- Dễ mở rộng trong tương lai.

Phần tiếp theo sẽ trình bày chi tiết các dịch vụ AWS được sử dụng trong dự án.