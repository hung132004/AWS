---
title: "Lưu file đính kèm với Amazon S3"
date: 2026-07-21
weight: 8
chapter: false
pre: "<b>5.8 </b>"
---

Amazon S3 được sử dụng để lưu file đính kèm khi người dùng gửi ticket, ví dụ ảnh lỗi hoặc tài liệu minh họa.

#### Các bước thực hiện

1. Tạo S3 bucket riêng tư để lưu file.
2. Lambda tạo presigned URL để upload hoặc tải file.
3. Frontend gửi file lên S3 thông qua URL được cấp.
4. Object key của file được lưu cùng ticket trong DynamoDB.

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.6-Amazon-S3/s3-bucket.png"
alt="S3 bucket"
caption="Hình 5.8.1: S3 bucket dùng để lưu file đính kèm."
>}}

{{< project-image
src="images/5-Workshop/5.3-AWS-Services/5.3.6-Amazon-S3/uploaded-files.png"
alt="Uploaded files"
caption="Hình 5.8.2: File đính kèm đã được upload lên S3."
>}}