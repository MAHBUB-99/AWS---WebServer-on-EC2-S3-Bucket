# 🚀 Setup a Basic Web Server on EC2 & Host HTML on S3

### This guide will walk you through setting up an Nginx web server on an EC2 instance and optionally hosting your HTML file on AWS S3.

## ☁️ Part 1: Setting Up a Web Server on EC2

### 🔑 Step 0: Prepare Your SSH Key

Copy your key to your Linux home (from WSL):

```bash
cp /mnt/c/Users/ASUS/Downloads/_mahbub_.pem.pem ~/.ssh/mahbub.pem
```

Fix permissions:
```bash
chmod 400 ~/.ssh/mahbub.pem
```

Connect to your EC2 instance:
```bash
ssh -i ~/.ssh/mahbub.pem ubuntu@<your-ec2-public-ip>
```

### 🌐 Step 1: Update Package Repositories

Always start by updating your packages:
```bash
sudo apt update -y
```

This ensures you get the latest package info.

🛠️ Step 2: Install Nginx

Install the Nginx web server:
```bash
sudo apt install nginx -y
```

### ▶️ Step 3: Start the Web Server

Start Nginx:
```bash
sudo systemctl start nginx
```

(Optional) Enable Nginx to start on boot:
```bash
sudo systemctl enable nginx
```

Verify it’s running:
```bash
systemctl status nginx
```

You should see:
```bash
active (running)
```

### 📝 Step 4: Create a Simple HTML Page

Go to Nginx’s document root:
```bash
cd /var/www/html
```

Create and edit your index.html:
```bash
sudo nano index.html
```
Add the HTML content from **index.html**
Save and exit (Ctrl + X, then Y, then Enter).

### ✅ Step 5: Test Your Web Server

Open your web browser and enter your EC2 public IPv4:

```bash
http://<your-ec2-public-ip>
```

You should see index.html page styled nicely.

## ☁️ Part 2: Creating an S3 Bucket and Hosting the HTML File

Follow these steps to upload and host your HTML page on AWS S3.

---

### Step 1: Create an S3 Bucket

1. Navigate to the **S3** service in the AWS Management Console.  
2. Click **Create bucket**.  
3. Enter a **globally unique bucket name**.  
4. Select your preferred **AWS Region**.  
5. Keep default bucket settings.  
6. **Disable "Block all public access"**.  
7. Acknowledge the **public access warning**.

---

### Step 2: Upload the `index.html` File

1. Open your newly created S3 bucket.  
2. Click **Upload** → **Add files** → select `index.html` from your local machine.  
3. Click **Upload** to store the file in the bucket.

---

### Step 3: Make the Object Publicly Accessible

1. Select the uploaded `index.html` file.  
2. Go to **Permissions → Public access** → **Grant public read access**.  
3. Save changes.

or
### Add Bucket Policy

Go to your bucket → Permissions → Bucket policy, and add something like this:

```bash
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::mahbub-website-bucket/*"
        }
    ]
}
```

---

### Step 4: Access the HTML File from S3

1. Copy the **Object URL** of the uploaded file.  
2. Open your web browser and paste the URL.  
3. Verify that your HTML page is displayed.

> ✅ **Result:** Your static website is now live and publicly accessible via S3.


---

## 🙏 Thank You

Your feedback and contributions are always welcome.  
Happy hosting with AWS! 🚀

