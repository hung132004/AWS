---
title: "Đề xuất dự án"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Campus IT Support Ticket Portal
## Hệ thống helpdesk serverless trên AWS cho hỗ trợ IT trong trường học

---

### 1. Tổng quan dự án

Campus IT Support Ticket Portal là hệ thống helpdesk serverless dành cho môi trường trường học. Hệ thống hỗ trợ sinh viên và nhân viên gửi yêu cầu hỗ trợ IT, theo dõi lịch sử và trạng thái xử lý ticket, nhận thông báo khi ticket được tạo hoặc cập nhật. Đồng thời, hệ thống cung cấp giao diện quản trị để đội ngũ IT tiếp nhận, phân loại, cập nhật, ghi chú xử lý và xóa ticket khi cần.

Frontend được triển khai công khai bằng **AWS Amplify Hosting** và kết nối với GitHub để tự động build/deploy khi có thay đổi mã nguồn. Người dùng đăng ký và đăng nhập thông qua **Amazon Cognito Hosted UI**. Backend được xây dựng bằng **Amazon API Gateway**, **AWS Lambda**, **Amazon DynamoDB**, **Amazon S3**, **Amazon SES**, **Amazon CloudWatch** và **AWS IAM**.

Dự án không chỉ dừng ở chức năng CRUD ticket. Hệ thống còn hỗ trợ file đính kèm bằng S3 Presigned URL, gửi email bất đồng bộ bằng Amazon SES, và cập nhật giao diện theo thời gian thực thông qua DynamoDB Streams kết hợp WebSocket API.

---

### 2. Vấn đề cần giải quyết

Trong môi trường trường học, yêu cầu hỗ trợ IT thường được gửi qua nhiều kênh khác nhau như tin nhắn, email, điện thoại hoặc báo trực tiếp. Cách làm này dễ gây ra các vấn đề:

- Yêu cầu hỗ trợ bị thất lạc, trùng lặp hoặc không có lịch sử xử lý rõ ràng.
- Người dùng khó biết ticket của mình đang ở trạng thái nào.
- Bộ phận IT thiếu một hàng đợi tập trung để phân loại và ưu tiên sự cố.
- File minh chứng như ảnh lỗi hoặc tài liệu liên quan thường bị gửi rời rạc.
- Admin khó theo dõi tổng số ticket, ticket đang xử lý, ticket ưu tiên cao và ticket đã giải quyết.

Campus IT Support Ticket Portal giải quyết các vấn đề trên bằng một hệ thống tập trung gồm hai nhóm người dùng:

- **Users:** đăng ký/đăng nhập, gửi ticket, upload file đính kèm, tra cứu ticket, xem lịch sử yêu cầu và nhận thông báo.
- **Admins:** xem dashboard, tìm kiếm/lọc ticket, xem chi tiết, cập nhật trạng thái, thêm ghi chú xử lý, xóa ticket và nhận cảnh báo khi có ticket High/Critical.

---

### 3. Kiến trúc giải pháp

#### Sơ đồ kiến trúc tổng quan

{{< project-image
src="images/5-Workshop/5.2-System-Architecture/Architecture.jpg"
alt="Sơ đồ kiến trúc Campus IT Support Ticket Portal"
caption="Hình 2.1: Kiến trúc tổng quan của Campus IT Support Ticket Portal."
>}}

#### Mô tả kiến trúc

Người dùng và quản trị viên truy cập frontend được host trên **AWS Amplify Hosting**. Khi cần đăng nhập, trình duyệt được chuyển tới **Amazon Cognito Hosted UI**. Sau khi xác thực thành công, Cognito cấp JWT token cho frontend.

Frontend gửi JWT token trong request đến **Amazon API Gateway HTTP API**. API Gateway sử dụng **JWT Authorizer** để xác thực token trước khi chuyển request đến **CampusSupportTicketService Lambda**. Lambda xử lý nghiệp vụ ticket, kiểm tra quyền User/Admin, lưu dữ liệu vào **DynamoDB CampusSupportTickets** và tạo **S3 Presigned URL** để upload hoặc tải file đính kèm trong bucket riêng tư.

