---
title: "Overview"
weight: 1
chapter: true
pre: " <b> 5.1. </b> "
---

<div style="text-align: left; font-size: 16px; line-height: 1.8;">

## About LunaGenZ

LunaGenZ is an innovative Numerology application designed to calculate and generate detailed personal numerology reports. To ensure high availability, scalability, and cost optimization, the entire application is built on **AWS Serverless architecture**.

---

## Architecture Overview

In this workshop, you will deploy the following components:

### 1. Frontend (Amazon S3 & CloudFront)

Static user interface (built with HTML/CSS/JS or Framework). It is stored on S3 and distributed globally via CloudFront.

### 2. Backend (Amazon API Gateway & AWS Lambda)

Core numerology calculation logic is processed by AWS Lambda functions, triggered securely through API Gateway.

### 3. PDF Report Generation (AWS Lambda)

A dedicated Serverless function that automatically compiles calculation results into a downloadable PDF report.

---

## Architecture Diagram

<div style="text-align: center; margin: 20px 0;">
<img src="/workshop_mytam/5-Workshop/images/architecture-diagram.png" alt="LunaGenZ Architecture" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.1);">
</div>

---

## What Will You Build?

By the end of this workshop, you will have a complete Serverless application running on AWS, with:

- **Frontend Interface** - Static HTML/CSS/JS hosted on S3, distributed globally via CloudFront
- **Backend Logic** - Numerology calculations processed by AWS Lambda, triggered via API Gateway
- **PDF Report Generation** - Automatically generate downloadable PDF reports using Serverless functions

---

## Next Steps

Proceed to **Prerequisites** section to begin.

</div>
