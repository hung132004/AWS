---
title: "Tổng quan dự án"
date: 2026-07-21
weight: 1
chapter: false
pre: "<b>5.1 </b>"
---

## Campus IT Support Ticket Portal

**Campus IT Support Ticket Portal** là hệ thống helpdesk serverless dành cho môi trường trường học. Hệ thống cho phép sinh viên và nhân viên gửi yêu cầu hỗ trợ kỹ thuật, theo dõi quá trình xử lý và nhận thông báo khi ticket được tạo hoặc cập nhật.

Hệ thống cũng cung cấp giao diện quản trị dành cho đội ngũ IT. Quản trị viên có thể tiếp nhận, tìm kiếm, phân loại, cập nhật trạng thái, thêm ghi chú xử lý và xóa ticket. Dữ liệu trên giao diện có thể được đồng bộ theo thời gian thực mà không cần tải lại trang.

Frontend của dự án được triển khai bằng **AWS Amplify Hosting** tại:

[Truy cập Campus IT Support Ticket Portal](https://main.d37atxjbyyp60m.amplifyapp.com)

---

## 1. Mục tiêu dự án

Dự án được xây dựng nhằm đạt được các mục tiêu sau:

- Cung cấp một kênh tập trung để sinh viên và nhân viên gửi yêu cầu hỗ trợ IT.
- Hỗ trợ các nhóm sự cố phổ biến như WiFi, tài khoản, phần mềm và thiết bị.
- Cho phép người dùng theo dõi lịch sử và trạng thái xử lý ticket.
- Cho phép đính kèm hình ảnh, tài liệu PDF và các tệp liên quan.
- Gửi email xác nhận khi ticket được tạo.
- Gửi thông báo khi trạng thái hoặc ghi chú của ticket thay đổi.
- Cập nhật dữ liệu theo thời gian thực bằng WebSocket.
- Cung cấp dashboard để quản trị viên theo dõi và xử lý ticket.
- Sử dụng kiến trúc serverless nhằm giảm nhu cầu quản lý máy chủ.
- Tự động build và triển khai frontend từ GitHub bằng AWS Amplify Hosting.

---

## 2. Đối tượng sử dụng

Hệ thống phục vụ hai nhóm người dùng chính.

### Người dùng

Người dùng có thể là sinh viên hoặc nhân viên trong trường. Các chức năng chính gồm:

- Đăng ký tài khoản.
- Đăng nhập và đăng xuất.
- Gửi yêu cầu hỗ trợ IT.
- Chọn nhóm sự cố và mức độ ưu tiên.
- Đính kèm tệp vào ticket.
- Nhận mã ticket sau khi gửi.
- Tra cứu ticket bằng mã.
- Xem lịch sử các yêu cầu đã gửi.
- Nhận email và cập nhật trạng thái theo thời gian thực.

### Quản trị viên

Quản trị viên là thành viên của đội ngũ hỗ trợ IT. Các chức năng chính gồm:

- Xem dashboard tổng quan.
- Xem toàn bộ danh sách ticket.
- Tìm kiếm và lọc ticket.
- Xem nội dung chi tiết và tệp đính kèm.
- Cập nhật trạng thái ticket.
- Thêm ghi chú xử lý.
- Xóa ticket.
- Nhận cảnh báo khi xuất hiện ticket có mức ưu tiên High hoặc Critical.

---

## 3. Công nghệ và dịch vụ chính

Dự án sử dụng các công nghệ và dịch vụ sau:

- **Hugo, HTML, CSS và JavaScript:** xây dựng giao diện frontend.
- **GitHub:** quản lý mã nguồn và lịch sử phiên bản.
- **AWS Amplify Hosting:** lưu trữ frontend và triển khai CI/CD.
- **Amazon Cognito:** đăng ký, đăng nhập, đăng xuất và phân quyền.
- **Amazon API Gateway:** cung cấp HTTP API và WebSocket API.
- **AWS Lambda:** xử lý nghiệp vụ ticket, thông báo và kết nối WebSocket.
- **Amazon DynamoDB:** lưu ticket và thông tin kết nối WebSocket.
- **Amazon S3:** lưu trữ tệp đính kèm trong bucket riêng tư.
- **Amazon SES:** gửi email xác nhận và thông báo.
- **Amazon CloudWatch:** lưu log và giám sát hệ thống.
- **AWS IAM:** quản lý vai trò và quyền truy cập giữa các dịch vụ.

---

## 4. Logo dự án

Logo sử dụng tên **Campus Support – Helpdesk Portal**, thể hiện mục đích xây dựng một cổng hỗ trợ kỹ thuật tập trung dành cho môi trường trường học.

{{< project-image
src="images/5-Workshop/5.1-Project-overview/project-logo.png"
alt="Logo Campus IT Support Ticket Portal"
caption="Hình 5.1.1: Logo của Campus IT Support Ticket Portal."
>}}

---

## 5. Giao diện khi chưa đăng nhập

Khi chưa đăng nhập, người dùng có thể xem thông tin giới thiệu của hệ thống và sử dụng các nút đăng nhập hoặc đăng ký.

Giao diện hiển thị biểu mẫu gửi yêu cầu hỗ trợ, khu vực nhập thông tin sự cố và các gợi ý giúp người dùng cung cấp đủ dữ liệu cho đội ngũ IT.

{{< project-image
src="images/5-Workshop/5.1-Project-overview/guest-homepage.png"
alt="Giao diện trang chủ khi chưa đăng nhập"
caption="Hình 5.1.2: Giao diện trang chủ khi người dùng chưa đăng nhập."
>}}

---

## 6. Giao diện người dùng sau khi đăng nhập

Sau khi đăng nhập thành công thông qua Amazon Cognito, thông tin tài khoản được hiển thị trên thanh điều hướng.

Một số trường trong biểu mẫu có thể được tự động điền dựa trên thông tin của người dùng đã xác thực. Người dùng có thể gửi ticket, xem các yêu cầu đã tạo và nhận cập nhật trạng thái mà không cần tải lại trang.

{{< project-image
src="images/5-Workshop/5.1-Project-overview/user-homepage.png"
alt="Giao diện người dùng sau khi đăng nhập"
caption="Hình 5.1.3: Giao diện người dùng sau khi đăng nhập thành công."
>}}

---

## 7. Giao diện quản trị viên

Trang quản trị cung cấp dashboard tổng quan về tình trạng của hệ thống, bao gồm:

- Tổng số ticket.
- Số ticket đang xử lý.
- Số ticket có mức ưu tiên cao.
- Số ticket đã được giải quyết.

Quản trị viên có thể tìm kiếm và lọc ticket theo trạng thái, mức độ ưu tiên hoặc nhóm sự cố. Hệ thống cũng cho phép xem chi tiết, mở tệp đính kèm, cập nhật trạng thái và xóa ticket.

Danh sách ticket được lấy từ Amazon DynamoDB thông qua Amazon API Gateway và AWS Lambda.

{{< project-image
src="images/5-Workshop/5.1-Project-overview/admin-dashboard.png"
alt="Dashboard quản trị viên"
caption="Hình 5.1.4: Dashboard quản trị và danh sách ticket."
>}}

---

## 8. Kết quả tổng quan

Dự án đã hình thành một hệ thống helpdesk serverless với các thành phần chính:

- Frontend được triển khai công khai.
- Có đăng ký, đăng nhập và đăng xuất.
- Có phân quyền giữa User và Admin.
- Có HTTP API để tạo, đọc, cập nhật và xóa ticket.
- Có cơ sở dữ liệu Amazon DynamoDB.
- Có lưu trữ tệp riêng tư bằng Amazon S3.
- Có email bất đồng bộ bằng Amazon SES.
- Có cập nhật thời gian thực bằng WebSocket.
- Có log và giám sát bằng Amazon CloudWatch.
- Có quy trình CI/CD từ GitHub đến AWS Amplify Hosting.

Phần tiếp theo sẽ trình bày kiến trúc tổng thể và luồng dữ liệu giữa các thành phần trong hệ thống.