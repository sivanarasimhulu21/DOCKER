# 🐳 Docker Environment Setup on AWS EC2

This document explains how to set up Docker on an **AWS EC2 instance**, from account creation to container execution.  

---

## 🌐 Step 1: Create and Log in to Your AWS Account
1. Go to [https://aws.amazon.com/](https://aws.amazon.com/).
2. Click **Create an AWS Account**.
3. Enter your email, password, and billing details.
4. Once logged in, go to **AWS Management Console**.
5. Search for **EC2** → **Launch Instance**.

### ✅ Instance Configuration:
- **Name:** Docker-Setup
- **AMI (OS):** Ubuntu Server 22.04 LTS
- **Instance Type:** t2.micro (Free Tier)
- **Storage:** 8 GB (default)
- **Key Pair:** Create and download `.pem` file
- **Security Group:** Allow ports `22` (SSH) and `8080` (for web app access)

Click **Launch Instance** 🚀

---

## 🔐 Step 2: Connect to EC2 Instance
From your terminal:
```bash
chmod 400 my-key.pem
ssh -i "my-key.pem" ubuntu@<EC2-PUBLIC-IP>
