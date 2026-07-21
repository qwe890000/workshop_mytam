---
title: "Workshop"
date: 2026-01-01
weight: 5
chapter: false
pre: " 5. "
---

#### Tổng quan

**LunaGenZ** là một dự án Thần Số Học được xây dựng hoàn toàn trên kiến trúc AWS Serverless. Workshop này sẽ hướng dẫn toàn bộ quy trình triển khai logic Backend, tự động hóa việc tạo báo cáo PDF nội bộ, và host ứng dụng Frontend.

Trong bài lab này, chúng em đã thực hiện:
+ Xây dựng và triển khai Backend Serverless bằng AWS Lambda và API Gateway.
+ Tự động hóa quá trình sinh báo cáo PDF dựa trên các chỉ số Thần Số Học.
+ Host giao diện Frontend đảm bảo tính sẵn sàng cao trên Amazon S3 và Amazon CloudFront.

#### Nội dung

1. [Tổng quan Workshop](5.1-overview/)
2. [Chuẩn bị (Prerequisites)](5.2-prerequisites/)
3. [Backend Lambda](5.3-backend-lambda/)
   - [Tạo Lambda Function](5.3.1-create-lambda-function/)
   - [Cấu hình API Gateway](5.3.2-configure-api-gateway/)
4. [Tạo báo cáo PDF](5.4-create-pdf-report/)
   - [Tạo Lambda PDF Generator](5.4.1-create-lambda-pdf-generator/)
5. [Hosting Frontend](5.5-hosting-frontend/)
   - [Deploy Frontend lên S3](5.5.1-deploy-frontend-to-s3/)
   - [CloudFront CDN](5.5.2-cloudfront-cdn/)
6. [Dọn dẹp](5.6-cleanup/)
   - [Dọn dẹp tài nguyên](5.6.1-clean-up-resources/)

#### Sơ đồ kiến trúc

![LunaGenZ Architecture](images/lunagenz-architecture.svg)

#### Liên kết

- **Website:** [https://www.lunagenz.sbs/](https://www.lunagenz.sbs/)
