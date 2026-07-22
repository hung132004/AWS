---
title: "Kiểm tra tài nguyên và chi phí"
date: 2026-07-21
weight: 13
chapter: false
pre: "<b>5.13 </b>"
---

Sau khi triển khai và kiểm thử, tôi rà soát lại các tài nguyên AWS để tránh phát sinh chi phí không cần thiết.

#### Các bước thực hiện

1. Kiểm tra Amplify app và domain đang hoạt động.
2. Kiểm tra Lambda, DynamoDB, S3, SES, API Gateway và CloudWatch.
3. Theo dõi Billing Dashboard để kiểm soát chi phí.
4. Giữ lại các tài nguyên cần thiết cho demo và báo cáo.
5. Ghi chú các tài nguyên có thể cleanup sau khi hoàn tất chấm bài.

#### Kết quả

Các tài nguyên chính vẫn được giữ lại để phục vụ demo website. Sau khi hoàn tất báo cáo, có thể xóa tài nguyên không cần thiết để tránh phát sinh chi phí.