---
title: "Workshop"
date: 2026-01-01
weight: 5
chapter: false
pre: " 5. "
---

# Workshop: Xây dựng Ứng dụng Serverless với AWS

---

## Tổng quan

**LunaGenZ** là một dự án Thần Số Học được xây dựng hoàn toàn trên kiến trúc AWS Serverless. Workshop này sẽ hướng dẫn toàn bộ quy trình triển khai logic Backend, tự động hóa việc tạo báo cáo PDF nội bộ, và host ứng dụng Frontend.

Trong bài lab này, chúng em đã thực hiện:
- Xây dựng và triển khai Backend Serverless bằng AWS Lambda và API Gateway.
- Tự động hóa quá trình sinh báo cáo PDF dựa trên các chỉ số Thần Số Học.
- Host giao diện Frontend đảm bảo tính sẵn sàng cao trên Amazon S3 và Amazon CloudFront.

---

## Giới thiệu về LunaGenZ

LunaGenZ là một ứng dụng Thần Số Học sáng tạo, được thiết kế để tính toán và tạo ra các báo cáo thần số học cá nhân chi tiết. Để đảm bảo tính sẵn sàng cao, khả năng mở rộng và tối ưu chi phí, toàn bộ ứng dụng được xây dựng trên kiến trúc **Serverless của AWS**.

---

## Bạn sẽ xây dựng gì?

Cuối workshop này, bạn sẽ có một ứng dụng Serverless hoàn chỉnh chạy trên AWS, với:

- **Giao diện Frontend** - Giao diện người dùng tĩnh (HTML/CSS/JS), được lưu trữ trên S3 và phân phối toàn cầu qua CloudFront
- **Logic Backend** - Xử lý tính toán thần số học bằng AWS Lambda, được kích hoạt an toàn thông qua API Gateway
- **Tạo báo cáo PDF** - Tự động tổng hợp kết quả thành PDF có thể tải xuống bằng hàm Serverless chuyên dụng

---

## Sơ đồ kiến trúc

![LunaGenZ Architecture](images/architecture-diagram.png)

---

## Kiến trúc chi tiết

| Thành phần | Dịch vụ AWS | Mô tả |
|------------|-------------|-------|
| **Frontend** | Amazon S3 + CloudFront | Giao diện người dùng tĩnh, lưu trữ tĩnh, phân phối toàn cầu với HTTPS |
| **Backend API** | Amazon API Gateway + Lambda | Xử lý logic tính toán thần số học, REST API endpoint |
| **PDF Generator** | AWS Lambda | Tạo báo cáo PDF tự động từ kết quả tính toán |
| **Lưu trữ PDF** | Amazon S3 | Lưu trữ các file PDF đã tạo |

---

## Luồng hoạt động

1. **Người dùng** truy cập website qua **CloudFront**
2. **CloudFront** phân phối nội dung từ **S3 Bucket**
3. Người dùng nhập thông tin (Họ tên, Ngày sinh)
4. **Frontend** gửi request đến **API Gateway**
5. **API Gateway** kích hoạt **Lambda Function**
6. **Lambda** tính toán và trả kết quả
7. Khi cần, **Lambda PDF Generator** tạo báo cáo PDF và lưu vào S3

---

## Các chỉ số Thần Số Học được tính toán

| Chỉ số | Mô tả |
|--------|-------|
| **Life Path Number** | Con đường cuộc đời - từ ngày sinh |
| **Expression Number** | Biểu hiện tài năng - từ họ tên đầy đủ |
| **Soul Urge Number** | Linh hồn bên trong - từ nguyên âm trong tên |
| **Personality Number** | Tính cách bên ngoài - từ phụ âm trong tên |
| **Birthday Number** | Ngày sinh rút gọn |

---

## Nội dung chi tiết

### 1. Tổng quan Workshop
- [5.1 - Tổng quan](5.1-overview/)
  - Giới thiệu về LunaGenZ và kiến trúc Serverless
  - Tổng quan các thành phần sẽ triển khai
  - Luồng hoạt động của ứng dụng

### 2. Chuẩn bị (Prerequisites)
- [5.2 - Điều kiện tiên quyết](5.2-prerequisites/)
  - Yêu cầu trước khi bắt đầu
  - Source Code và công cụ cần thiết (AWS Account, AWS CLI, Git)

### 3. Backend Lambda
- [5.3.1 - Tạo Lambda Function](5.3-backend-lambda/5.3.1-create-lambda/)
  - Tạo IAM Role với quyền cần thiết
  - Viết Lambda để tính toán các chỉ số thần số học
  - Cấu hình Environment Variables
  - Monitoring với CloudWatch

- [5.3.2 - Cấu hình API Gateway](5.3-backend-lambda/5.3.2-configure-api-gateway/)
  - Tạo REST API endpoint để gọi Lambda
  - Cấu hình CORS
  - Test API

### 4. Tạo báo cáo PDF
- [5.4.1 - Tạo Lambda PDF Generator](5.4-create-pdf-report/5.4.1-create-pdf-function/)
  - Tạo Lambda Layer cho Puppeteer
  - Viết Lambda để tạo PDF sử dụng PDFKit
  - Upload PDF lên S3

### 5. Hosting Frontend
- [5.5.1 - S3 Hosting](5.5-hosting-frontend/5.5.1-s3-hosting/)
  - Upload static files lên S3
  - Bật static website hosting
  - Cấu hình Bucket Policy

- [5.5.2 - CloudFront CDN](5.5-hosting-frontend/5.5.2-cloudfront/)
  - Phân phối nội dung toàn cầu với HTTPS
  - Cấu hình SSL Certificate
  - Cache invalidation

### 6. Dọn dẹp
- [5.6.1 - Dọn dẹp Resources](5.6-cleanup/5.6.1-cleanup-resources/)
  - Hướng dẫn xóa tất cả resources đã tạo
  - Tránh phát sinh chi phí không cần thiết

---

## Thứ tự thực hiện

```
Tổng quan → Chuẩn bị → Tạo Lambda (Backend) → Cấu hình API Gateway → Tạo Lambda (PDF) → S3 Hosting → CloudFront → Dọn dẹp
```

---

## Công nghệ sử dụng

| Công nghệ | Mục đích |
|-----------|----------|
| **Node.js 20.x** | Runtime cho AWS Lambda |
| **HTML/CSS/JS** | Frontend tĩnh |
| **Puppeteer** | Chuyển HTML sang PDF |
| **PDFKit** | Tạo file PDF |

---

## Liên kết

- **Website:** [https://www.lunagenz.sbs/](https://www.lunagenz.sbs/)
- **Video Demo:** [Xem video](https://drive.google.com/drive/folders/1EIiVDEET1jN1fQLz751UtGRnkJPrTmsI?usp=sharing)
- **GitHub:** [https://github.com/qwe890000/workshop_mytam](https://github.com/qwe890000/workshop_mytam)