Khi ticket được tạo hoặc cập nhật, **DynamoDB Streams** kích hoạt **CampusSupportNotificationService**. Lambda này gửi email bằng **Amazon SES** và phát sự kiện realtime qua **API Gateway WebSocket API**. Thông tin kết nối WebSocket được quản lý bởi **CampusSupportWebSocketService** và lưu trong bảng **DynamoDB CampusSupportConnections**.

---

### 4. Các dịch vụ AWS sử dụng

| Dịch vụ | Vai trò trong hệ thống |
| --- | --- |
| **AWS Amplify Hosting** | Host frontend và tự động build/deploy từ GitHub |
| **Amazon Cognito Hosted UI** | Quản lý đăng ký, đăng nhập, đăng xuất và phiên người dùng |
| **Cognito Groups** | Phân quyền tài khoản theo nhóm `Users` và `Admins` |
| **API Gateway HTTP API** | Cung cấp endpoint cho các thao tác tạo, đọc, cập nhật và xóa ticket |
| **API Gateway JWT Authorizer** | Xác thực JWT token từ Cognito trước khi cho phép gọi API |
| **API Gateway WebSocket API** | Gửi cập nhật thời gian thực đến trình duyệt User/Admin |
| **AWS Lambda** | Xử lý nghiệp vụ ticket, thông báo, WebSocket và kiểm tra quyền truy cập |
| **Amazon DynamoDB** | Lưu dữ liệu ticket và thông tin kết nối WebSocket |
| **DynamoDB Streams** | Phát hiện sự kiện ticket được tạo hoặc cập nhật để kích hoạt thông báo |
| **Amazon S3** | Lưu file đính kèm trong bucket riêng tư |
| **S3 Presigned URL** | Cho phép upload/tải file trong thời gian giới hạn mà không public bucket |
| **Amazon SES** | Gửi email xác nhận, cảnh báo ticket ưu tiên cao và thông báo đổi trạng thái |
| **Amazon CloudWatch** | Lưu log Lambda/API và hỗ trợ debug, theo dõi lỗi |
| **AWS IAM** | Cấp quyền least privilege giữa Lambda và các dịch vụ AWS khác |

---

### 5. Chức năng chính

#### Chức năng phía người dùng

- Đăng ký, đăng nhập và đăng xuất bằng Amazon Cognito.
- Gửi yêu cầu hỗ trợ theo nhóm WiFi, tài khoản, phần mềm hoặc thiết bị.
- Chọn mức độ ưu tiên và nhập mô tả sự cố.
- Đính kèm file PDF, PNG, JPG hoặc WebP.
- Nhận mã ticket sau khi gửi.
- Tra cứu ticket bằng mã.
- Xem lịch sử yêu cầu đã gửi.
- Nhận email xác nhận và cập nhật trạng thái theo thời gian thực.

#### Chức năng phía quản trị viên

- Xem dashboard tổng số ticket, ticket đang xử lý, ticket ưu tiên cao và ticket đã giải quyết.
- Tìm kiếm và lọc ticket theo trạng thái, mức ưu tiên hoặc nhóm sự cố.
- Xem chi tiết ticket và file đính kèm.
- Cập nhật trạng thái và ghi chú xử lý.
- Xóa ticket khỏi hệ thống trong phạm vi demo.
- Nhận email cảnh báo khi có ticket High hoặc Critical.
- Danh sách ticket tự cập nhật khi có thay đổi mà không cần reload.

---

### 6. API đã triển khai

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.3-Amazon-API-Gateway/routes.png"
alt="Các route API Gateway đã triển khai"
caption="Hình 2.2: Các route API Gateway dùng cho chức năng quản lý ticket."
>}}

Các route đều được bảo vệ bằng JWT. Các thao tác quản trị được Lambda kiểm tra thêm Cognito Group trước khi xử lý.

---

### 7. Mô hình dữ liệu chính

#### Bảng CampusSupportTickets

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.5-Amazon-DynamoDB/ticket-table-overview.png"
alt="Bảng DynamoDB CampusSupportTickets"
caption="Hình 2.3: Tổng quan bảng DynamoDB lưu dữ liệu ticket."
>}}

#### Bảng CampusSupportConnections

Bảng này lưu các `connectionId` WebSocket đang hoạt động để Notification Lambda có thể gửi sự kiện cập nhật đến đúng trình duyệt đang kết nối.

---

### 8. Kế hoạch kiểm thử

