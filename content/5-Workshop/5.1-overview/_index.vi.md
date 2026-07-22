---
title: "Tổng quan"
weight: 1
chapter: true
pre: " <b> 5.1. </b> "
---

<div style="text-align: left; font-size: 16px; line-height: 1.8;">

## Về LunaGenZ

LunaGenZ là ứng dụng Thần Số Học sáng tạo, được thiết kế để tính toán và tạo báo cáo thần số học chi tiết cho cá nhân. Để đảm bảo tính khả dụng cao, khả năng mở rộng và tối ưu chi phí, toàn bộ ứng dụng được xây dựng trên **kiến trúc Serverless của AWS**.

---

## Tổng quan Kiến trúc

Trong workshop này, bạn sẽ triển khai các thành phần sau:

### 1. Frontend (Amazon S3 & CloudFront)

Giao diện người dùng tĩnh (được xây dựng bằng HTML/CSS/JS hoặc Framework). Được lưu trữ trên S3 và phân phối toàn cầu qua CloudFront.

### 2. Backend (Amazon API Gateway & AWS Lambda)

Logic tính toán thần số học cốt lõi được xử lý bởi các hàm AWS Lambda, được kích hoạt một cách bảo mật thông qua API Gateway.

### 3. Tạo báo cáo PDF (AWS Lambda)

Một hàm Serverless chuyên dụng tự động tổng hợp kết quả tính toán thành báo cáo PDF có thể tải xuống.

---

## Sơ đồ Kiến trúc

<div style="text-align: center; margin: 20px 0;">
<img src="/workshop_mytam/images/architecture-diagram.png" alt="LunaGenZ Architecture" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.1);">
</div>

---

## Bạn sẽ xây dựng gì?

Cuối workshop này, bạn sẽ có một ứng dụng Serverless hoàn chỉnh chạy trên AWS, với:

- **Giao diện Frontend** - Giao diện HTML/CSS/JS tĩnh được host trên S3, phân phối toàn cầu qua CloudFront
- **Logic Backend** - Tính toán thần số học được xử lý bởi AWS Lambda, kích hoạt qua API Gateway
- **Tạo báo cáo PDF** - Tự động tạo báo cáo PDF có thể tải xuống bằng các hàm Serverless

---

## Bước tiếp theo

Chuyển sang **Điều kiện tiên quyết** để đảm bảo đã chuẩn bị đầy đủ các công cụ cần thiết.

</div>
