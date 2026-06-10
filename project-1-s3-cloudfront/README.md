# Project 1: Static Website Hosting on AWS S3 + CloudFront

## Overview
Hosted a static portfolio website on Amazon S3, delivered globally 
through CloudFront CDN with HTTPS enabled — without managing 
a single server.

---

## Architecture
---

## AWS Services Used

| Service | Purpose |
|---|---|
| Amazon S3 | Static file storage and website hosting |
| Amazon CloudFront | CDN for global delivery and HTTPS |
| AWS IAM | Secure CLI access with least-privilege user |

---

## What I Built

- Created an S3 bucket configured for static website hosting
- Applied a bucket policy to allow public read access
- Uploaded HTML files (index.html and error.html)
- Created a CloudFront distribution pointing to the S3 website endpoint
- Configured HTTP → HTTPS redirect at the CloudFront level
- Troubleshot and resolved a 504 Gateway Timeout caused by 
  incorrect origin domain configuration

---

## Real-World Problem I Solved

**Issue:** CloudFront returned a 504 Gateway Timeout error on first deployment

**Root Cause:** The CloudFront origin was pointed to the S3 REST 
endpoint instead of the S3 static website endpoint

**Fix:**
- Retrieved the correct website endpoint from S3 → Properties 
  → Static website hosting
- Updated the CloudFront origin domain to use the website endpoint
- Created a cache invalidation (`/*`) to clear stale configuration
- Confirmed resolution by successfully loading the site

**Lesson:** CloudFront requires the S3 *website* endpoint 
(not the REST endpoint) to correctly serve index.html as 
the root document

---

## Screenshots

### Live Website via CloudFront
![Website Screenshot](screenshots/website.png)

### CloudFront Distribution Settings
![CloudFront Screenshot](screenshots/cloudfront.png)

### S3 Bucket Configuration
![S3 Screenshot](screenshots/s3-bucket.png)

---

## Security Practices Applied

- Root account not used — dedicated IAM user created for CLI access
- IAM user follows least-privilege principles
- HTTPS enforced via CloudFront viewer protocol policy
- Billing alarm configured to monitor unexpected charges

---

## Key Learnings

- S3 static website hosting requires the website endpoint 
  (not REST endpoint) when used as a CloudFront origin
- CloudFront cache invalidation is required after origin changes
- HTTPS can be enabled without managing SSL certificates manually 
  — CloudFront handles it natively
- Real-world debugging requires checking each layer independently 
  (S3 → CloudFront → Browser)

---



## 📅 Date Completed
June 2026
