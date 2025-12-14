# 🚀 Project 1: Static Website Hosting on AWS using S3, Route53, and CloudFront

## 📌 Project Overview
This project demonstrates how I hosted a static website on Amazon Web Services (AWS) using **Amazon S3** for storage, **Amazon CloudFront** for global content delivery, **Amazon Route 53** for DNS management, and **AWS Certificate Manager (ACM)** for secure HTTPS communication.

The solution is designed to be scalable, secure, highly available, and cost-effective, eliminating the need for traditional server management.

## 🔗 Live Demo
🚀 **Website URL:** [https://ismailoyeleke.com](https://ismailoyeleke.com)

## 🏗️ Architecture
The architecture follows a standard serverless hosting pattern:

<img width="559" height="239" alt="Architecture_P1_Static Website Hosting" src="https://github.com/user-attachments/assets/32ec5a86-1e1b-4c24-ae64-db4abbe64da9" />


## 🛠️ AWS Services Used
* **Amazon S3:** Storage and hosting of static website files.
* **Amazon CloudFront:** Global content delivery and HTTPS enforcement.
* **Amazon Route 53:** Domain registration and DNS routing.
* **AWS Certificate Manager (ACM):** SSL/TLS certificate management.

## ⚙️ Implementation Details

### Step 1: Create an S3 Bucket
I navigated to the Amazon S3 Console and created a new bucket with the name `ismailoyeleke.com`, matching my domain name.
* **Region:** `us-east-1` (N. Virginia).
* **Public Access:** Disabled "Block all public access" to allow global reach.

<img width="1920" height="1280" alt="1 bucket_created" src="https://github.com/user-attachments/assets/d7b3641c-46f4-4017-81dc-f58ef599d5aa" />


### Step 2: Enable Static Website Hosting
I enabled **Static Website Hosting** under the bucket properties and set `index.html` as the index document.

<img width="1920" height="1280" alt="2 enable static website hosting" src="https://github.com/user-attachments/assets/be9a0b33-7638-4e92-be0b-f659b82d7dc9" />


### Step 3: Upload Website Files
I uploaded all static website files, including `index.html`, `style.css`, and `script.js` files, into the S3 bucket.

<img width="1920" height="1280" alt="3 upload content" src="https://github.com/user-attachments/assets/00d92a7f-7157-49a2-a4ed-e3a5ac1030e5" />


### Step 4: Configure S3 Bucket Policy
To allow public read access, I configured the bucket policy using the JSON below. This allows users to access the website content publicly while maintaining controlled permissions.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::[ismailoyeleke.com/](https://ismailoyeleke.com/)*"
        }
    ]
}
```

<img width="1920" height="1280" alt="4 Bucket policy" src="https://github.com/user-attachments/assets/2a4c2366-296a-4a26-88c9-1768f1be3c7b" />


### Step 5: Register Domain & Create Hosted Zone
I purchased the domain `ismailoyeleke.com` using Amazon Route 53. After registration, I created a **Public Hosted Zone** for DNS management.


<img width="1920" height="1280" alt="5 Registered domain" src="https://github.com/user-attachments/assets/b2f1c278-1d30-4e52-8923-0768652b66a1" />

<img width="1920" height="1280" alt="6 Hosted zone" src="https://github.com/user-attachments/assets/5c3fc530-775e-4529-b60c-d804ae5ecb15" />


### Step 6: Configure CloudFront (CDN)
I created a CloudFront distribution to improve performance and security:
* **Origin Domain:** Selected the S3 website endpoint.
* **Viewer Protocol Policy:** Redirect HTTP to HTTPS.
* **Alternate Domain Name (CNAME):** Added `ismailoyeleke.com`.

<img width="1920" height="1280" alt="7 CloudFront Distribution" src="https://github.com/user-attachments/assets/4abcae07-cdfb-408e-9bd7-9c2d7c4cc802" />


### Step 7: Configure SSL Certificate
I requested a public SSL certificate in **AWS Certificate Manager (ACM)** for my domain. The certificate was validated using DNS validation via Route 53 and attached to the CloudFront distribution.

<img width="1920" height="1280" alt="8 Request Certificate" src="https://github.com/user-attachments/assets/623d79c8-f76f-4f89-a40f-837a5c3aa371" />


### Step 8: Configure Route 53 DNS Record
I created an **A Record** in Route 53 and configured it as an **Alias** pointing to the CloudFront distribution.
* **Record Type:** A - Routes traffic to an IPv4 address.
* **Route Traffic To:** Alias to CloudFront distribution.

<img width="1920" height="1280" alt="10 Create a record" src="https://github.com/user-attachments/assets/28c1169c-dfb5-47b5-8cee-ea39926397ad" />


### Step 9: Verify Website
I accessed the website using `https://ismailoyeleke.com` to confirm that HTTPS is enabled and content is delivered via CloudFront.

<img width="1920" height="1280" alt="11 website ready" src="https://github.com/user-attachments/assets/dd3bf5ee-40f8-4b33-8fff-54024070a93e" />


## 💡 Challenges & Solutions
During the implementation, I encountered a few real-world challenges:

* **⚠️ Challenge: CloudFront Caching Issues**
    * *Issue:* Updates to `index.html` were not immediately visible.
    * *Solution:* I created a **CloudFront Invalidation** (path `/*`) to refresh the cached content.

* **⚠️ Challenge: DNS Propagation**
    * *Issue:* DNS changes can take up to 24 hours to propagate globally.
    * *Solution:* I verified settings and waited for AWS Route 53 to resolve the changes.

* **⚠️ Challenge: Configuring SSL**
    * *Issue:* Securing a custom domain required validation.
    * *Solution:* I used AWS Certificate Manager with DNS validation through Route 53 for seamless integration.

## ✅ Project Outcome
I successfully deployed a production-ready static website accessible at **https://ismailoyeleke.com**. The site is secured with HTTPS, auto-scales to handle traffic spikes, and incurs minimal costs compared to traditional server-based hosting.


---
*Created by [Oyeleke Ismail](https://www.linkedin.com/in/ismail-oyeleke-6930b6317/) - AWS Certified Solutions Architect*
