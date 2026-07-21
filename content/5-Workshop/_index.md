---
title: "Workshop"
date: 2026-01-01
weight: 5
chapter: false
pre: " 5. "
---

### Overview

**LunaGenZ** is a Numerology project built entirely on AWS Serverless architecture. This workshop will guide you through the entire process of deploying Backend logic, automating internal PDF report generation, and hosting the Frontend application.

In this lab, we have implemented:
+ Built and deployed Serverless Backend using AWS Lambda and API Gateway.
+ Automated PDF report generation based on Numerology indicators.
+ Hosted Frontend interface with high availability on Amazon S3 and Amazon CloudFront.

### Content

1. [Workshop Overview](5.1-overview/)
2. [Prerequisites](5.2-prerequisites/)
3. [Backend Lambda](5.3-backend-lambda/)
   - [Create Lambda Function](5.3.1-create-lambda-function/)
   - [Configure API Gateway](5.3.2-configure-api-gateway/)
4. [Create PDF Report](5.4-create-pdf-report/)
   - [Create Lambda PDF Generator](5.4.1-create-lambda-pdf-generator/)
5. [Frontend Hosting](5.5-hosting-frontend/)
   - [Deploy Frontend to S3](5.5.1-deploy-frontend-to-s3/)
   - [CloudFront CDN](5.5.2-cloudfront-cdn/)
6. [Cleanup](5.6-cleanup/)
   - [Clean up Resources](5.6.1-clean-up-resources/)

### Architecture Diagram

![LunaGenZ Architecture](images/lunagenz-architecture.svg)

### Links

- **Website:** [https://www.lunagenz.sbs/](https://www.lunagenz.sbs/)
