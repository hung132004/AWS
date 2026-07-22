---
title: "Chia sẻ và Đánh giá"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

## Tổng kết quá trình thực tập

Chương trình thực tập đã mang đến cho tôi cơ hội quý báu để tiếp cận các công nghệ điện toán đám mây và quy trình phát triển phần mềm hiện đại. Trước khi bắt đầu dự án, tôi đã dành thời gian tìm hiểu hệ sinh thái AWS, bao gồm các khái niệm về điện toán đám mây, nguyên tắc bảo mật, mạng, lưu trữ, dịch vụ tính toán và quy trình triển khai ứng dụng. Từng bước, tôi trở nên tự tin hơn trong việc sử dụng các dịch vụ của AWS cũng như hiểu được cách chúng phối hợp với nhau để xây dựng một hệ thống hoàn chỉnh.

Nhiệm vụ chính của tôi trong suốt thời gian thực tập là thiết kế và triển khai **Campus IT Support Ticket Portal**, một ứng dụng web serverless cho phép sinh viên và nhân viên gửi yêu cầu hỗ trợ kỹ thuật, đồng thời cung cấp cho quản trị viên các công cụ để theo dõi và xử lý ticket một cách hiệu quả. Thay vì chỉ tập trung vào việc lập trình, tôi còn được học cách phân tích yêu cầu, thiết kế kiến trúc hệ thống, cấu hình các tài nguyên trên nền tảng đám mây và kiểm tra để đảm bảo mọi thành phần hoạt động ổn định cùng nhau.

Ứng dụng được xây dựng theo kiến trúc serverless, giúp giảm đáng kể công việc quản lý hạ tầng và cho phép mỗi dịch vụ AWS đảm nhiệm một vai trò riêng biệt. Phần giao diện được triển khai bằng **AWS Amplify Hosting**, trong khi việc xác thực và phân quyền người dùng được thực hiện thông qua **Amazon Cognito**. Các yêu cầu từ phía người dùng được xử lý bởi **Amazon API Gateway**, logic nghiệp vụ được triển khai trên **AWS Lambda**, và dữ liệu được lưu trữ trong **Amazon DynamoDB**. Các tệp đính kèm được lưu trên **Amazon S3**, email thông báo được gửi bằng **Amazon SES**, việc giám sát hệ thống được thực hiện thông qua **Amazon CloudWatch**, còn quyền truy cập giữa các dịch vụ được quản lý bằng **AWS IAM**.

Quá trình làm việc với kiến trúc này giúp tôi nhận ra rằng việc phát triển một ứng dụng trên nền tảng đám mây không chỉ đơn thuần là kết nối các dịch vụ lại với nhau. Mỗi thành phần cần được cấu hình chính xác, cấp quyền phù hợp, kiểm thử cẩn thận và giám sát thường xuyên để đảm bảo hệ thống hoạt động ổn định và an toàn. Tôi cũng hiểu được tầm quan trọng của việc thiết kế luồng dữ liệu ngay từ đầu, bởi chỉ một thay đổi nhỏ ở một dịch vụ cũng có thể ảnh hưởng đến nhiều thành phần khác trong hệ thống.

## Kiến thức và kỹ năng đạt được

Trong suốt quá trình thực tập, tôi đã nâng cao cả kiến thức chuyên môn lẫn kỹ năng thực hành.

- Học cách triển khai và cập nhật ứng dụng web tĩnh bằng AWS Amplify Hosting.
- Hiểu quy trình xác thực người dùng, phân quyền và xác minh JWT Token với Amazon Cognito.
- Có kinh nghiệm cấu hình HTTP API và tích hợp với AWS Lambda thông qua Amazon API Gateway.
- Triển khai các chức năng CRUD để quản lý ticket bằng AWS Lambda.
- Hiểu cách Amazon DynamoDB lưu trữ dữ liệu NoSQL và tổ chức dữ liệu cho ứng dụng.
- Thực hành tải lên, truy xuất và quản lý tệp an toàn bằng Amazon S3.
- Triển khai chức năng gửi email thông báo với Amazon SES.
- Sử dụng Amazon CloudWatch để theo dõi log, phát hiện lỗi và giám sát hoạt động của hệ thống backend.
- Áp dụng IAM Roles và IAM Policies để kiểm soát quyền truy cập giữa các dịch vụ theo nguyên tắc bảo mật.
- Cải thiện kỹ năng sử dụng GitHub, viết tài liệu bằng Hugo và quản lý quá trình triển khai dự án.

## Những khó khăn gặp phải

Mặc dù kiến trúc của dự án đã được xây dựng rõ ràng, tôi vẫn gặp nhiều khó khăn trong quá trình triển khai. Một trong những thách thức lớn nhất là tích hợp nhiều dịch vụ AWS thành một quy trình thống nhất. Amazon Cognito, API Gateway, Lambda, DynamoDB và S3 đều phụ thuộc vào việc cấu hình chính xác, vì vậy chỉ cần một thành phần gặp lỗi thì toàn bộ luồng xử lý có thể bị ảnh hưởng.

