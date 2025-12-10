# 🚀 Project 1: Static Website Hosting on AWS

## 📌 Overview
This project demonstrates how to host a secure, high-performance static website on AWS using a serverless architecture. By leveraging **Amazon S3** for storage, **Amazon CloudFront** for content delivery (caching), and **Amazon Route 53** for DNS management, this solution ensures low latency and high availability globally.

## 🏗️ Architecture
The architecture follows a standard static hosting pattern:

<img width="761" height="411" alt="Hosting static website using s3 drawio" src="https://github.com/user-attachments/assets/b275bae1-ed09-41a8-9e6d-527220a1671f" />

## 🛠️ Services Used
* **Amazon S3:** Object storage for hosting HTML, CSS, and JS files.
* **Amazon CloudFront:** Content Delivery Network (CDN) for caching and HTTPS.
* **Amazon Route 53:** DNS Web Service for domain registration and routing.
* **AWS Certificate Manager (ACM):** For provisioning free SSL/TLS certificates.

## 📋 Prerequisites
* An active AWS Account.
* A registered domain name (via Route 53 or external registrar)- `ismailoyeleke.com`
* Basic HTML/CSS files (`index.html`).

## ⚙️ Implementation Steps

### Step 1: Create an S3 Bucket
1. Navigate to the **S3 Console**.
2. Click **Create bucket**.
3. **Bucket Name:** Must match your domain name (e.g., `www.ismailoyeleke.com`).
4. **Region:** `us-east-1`.
5. **Public Access:** Uncheck "Block all public access" (Acknowledging the warning).
6. Click **Create bucket**.

### Step 2: Enable Static Website Hosting
1. Go to the **Properties** tab of your new bucket.
2. Scroll to **Static website hosting** and click **Edit**.
3. Select **Enable**.
4. **Index document:** `index.html`.
5. Save changes.

### Step 3: Upload Content
1. Upload your `index.html`, `style.css`, and other assets to the bucket.
2. Ensure the file permissions allow reading or configure the bucket policy (next step).

### Step 4: Configure Bucket Policy
To make the website public, add the following policy in the **Permissions** tab:

    {
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "PublicReadGetObject",
			"Effect": "Allow",
			"Principal": "*",
			"Action": "s3:GetObject",
			"Resource": "arn:aws:s3:::ismailoyeleke.com/*"
		}
	]
	}


### Step 5: Configure CloudFront (CDN)
1. Navigate to **CloudFront** and click **Create distribution**.
2. **Origin Domain:** Select your S3 bucket endpoint.
3. **Viewer Protocol Policy:** "Redirect HTTP to HTTPS".
4. **Custom SSL Certificate:** Request or import a certificate via ACM for your domain.
5. Create the distribution.

### Step 6: Configure DNS with Route 53
1. Go to **Route 53 > Hosted Zones**.
2. Create an **A Record**.
3. Toggle **Alias** to "Yes".
4. **Route traffic to:** Alias to CloudFront Distribution.
5. Select your distribution and create the record.

## 💡 Challenges & Learnings
* **DNS Propagation:** Learned that DNS changes can take up to 24 hours to propagate globally, though Route 53 is usually fast.
* **Caching:** Encountered an issue where updates to `index.html` weren't showing immediately. Solved this by creating a **CloudFront Invalidation** for `/*`.

## 🔮 Future Improvements
* **Security:** Implement **Origin Access Control (OAC)** to restrict S3 access so only CloudFront can view the files (disabling public S3 access).
* **CI/CD:** Automate the deployment using **GitHub Actions** to sync files to S3 automatically on push.

---
*Created by [Oyeleke Ismail](https://www.linkedin.com/in/ismail-oyeleke-6930b6317/) - AWS Solutions Architect*