| Test case | Kết quả mong đợi |
| --- | --- |
| User đăng ký và đăng nhập | Cognito xác thực thành công và tài khoản thuộc nhóm Users |
| User gửi ticket hợp lệ | Ticket được lưu vào DynamoDB và trả về mã ticket |
| User upload file đính kèm | File được upload lên S3 qua Presigned URL |
| User tra cứu ticket | Hệ thống trả về đúng thông tin ticket |
| Admin xem dashboard | Danh sách và số liệu ticket hiển thị đúng |
| Admin cập nhật trạng thái | DynamoDB được cập nhật và phát sinh sự kiện MODIFY |
| Admin xóa ticket | Ticket được xóa khỏi DynamoDB |
| Ticket được tạo | SES gửi email xác nhận cho địa chỉ đã xác minh |
| Ticket High/Critical được tạo | SES gửi email cảnh báo cho đội IT |
| Ticket thay đổi | WebSocket gửi sự kiện để giao diện cập nhật không cần reload |
| Request thiếu JWT | API Gateway từ chối request |
| User thường gọi API admin | Lambda từ chối thao tác |
| Backend phát sinh lỗi | CloudWatch Logs ghi nhận lỗi để debug |

---

### 9. Ước tính chi phí

| Dịch vụ | Chi phí ước tính/tháng | Ghi chú |
| --- | --- | --- |
| AWS Amplify Hosting | ~$0-2 | Frontend traffic nhỏ |
| Amazon Cognito | ~$0 | Phù hợp demo users trong free tier |
| API Gateway HTTP/WebSocket API | ~$0-2 | Phụ thuộc số request và kết nối realtime |
| AWS Lambda | ~$0-1 | Chạy theo request/event |
| Amazon DynamoDB | ~$0-2 | Dữ liệu ticket nhỏ, dùng on-demand |
| Amazon S3 | ~$0-1 | File đính kèm dung lượng nhỏ |
| Amazon SES | ~$0-1 | Lượng email demo thấp |
| Amazon CloudWatch | ~$0-1 | Log cơ bản cho Lambda/API |
| **Tổng cộng** | **~$0-10/tháng** | Phụ thuộc traffic, dung lượng file và số lượng email |

---

### 10. Rủi ro và giới hạn

| Rủi ro/Giới hạn | Ảnh hưởng | Cách xử lý |
| --- | --- | --- |
| SES còn ở Sandbox | Chỉ gửi email đến địa chỉ đã xác minh | Request production access nếu triển khai thật |
| Cognito group cấu hình sai | User/Admin có thể sai quyền | Kiểm tra group claim trong Lambda |
| IAM role quá rộng | Tăng rủi ro bảo mật | Áp dụng least privilege |
| S3 bucket public nhầm | File đính kèm có thể bị lộ | Giữ bucket private và dùng Presigned URL |
| CORS cấu hình sai | Frontend không gọi được API | Cấu hình CORS theo domain Amplify |
| WebSocket connection hết hạn | Giao diện không nhận realtime update | Xóa connectionId lỗi và reconnect khi cần |
| Quên cleanup tài nguyên | Phát sinh chi phí | Theo dõi Billing Dashboard và ghi chú cleanup |

---

### 11. Kết quả mong đợi

Dự án hướng đến một hệ thống helpdesk serverless hoàn chỉnh ở mức demo/portfolio junior cloud project với các kết quả:

- Frontend được deploy công khai bằng AWS Amplify Hosting.
- Có xác thực và phân quyền User/Admin bằng Amazon Cognito.
- API được bảo vệ bằng JWT Authorizer.
- Lambda xử lý nghiệp vụ ticket và kiểm tra quyền.
- DynamoDB lưu ticket và WebSocket connection.
- S3 lưu file đính kèm riêng tư bằng Presigned URL.
- SES gửi email xác nhận và thông báo.
- WebSocket hỗ trợ cập nhật giao diện theo thời gian thực.
- CloudWatch hỗ trợ quan sát lỗi và debug.
- IAM áp dụng quyền tối thiểu cần thiết cho các Lambda function.

Giá trị chính của dự án là mô phỏng được quy trình tiếp nhận và xử lý yêu cầu IT trong môi trường trường học bằng kiến trúc serverless thực tế trên AWS.