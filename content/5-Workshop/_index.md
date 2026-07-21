---
title: "Workshop"
date: 2026-01-01
weight: 5
chapter: false
pre: " 5. "
---

# Workshop: Building a Serverless Application with AWS

---

### Overview

**LunaGenZ** is a Numerology project built entirely on AWS Serverless architecture. This workshop will guide you through the entire process of deploying Backend logic, automating internal PDF report generation, and hosting the Frontend application.

In this lab, we have implemented:
- Built and deployed Serverless Backend using AWS Lambda and API Gateway.
- Automated PDF report generation based on Numerology indicators.
- Hosted Frontend interface with high availability on Amazon S3 and Amazon CloudFront.

---

### What will you build?

At the end of this workshop, you will have a complete Serverless application running on AWS, with:
- **Frontend Interface** - Static user interface (HTML/CSS/JS)
- **Backend Logic** - Process numerology calculations using AWS Lambda
- **PDF Report Generation** - Automatically compile results into downloadable PDF

---

### Architecture Diagram

![LunaGenZ Architecture](images/lunagenz-architecture.svg)

### Detailed Architecture

| Component | AWS Service | Description |
|-----------|-------------|-------------|
| **Frontend** | Amazon S3 + CloudFront | User interface, static hosting, global distribution |
| **Backend API** | Amazon API Gateway + Lambda | Process numerology calculation logic |
| **PDF Generator** | AWS Lambda | Automatically generate PDF reports |
| **PDF Storage** | Amazon S3 | Store generated PDF files |

---

### Content

1. [Workshop Overview](5.1-overview/)
   - Introduction to LunaGenZ and Serverless architecture
   - Overview of components to deploy

2. [Prerequisites](5.2-prerequisites/)
   - Requirements before starting
   - Source Code and necessary tools

3. [Backend Lambda](5.3-backend-lambda/)
   - [Create Lambda Function](5.3.1-create-lambda/) - Write Lambda to calculate numerology indicators
   - [Configure API Gateway](5.3.2-configure-api-gateway/) - Create REST API endpoint to invoke Lambda

4. [Create PDF Report](5.4-create-pdf-report/)
   - [Create Lambda PDF Generator](5.4.1-create-pdf-function/) - Write Lambda to generate PDF using PDFKit

5. [Frontend Hosting](5.5-hosting-frontend/)
   - [S3 Hosting](5.5.1-s3-hosting/) - Upload static files to S3 and enable static website hosting
   - [CloudFront CDN](5.5.2-cloudfront/) - Distribute content globally with HTTPS

6. [Cleanup](5.6-cleanup/)
   - [Clean up Resources](5.6.1-cleanup-resources/) - Guide to delete all created resources

---

### Links

- **Website:** [https://www.lunagenz.sbs/](https://www.lunagenz.sbs/)
- **Video Demo:** [https://drive.google.com/drive/folders/1EIiVDEET1jN1fQLz751UtGRnkJPrTmsI?usp=sharing](https://drive.google.com/drive/folders/1EIiVDEET1jN1fQLz751UtGRnkJPrTmsI?usp=sharing)
- **GitHub:** [https://github.com/qwe890000/workshop_mytam](https://github.com/qwe890000/workshop_mytam)
