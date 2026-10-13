# Secure-Banking-Application-on-AWS

# 🏦 Secure Banking Application on AWS

A secure, scalable, cloud-based **banking demo application** built on AWS. It showcases how core AWS services work together to deliver authentication, data protection, high availability, monitoring, and auditing for a financial-style workload.

> ⚠️ **Disclaimer:** This is a learning/demo project. Fund transfers are **simulated** and no real money or real customer data is involved.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [AWS Services Used](#-aws-services-used)
- [Security Highlights](#-security-highlights)
- [Data Consistency](#-data-consistency)
- [Monitoring & Auditing](#-monitoring--auditing)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [Screenshots](#-screenshots)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 🔍 Overview

This project demonstrates the design and deployment of a secure banking application using AWS. It covers the full cloud stack: compute and scaling, managed database, identity and access management, encryption, and observability, all following AWS security best practices.

## ✨ Features

- 🔐 **Customer authentication** with Amazon Cognito
- 💰 **Account balance enquiry**
- 🔁 **Simulated fund transfers** between accounts
- 📜 **Transaction history** for each account
- ✅ **Consistent transfers** using database transactions with rollback
- 📈 **Scalable and highly available** deployment behind a load balancer
- 📊 **Monitoring, logging, and alerting** with CloudWatch
- 🕵️ **Account activity auditing** with CloudTrail

## 🏗️ Architecture

```
                     ┌──────────────┐
   User ───────────► │   Cognito    │  (Authentication)
     │               └──────────────┘
     ▼
┌─────────────────────────────┐
│ Application Load Balancer   │
└──────────────┬──────────────┘
               ▼
   ┌───────────────────────────┐
   │ Auto Scaling Group        │
   │  ┌─────────┐ ┌─────────┐  │
   │  │  EC2    │ │  EC2    │  │   (IAM roles attached)
   │  └─────────┘ └─────────┘  │
   └──────────────┬────────────┘
                  ▼
        ┌───────────────────┐
        │ Amazon RDS        │  (Encrypted with AWS KMS)
        │ Accounts & Txns   │
        └───────────────────┘

   CloudWatch  → Logs, metrics, alarms
   CloudTrail  → Account activity & audit trail
```

> 💡 Replace this diagram with your own architecture diagram image (e.g. `docs/architecture.png`) if you have one.

## ☁️ AWS Services Used

| Service | Purpose |
|---|---|
| **Amazon EC2** | Hosts the application servers |
| **Application Load Balancer (ALB)** | Distributes traffic across instances |
| **Auto Scaling** | Scales instances up/down based on demand |
| **Amazon RDS** | Stores customer account details and transaction records |
| **Amazon Cognito** | Customer sign-up, sign-in, and authentication |
| **AWS IAM** | Roles and permissions for secure access to AWS resources |
| **AWS KMS** | Encryption and data protection |
| **Amazon CloudWatch** | Application monitoring, logs, and alerts |
| **AWS CloudTrail** | Tracks AWS account activity for auditing |

## 🔒 Security Highlights

- **Authentication:** Users are authenticated through Amazon Cognito.
- **Least privilege:** IAM roles grant only the permissions each component needs.
- **Encryption:** AWS KMS is used for encryption and data protection.
- **Network isolation:** Resources are placed in a segmented network, with the database kept away from direct public access.
- **Auditability:** CloudTrail records account activity for review and compliance-style auditing.

## 🧾 Data Consistency

Fund transfers use **database transactions** so that debit and credit operations either both succeed or both fail. If anything goes wrong mid-transfer, the transaction is **rolled back**, preventing partial updates and keeping account balances accurate.

## 📊 Monitoring & Auditing

- **CloudWatch** collects application logs and metrics, and triggers alerts when thresholds are breached.
- **CloudTrail** keeps a record of API calls and account activity across the AWS account.

## 🚀 Getting Started

### Prerequisites

- An AWS account
- AWS CLI configured (`aws configure`)
- Basic knowledge of EC2, RDS, and IAM

### Setup Steps

1. **Network:** Create a VPC with public and private subnets.
2. **Database:** Launch an Amazon RDS instance in a private subnet with KMS encryption enabled.
3. **Authentication:** Create a Cognito User Pool and App Client.
4. **IAM:** Create an IAM role for EC2 with least-privilege permissions and attach it to a launch template.
5. **Compute:** Create a Launch Template and an Auto Scaling Group for the EC2 instances.
6. **Load balancing:** Create an Application Load Balancer and register the Auto Scaling Group as its target.
7. **Application:** Deploy the application code and configure environment variables (RDS endpoint, Cognito IDs).
8. **Monitoring:** Enable CloudWatch logs, alarms, and CloudTrail.

### Environment Variables

```env
DB_HOST=<rds-endpoint>
DB_NAME=<database-name>
DB_USER=<db-username>
DB_PASSWORD=<store-in-secrets-manager-or-parameter-store>
COGNITO_USER_POOL_ID=<user-pool-id>
COGNITO_CLIENT_ID=<app-client-id>
AWS_REGION=<region>
```

> Never commit real credentials to GitHub.

## 📁 Project Structure

```
secure-banking-aws/
├── app/                # Application source code
├── database/           # Schema and SQL scripts
├── docs/               # Architecture diagram and screenshots
└── README.md
```

> Update this to match your actual repository layout.

## 🖼️ Screenshots

Add screenshots of the login page, balance enquiry, transfer flow, transaction history, and CloudWatch dashboard here.

## 🔮 Future Improvements

- Multi-factor authentication (MFA) with Cognito
- Multi-AZ RDS deployment for higher availability
- AWS WAF in front of the load balancer
- Infrastructure as Code with CloudFormation or Terraform
- CI/CD pipeline for automated deployments

## 👤 Author

**Gokulan A**
Aspiring Cloud Engineer | B.Sc Information Technology, Madurai Kamaraj University
AWS Certified Solutions Architect (Coursera)

---

⭐ If you found this project helpful, consider giving it a star!