Việc quản lý quyền truy cập cũng là một thử thách đáng kể. Một số IAM Policy chưa được cấu hình đúng khiến Lambda không thể truy cập DynamoDB, S3 hoặc SES. Để khắc phục, tôi phải kiểm tra kỹ Execution Role, Resource Policy và tài liệu chính thức của AWS nhằm xác định chính xác quyền còn thiếu mà vẫn đảm bảo nguyên tắc cấp quyền tối thiểu.

Quá trình gỡ lỗi trong môi trường serverless cũng khác biệt so với các ứng dụng truyền thống. Do không có máy chủ để theo dõi trực tiếp, tôi phải sử dụng CloudWatch Logs để kiểm tra quá trình thực thi của Lambda, phản hồi từ API Gateway và các lỗi phát sinh trong từng bước xử lý. Nhờ đó, kỹ năng phân tích và xử lý sự cố của tôi được cải thiện đáng kể.

Bên cạnh đó, việc duy trì tài liệu dự án cũng đòi hỏi nhiều thời gian và sự cẩn thận. Mỗi khi kiến trúc hoặc chức năng của hệ thống thay đổi, các sơ đồ, tài liệu workshop, hướng dẫn triển khai và báo cáo tiến độ cũng cần được cập nhật để đảm bảo tính nhất quán.

## Đánh giá cá nhân

Nhìn chung, tôi đánh giá chương trình thực tập đã giúp tôi nâng cao đáng kể hiểu biết về điện toán đám mây cũng như phương pháp phát triển ứng dụng serverless. Việc kết hợp giữa tự học, thực hành và sự hướng dẫn từ mentor đã giúp tôi củng cố nền tảng kỹ thuật cũng như khả năng giải quyết vấn đề trong thực tế.

Ngoài kiến thức chuyên môn, tôi còn cải thiện nhiều kỹ năng mềm như quản lý thời gian, giao tiếp kỹ thuật, viết tài liệu và tổ chức công việc. Việc chia nhỏ các nhiệm vụ lớn thành từng giai đoạn giúp tôi quản lý tiến độ hiệu quả hơn và hoàn thành dự án đúng kế hoạch.

Chương trình thực tập cũng giúp tôi nhận ra tầm quan trọng của việc học tập liên tục. AWS cung cấp rất nhiều dịch vụ và mỗi dự án đều mang đến những công nghệ cũng như phương pháp mới. Điều này tạo động lực để tôi tiếp tục nghiên cứu sâu hơn về phát triển ứng dụng trên nền tảng đám mây và các kiến trúc hiện đại.

## Định hướng phát triển

Nếu có cơ hội tiếp tục phát triển dự án này, tôi mong muốn cải thiện thêm một số nội dung sau:

- Xây dựng dashboard thống kê trực quan với biểu đồ và báo cáo chi tiết.
- Nâng cấp chức năng tìm kiếm và lọc ticket với nhiều điều kiện hơn.
- Bổ sung nhật ký hoạt động (Audit Log) để theo dõi thao tác của quản trị viên.
- Mở rộng chức năng thông báo bằng nhiều kênh khác ngoài email.
- Tăng cường bảo mật thông qua các IAM Policy chi tiết và cơ chế xác thực bổ sung.
- Tối ưu hiệu năng hệ thống và giảm chi phí vận hành bằng cách tối ưu cấu hình tài nguyên.
- Hoàn thiện tài liệu hướng dẫn triển khai, bảo trì và xử lý sự cố để thuận tiện cho việc phát triển sau này.

## Kết luận

Hoàn thành kỳ thực tập này là một cột mốc quan trọng trong quá trình học tập của tôi. Chương trình đã giúp tôi áp dụng kiến thức được học tại trường vào một dự án thực tế, đồng thời tích lũy kinh nghiệm với các công nghệ điện toán đám mây đang được sử dụng phổ biến trong doanh nghiệp.

Quan trọng hơn, tôi đã hiểu rõ hơn về cách một ứng dụng hiện đại được thiết kế, triển khai, bảo mật và vận hành trên nền tảng AWS. Những kiến thức và kinh nghiệm thu được trong suốt quá trình thực tập đã giúp tôi tự tin hơn khi xây dựng các ứng dụng cloud và tạo nền tảng vững chắc cho định hướng phát triển nghề nghiệp trong lĩnh vực phát triển phần mềm và điện toán đám mây trong tương lai.

Tôi xin chân thành cảm ơn các mentor và những người đã đồng hành trong suốt chương trình thực tập. Sự hướng dẫn và hỗ trợ của mọi người đã góp phần quan trọng vào sự phát triển chuyên môn cũng như kỹ năng làm việc của tôi. Tôi tin rằng những kinh nghiệm tích lũy được từ kỳ thực tập này sẽ là hành trang quý giá cho con đường học tập và sự nghiệp sau này.