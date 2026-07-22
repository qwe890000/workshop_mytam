---
title: "Workshop"
date: 2026-01-01
weight: 5
chapter: false
pre: " 5. "
---

<div style="text-align: left; font-size: 16px; line-height: 1.8;">

# Workshop: Building a Serverless Application with AWS

---

## Overview

**LunaGenZ** is a Numerology project built entirely on AWS Serverless architecture. This workshop will guide you through the entire process of deploying Backend logic, automating PDF report generation, and hosting the Frontend application.

In this lab, we have completed:

- Built and deployed a Serverless Backend using AWS Lambda and API Gateway.
- Automated the process of generating PDF reports based on Numerology indices.
- Hosted the Frontend interface with high availability on Amazon S3 and Amazon CloudFront.

---

## About LunaGenZ

LunaGenZ is an innovative Numerology application, designed to calculate and generate detailed personal numerology reports. To ensure high availability, scalability, and cost optimization, the entire application is built on **AWS Serverless architecture**.

---

## What Will You Build?

By the end of this workshop, you will have a complete Serverless application running on AWS, with:

- **Frontend Interface** - Static user interface (HTML/CSS/JS), stored on S3 and distributed globally via CloudFront
- **Backend Logic** - Numerology calculation processing using AWS Lambda, securely triggered through API Gateway
- **PDF Report Generation** - Automatically compile results into downloadable PDFs using a dedicated Serverless function

---

## Architecture Diagram

<div style="text-align: center; margin: 20px 0;">
<img src="/workshop_mytam/images/architecture-diagram.png" alt="LunaGenZ Architecture" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.1);">
</div>

---

## Detailed Architecture

| Component | AWS Services | Description |
|:----------|:------------|:------------|
| **Frontend** | Amazon S3 + CloudFront | Static user interface, static hosting, global distribution with HTTPS |
| **Backend API** | Amazon API Gateway + Lambda | Numerology calculation logic processing, REST API endpoint |
| **PDF Generator** | AWS Lambda | Automatically generate PDF reports from calculation results |
| **PDF Storage** | Amazon S3 | Store generated PDF files |

---

## Workflow

1. **User** accesses website via **CloudFront**
2. **CloudFront** distributes content from **S3 Bucket**
3. User enters information (Full Name, Birthdate)
4. **Frontend** sends request to **API Gateway**
5. **API Gateway** triggers **Lambda Function**
6. **Lambda** calculates and returns results
7. When needed, **Lambda PDF Generator** creates PDF report and saves to S3

---

## Numerology Indices Calculated

| Index | Description |
|:------|:------------|
| **Life Path Number** | Life path - from birthdate |
| **Expression Number** | Talent expression - from full name |
| **Soul Urge Number** | Inner soul - from vowels in name |
| **Personality Number** | Outer personality - from consonants in name |
| **Birthday Number** | Reduced birthday |

---

## Detailed Content

### 1. Workshop Overview
- [5.1 - Overview](5.1-overview/)
  - Introduction to LunaGenZ and Serverless architecture
  - Overview of components to deploy
  - Application workflow

### 2. Prerequisites
- [5.2 - Prerequisites](5.2-prerequisites/)
  - Prerequisites before starting
  - Source Code and required tools (AWS Account, AWS CLI, Git)

### 3. Backend Lambda
- [5.3.1 - Create Lambda Function](5.3-backend-lambda/5.3.1-create-lambda/)
  - Create IAM Role with necessary permissions
  - Write Lambda to calculate numerology indices
  - Configure Environment Variables
  - Monitoring with CloudWatch

- [5.3.2 - Configure API Gateway](5.3-backend-lambda/5.3.2-configure-api-gateway/)
  - Create REST API endpoint to invoke Lambda
  - Configure CORS
  - Test API

### 4. PDF Report Generation
- [5.4.1 - Create Lambda PDF Generator](5.4-create-pdf-report/5.4.1-create-pdf-function/)
  - Create Lambda Layer for Puppeteer
  - Write Lambda to generate PDF using PDFKit
  - Upload PDF to S3

### 5. Hosting Frontend
- [5.5.1 - S3 Hosting](5.5-hosting-frontend/5.5.1-s3-hosting/)
  - Upload static files to S3
  - Enable static website hosting
  - Configure Bucket Policy

- [5.5.2 - CloudFront CDN](5.5-hosting-frontend/5.5.2-cloudfront/)
  - Distribute content globally with HTTPS
  - Configure SSL Certificate
  - Cache invalidation

### 6. Cleanup
- [5.6.1 - Clean up Resources](5.6-cleanup/5.6.1-cleanup-resources/)
  - Guide to delete all created resources
  - Avoid unnecessary costs

---

## Execution Order

```
Overview → Prerequisites → Create Lambda (Backend) → Configure API Gateway → Create Lambda (PDF) → S3 Hosting → CloudFront → Cleanup
```

---

## Technologies Used

| Technology | Purpose |
|:-----------|:--------|
| **Node.js 20.x** | Runtime for AWS Lambda |
| **HTML/CSS/JS** | Static Frontend |
| **Puppeteer** | Convert HTML to PDF |
| **PDFKit** | Generate PDF files |

---

## Links

- **Website:** [https://www.lunagenz.sbs/](https://www.lunagenz.sbs/)
- **Video Demo:** [Watch video](https://drive.google.com/drive/folders/1EIiVDEET1jN1fQLz751UtGRnkJPrTmsI?usp=sharing)
- **GitHub:** [https://github.com/qwe890000/workshop_mytam](https://github.com/qwe890000/workshop_mytam)

</div>
