---
title: "Workshop"
date: 2026-01-01
weight: 5
chapter: false
pre: " 5. "
---

# Workshop: Xây dựng Ứng dụng Serverless với AWS

---

### Tổng quan

**LunaGenZ** là một dự án Thần Số Học được xây dựng hoàn toàn trên kiến trúc AWS Serverless. Workshop này sẽ hướng dẫn toàn bộ quy trình triển khai logic Backend, tự động hóa việc tạo báo cáo PDF nội dung, và host ứng dụng Frontend.

Trong bài lab này, chúng em đã thực hiện:
- Xây dựng và triển khai Backend Serverless bằng AWS Lambda và API Gateway.
- Tự động hóa quá trình sinh báo cáo PDF dựa trên các chỉ số Thần Số Học.
- Host giao diện Frontend đảm bảo tính sẵn sàng cao trên Amazon S3 và Amazon CloudFront.

---

### Bạn sẽ xây dựng gì?

Cuối workshop này, bạn sẽ có một ứng dụng Serverless hoàn chỉnh chạy trên AWS, với:
- **Giao diện Frontend** - Giao diện người dùng tĩnh (HTML/CSS/JS)
- **Logic Backend** - Xử lý tính toán thần số học bằng AWS Lambda
- **Tạo báo cáo PDF** - Tự động tổng hợp kết quả thành PDF có thể tải xuống

---

### Sơ đồ kiến trúc

![LunaGenZ Architecture](images/lunagenz-architecture.svg)

### Kiến trúc chi tiết

| Thành phần | Dịch vụ AWS | Mô tả |
|------------|-------------|-------|
| **Frontend** | Amazon S3 + CloudFront | Giao diện người dùng, lưu trữ tĩnh, phân phối toàn cầu |
| **Backend API** | Amazon API Gateway + Lambda | Xử lý logic tính toán thần số học |
| **PDF Generator** | AWS Lambda | Tạo báo cáo PDF tự động |
| **Lưu trữ PDF** | Amazon S3 | Lưu trữ các file PDF đã tạo |

---

### Nội dung

1. [Tổng quan Workshop](5.1-overview/)
   - Giới thiệu về LunaGenZ và kiến trúc Serverless
   - Tổng quan các thành phần sẽ triển khai

2. [Chuẩn bị (Prerequisites)](5.2-prerequisites/)
   - Yêu cầu trước khi bắt đầu
   - Source Code và công cụ cần thiết

3. [Backend Lambda](5.3-backend-lambda/)
   - [Tạo Lambda Function](5.3.1-create-lambda/) - Viết Lambda để tính toán các chỉ số thần số học
   - [Cấu hình API Gateway](5.3.2-configure-api-gateway/) - Tạo REST API endpoint để gọi Lambda

4. [Tạo báo cáo PDF](5.4-create-pdf-report/)
   - [Tạo Lambda PDF Generator](5.4.1-create-pdf-function/) - Viết Lambda để tạo PDF sử dụng PDFKit

5. [Hosting Frontend](5.5-hosting-frontend/)
   - [S3 Hosting](5.5.1-s3-hosting/) - Upload static files lên S3 và bật static website hosting
   - [CloudFront CDN](5.5.2-cloudfront/) - Phân phối nội dung toàn cầu với HTTPS

6. [Dọn dẹp](5.6-cleanup/)
   - [Dọn dẹp Resources](5.6.1-cleanup-resources/) - Hướng dẫn xóa tất cả resources đã tạo

---

### Liên kết

- **Website:** [https://www.lunagenz.sbs/](https://www.lunagenz.sbs/)
- **Video Demo:** [https://drive.google.com/drive/folders/1EIiVDEET1jN1fQLz751UtGRnkJPrTmsI?usp=sharing](https://drive.google.com/drive/folders/1EIiVDEET1jN1fQLz751UtGRnkJPrTmsI?usp=sharing)
- **GitHub:** [https://github.com/qwe890000/workshop_mytam](https://github.com/qwe890000/workshop_mytam)
