---
title: "Workshop"
date: 2026-01-01
weight: 5
chapter: false
pre: " 5. "
---

# Workshop: Building a Serverless Application with AWS

---

## Overview

**LunaGenZ** is a Numerology project built entirely on AWS Serverless architecture. This workshop will guide you through the entire process of deploying Backend logic, automating internal PDF report generation, and hosting the Frontend application.

In this lab, we have implemented:
- Built and deployed Serverless Backend using AWS Lambda and API Gateway.
- Automated PDF report generation based on Numerology indicators.
- Hosted Frontend interface with high availability on Amazon S3 and Amazon CloudFront.

---

## About LunaGenZ

LunaGenZ is an innovative Numerology application, designed to calculate and generate detailed personal numerology reports. To ensure high availability, scalability, and cost optimization, the entire application is built on **AWS Serverless architecture**.

---

## What will you build?

At the end of this workshop, you will have a complete Serverless application running on AWS, with:

- **Frontend Interface** - Static user interface (HTML/CSS/JS), hosted on S3 and distributed globally via CloudFront
- **Backend Logic** - Process numerology calculations using AWS Lambda, securely triggered through API Gateway
- **PDF Report Generation** - Automatically compile results into downloadable PDF using dedicated Serverless function

---

## Architecture Diagram

![LunaGenZ Architecture](images/lunagenz-architecture.png)

---

## Detailed Architecture

| Component | AWS Service | Description |
|-----------|-------------|-------------|
| **Frontend** | Amazon S3 + CloudFront | Static user interface, static hosting, global HTTPS distribution |
| **Backend API** | Amazon API Gateway + Lambda | Process numerology calculation logic, REST API endpoint |
| **PDF Generator** | AWS Lambda | Automatically generate PDF reports from calculation results |
| **PDF Storage** | Amazon S3 | Store generated PDF files |

---

## Workflow

1. **User** accesses website via **CloudFront**
2. **CloudFront** distributes content from **S3 Bucket**
3. User enters information (Name, Birthdate)
4. **Frontend** sends request to **API Gateway**
5. **API Gateway** triggers **Lambda Function**
6. **Lambda** calculates and returns results
7. When needed, **Lambda PDF Generator** creates PDF report and saves to S3

---

## Numerology Indicators Calculated

| Indicator | Description |
|-----------|-------------|
| **Life Path Number** | Life path - from birthdate |
| **Expression Number** | Talent expression - from full name |
| **Soul Urge Number** | Inner soul - from vowels in name |
| **Personality Number** | Outer personality - from consonants in name |
| **Birthday Number** | Reduced birth day |

---

## Detailed Content

### 1. Workshop Overview
- [5.1 - Overview](5.1-overview/)
  - Introduction to LunaGenZ and Serverless architecture
  - Overview of components to deploy
  - Application workflow

### 2. Prerequisites
- [5.2 - Prerequisites](5.2-prerequisites/)
  - Requirements before starting
  - Source Code and necessary tools (AWS Account, AWS CLI, Git)

### 3. Backend Lambda
- [5.3.1 - Create Lambda Function](5.3-backend-lambda/5.3.1-create-lambda/)
  - Create IAM Role with necessary permissions
  - Write Lambda to calculate numerology indicators
  - Configure Environment Variables
  - Monitoring with CloudWatch

- [5.3.2 - Configure API Gateway](5.3-backend-lambda/5.3.2-configure-api-gateway/)
  - Create REST API endpoint to invoke Lambda
  - Configure CORS
  - Test API

### 4. Create PDF Report
- [5.4.1 - Create Lambda PDF Generator](5.4-create-pdf-report/5.4.1-create-pdf-function/)
  - Create Lambda Layer for Puppeteer
  - Write Lambda to generate PDF using PDFKit
  - Upload PDF to S3

### 5. Frontend Hosting
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
|------------|---------|
| **Node.js 20.x** | Runtime for AWS Lambda |
| **HTML/CSS/JS** | Static Frontend |
| **Puppeteer** | Convert HTML to PDF |
| **PDFKit** | Generate PDF files |

---

## Links

- **Website:** [https://www.lunagenz.sbs/](https://www.lunagenz.sbs/)
- **Video Demo:** [View video](https://drive.google.com/drive/folders/1EIiVDEET1jN1fQLz751UtGRnkJPrTmsI?usp=sharing)
- **GitHub:** [https://github.com/qwe890000/workshop_mytam](https://github.com/qwe890000/workshop_mytam)
