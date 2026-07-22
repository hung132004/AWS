---
title: "Triển khai frontend với AWS Amplify"
date: 2026-07-21
weight: 4
chapter: false
pre: "<b>5.4 </b>"
---

Frontend của hệ thống được triển khai bằng **AWS Amplify Hosting**. Amplify được kết nối với GitHub để tự động build và deploy khi source code thay đổi.

#### Các bước thực hiện

1. Mở AWS Amplify Console và tạo ứng dụng mới.
2. Kết nối Amplify với repository GitHub của project.
3. Chọn branch chính để deploy.
4. Kiểm tra build settings và bắt đầu quá trình deploy.
5. Sau khi deploy thành công, mở domain mặc định của Amplify để kiểm tra website.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.1-AWS-Amplify-Hosting/amplify-hosting.png"
alt="AWS Amplify Hosting"
caption="Hình 5.4.1: Ứng dụng frontend được cấu hình trên AWS Amplify Hosting."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.1-AWS-Amplify-Hosting/deployment-success.png"
alt="Amplify deploy thành công"
caption="Hình 5.4.2: Amplify build và deploy frontend thành công."
>}}

#### Kết quả

Website đã được deploy công khai tại: [https://main.d37atxjbyyp60m.amplifyapp.com/](https://main.d37atxjbyyp60m.amplifyapp.com/)