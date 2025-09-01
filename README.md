# 🌐 Static Website CI/CD with Jenkins, S3 & CloudFront 🚀

![Jenkins](https://img.shields.io/badge/Jenkins-CI/CD-blue?logo=jenkins)
![AWS S3](https://img.shields.io/badge/AWS-S3-orange?logo=amazon-aws)
![CloudFront](https://img.shields.io/badge/AWS-CloudFront-purple?logo=amazon-aws)
![Status](https://img.shields.io/badge/Status-Deployed-success)

---

## 📌 Project Overview

This project demonstrates a **fully automated CI/CD pipeline** for deploying a static website using:

- 🧾 **HTML/CSS frontend**
- ⚙️ **Jenkins CI/CD**
- ☁️ **Amazon S3 (Static Website Hosting)**
- 🌍 **Amazon CloudFront (CDN)**

Every push to the `main` branch triggers Jenkins to:
1. Checkout the latest code
2. Upload website files to S3
3. Invalidate CloudFront cache to reflect updates globally

---

## 🧱 Tech Stack

| Tool        | Purpose                     |
|-------------|-----------------------------|
| `HTML/CSS`  | Static site frontend         |
| `Git & GitHub` | Version control & repo |
| `Jenkins`   | CI/CD automation             |
| `AWS S3`    | Static website hosting       |
| `AWS CloudFront` | CDN for global delivery |
| `Terraform` | Infrastructure as Code (optional) |

---

## 🛠️ Jenkins Pipeline Stages

```groovy
pipeline {
  agent any
  stages {
    stage('📥 Checkout Code') {...}
    stage('🔐 Configure AWS Credentials') {...}
    stage('🧹 Clean Up Unwanted Files') {...}
    stage('📤 Upload Static Site to S3') {...}
    stage('🌀 Invalidate CloudFront Cache') {...}
    stage('✅ Deployment Successful') {...}
  }
}
```

---

## 🔁 CI/CD Flow

```
GitHub → Jenkins → S3 (sync files)
                      ↓
                  CloudFront (fetch + cache)
                      ↓
                🌍 Fast Global Access
```

---

## 🚀 Live Deployment

| Service      | Link |
|--------------|------|
| **S3 URL**   | `http://vin-static-site-86673444.s3-website-us-east-1.amazonaws.com` |
| **CloudFront CDN** | `https://<your-distribution-id>.cloudfront.net` (Add once DNS is ready) |

---

## 📂 Folder Structure

```
vin-static-site/
│
├── index.html
├── 404.html
├── assets/
│   └── style.css
├── terraform/
│   └── (infra files for S3, IAM, CloudFront)
├── Jenkinsfile
└── README.md
```

---


## 📸 Screenshots

### Jenkins Stages:
![Jenkins stages](https://github.com/Vin22-03/Day16_static_site_CICD/blob/main/jenkins%20latest.png?raw=true)

### Final Website:
![Website](https://github.com/Vin22-03/Day16_static_site_CICD/blob/main/final.png?raw=true)


---

## ✍️ Author

**VinCloudOps**  
🔗 [GitHub](https://github.com/Vin22-03) | 🌐 [vincloudops.tech](https://vincloudops.tech)

---

## ⭐️ If you like this project, give it a star!

---

## 📌 Next Upgrade Ideas

- [ ] Add custom domain via Route 53
- [ ] Enable HTTPS with ACM + CloudFront
- [ ] Add monitoring with CloudWatch
