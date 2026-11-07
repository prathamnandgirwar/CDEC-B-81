# 🪟 Create a Windows EC2 Instance on AWS

## 📌 Overview

In this practical, we will create a **Windows Server EC2 instance** on AWS and connect to it using **RDP (Remote Desktop Protocol)**.

### Topics Covered

* Create Windows EC2 Instance
* Configure Key Pair
* Configure Security Group
* Allow RDP
* Configure 30 GB Storage
* Connect to Windows Server using RDP
* Retrieve Windows Administrator Password

---

# 🚀 1. Create Windows EC2 Instance

Login to the AWS Management Console and open:

```text
EC2 → Instances → Launch Instance
```

---

## Step 1: Name the Instance

Enter a suitable name.

Example:

```text
windows-server
```

---

## Step 2: Select AMI

Under **Application and OS Images**, select a Windows Server AMI.

For example:

```text
Windows Server
```

The exact Windows Server version available may vary.

---

## Step 3: Select Instance Type

Choose an appropriate instance type based on your requirements.

For learning purposes, select an instance type that is eligible for the benefits available to your AWS account.

Example:

```text
t3.micro
```

> Check the AWS Console for current pricing and eligibility before launching.

---

# 🔐 Step 4: Create or Select Key Pair

Under **Key Pair**, create a new key pair if you don't already have one.

Example:

```text
windows-key
```

Download the private key file.

Example:

```text
windows-key.pem
```

### ⚠️ Important

Keep your private key safe.

Do not:

* Share it with others
* Upload it to GitHub
* Send it in public groups
* Delete it before retrieving the Windows password

---

# 🔥 Step 5: Configure Security Group

A **Security Group** acts as a virtual firewall for the EC2 instance.

For Windows remote access, we need:

```text
RDP
Port: 3389
```

### Check RDP Rule

Go to the Security Group configuration and verify:

```text
Inbound Rules
    ↓
RDP
    ↓
TCP
    ↓
Port 3389
```

If RDP is not allowed, add an inbound rule:

```text
Type: RDP
Protocol: TCP
Port: 3389
Source: My IP
```

### Recommended

Whenever possible, use:

```text
My IP
```

instead of allowing:

```text
0.0.0.0/0
```

because opening RDP to the entire internet increases security risk.

---

# 💾 Step 6: Configure Storage

Configure the root volume.

For this practical, use:

```text
Root Volume: 30 GB
```

Example:

```text
Volume Type: gp3
Size: 30 GiB
```

---

# 🚀 Step 7: Launch the Instance

Review all configurations:

```text
Name
AMI
Instance Type
Key Pair
Security Group
Storage
```

Then click:

```text
Launch Instance
```

Wait until the instance state becomes:

```text
Running
```

---

# 🖥️ 2. Connect to Windows EC2 Instance

Select your Windows EC2 instance.

Click:

```text
Connect
```

You will see different connection options.

Select:

```text
RDP Client
```

---

# 📥 Step 1: Download Remote Desktop File

Under the RDP Client section, click:

```text
Download Remote Desktop File
```

A file will be downloaded to your local machine.

It will generally have an `.rdp` extension.

Example:

```text
windows-server.rdp
```

---

# 🔑 Step 2: Get Windows Administrator Password

To connect to the Windows server, we need the Administrator password.

Go to:

```text
EC2
→ Instances
→ Select Windows Instance
→ Connect
→ RDP Client
→ Get Password
```

---

# 🔐 Step 3: Upload Private Key

Click:

```text
Upload private key file
```

Select the private key that you downloaded earlier.

Example:

```text
windows-key.pem
```

Then click:

```text
Decrypt Password
```

AWS will display the Windows Administrator password.

---

# 📋 Step 4: Copy the Password

Copy the generated Administrator password.

Example:

```text
Username:
Administrator

Password:
<generated-password>
```

Keep the password secure.

---

# 🖥️ Step 5: Open RDP File

Go to the location where the `.rdp` file was downloaded.

Example:

```text
Downloads/
└── windows-server.rdp
```

Double-click the `.rdp` file.

The Remote Desktop Connection window will appear.

---

# 🔑 Step 6: Enter Password

When prompted:

```text
Username:
Administrator
```

Enter the password obtained from AWS.

Click:

```text
OK
```

You should now be connected to your Windows EC2 instance.

---

# 🎯 Windows EC2 Architecture

```text
AWS Cloud
    │
    └── EC2
         │
         └── Windows Server
                │
                ├── Security Group
                │      └── RDP → 3389
                │
                ├── Key Pair
                │
                └── 30 GB EBS Volume
                         │
                         ↓
                   Remote Desktop
                         │
                         ↓
                  Your Local Machine
```

---
# 🌐 Host a CSS/HTML Template Using Nginx on Ubuntu EC2

## 📌 Overview

In this practical, we will deploy a **static HTML/CSS website** on an Ubuntu EC2 server using the **Nginx web server**.

We will:

* Launch an Ubuntu EC2 instance
* Connect to the server
* Install Nginx
* Copy website files from local machine to EC2
* Configure Nginx
* Access the website using the EC2 Public IP

---

# 🏗️ Architecture

```text
Your Local Machine
       │
       │ SCP
       ↓
Ubuntu EC2 Instance
       │
       ├── Nginx
       │
       └── /var/www/html/
                │
                └── HTML/CSS Template
                         │
                         ↓
                    Web Browser
                         │
                         ↓
                  Public IP : 80
```

---

# 🚀 Step 1: Launch Ubuntu EC2 Instance

Create an Ubuntu EC2 instance.

Use:

```text
AMI: Ubuntu
Instance Type: Suitable learning instance
Key Pair: Your SSH key
```

---

# 🔐 Step 2: Configure Security Group

We need SSH and HTTP access.

### SSH

```text
Type: SSH
Port: 22
Source: My IP
```

SSH is required to connect to the Ubuntu server.

### HTTP

```text
Type: HTTP
Port: 80
Source: 0.0.0.0/0
```

HTTP port 80 is required so that users can access our website through a browser.

---

# 🖥️ Step 3: Connect to Ubuntu EC2

After launching the instance, copy its **Public IPv4 Address**.

Example:

```text
13.234.XX.XX
```

Open your local terminal.

Navigate to the directory containing your private key.

Example:

```bash
cd ~/Downloads
```

Connect to the server:

```bash
ssh -i key-name.pem ubuntu@<PUBLIC-IP>
```

Example:

```bash
ssh -i ubuntu-key.pem ubuntu@13.234.XX.XX
```

---

# 📁 Step 4: Prepare Your Website Template

On your **local machine**, make sure your HTML/CSS template folder exists.

Example:

```text
Downloads/
│
├── ubuntu-key.pem
│
└── template/
    ├── index.html
    ├── css/
    ├── js/
    ├── images/
    └── assets/
```

The `template` folder contains the website files.

---

# 📤 Step 5: Copy Template to EC2 Using SCP

We can use the `scp` command to securely copy files from our local machine to the EC2 server.

### SCP Syntax

```bash
scp -i <key-file> -r <folder> ubuntu@<public-ip>:/home/ubuntu/
```

Example:

```bash
scp -i ubuntu-key.pem -r template ubuntu@13.234.XX.XX:/home/ubuntu/
```

### Meaning

```text
scp
```

Securely copies files between systems.

```text
-i ubuntu-key.pem
```

Specifies the private key.

```text
-r
```

Copies the directory recursively.

```text
template
```

The local website folder.

```text
ubuntu@13.234.XX.XX
```

The Ubuntu EC2 user and server IP.

```text
/home/ubuntu/
```

The destination directory on the EC2 server.

---

# 🔎 Step 6: Verify the Template on EC2

Connect to the EC2 instance:

```bash
ssh -i ubuntu-key.pem ubuntu@<PUBLIC-IP>
```

Check the files:

```bash
ls
```

You should see:

```text
template
```

Go inside the directory:

```bash
cd template
```

Check its contents:

```bash
ls
```

Example:

```text
index.html
css
js
images
assets
```

---

# 🌐 Step 7: Install Nginx

Update the Ubuntu package repository:

```bash
sudo apt update
```

Install Nginx:

```bash
sudo apt install nginx -y
```

Check Nginx status:

```bash
sudo systemctl status nginx
```

You should see:

```text
active (running)
```

---

# 📂 Step 8: Understand Nginx Web Directory

The default Nginx website is generally served from:

```text
/var/www/html/
```

List the directory:

```bash
ls /var/www/html/
```

You may see:

```text
index.nginx-debian.html
```

This is the default Nginx page.

---

# 🗑️ Step 9: Remove Default Nginx Page

Remove the default HTML file:

```bash
sudo rm /var/www/html/index.nginx-debian.html
```

Check the directory:

```bash
ls /var/www/html/
```

The default page should now be removed.

---

# 📋 Step 10: Copy Template to Nginx Web Directory

Now copy the website files from your template directory to:

```text
/var/www/html/
```

For example:

```bash
sudo cp -r /home/ubuntu/template/* /var/www/html/
```

Verify:

```bash
ls -la /var/www/html/
```

You should see your website files.

Example:

```text
index.html
css/
js/
images/
assets/
```

---

# 🔍 Step 11: Verify index.html

Make sure your template contains an:

```text
index.html
```

Run:

```bash
ls /var/www/html/
```

Expected:

```text
index.html
css
js
images
```

Nginx will normally serve `index.html` as the default page.

---

# 🔄 Step 12: Restart Nginx

Restart Nginx:

```bash
sudo systemctl restart nginx
```

Check the status:

```bash
sudo systemctl status nginx
```

Expected:

```text
active (running)
```

---

# 🌍 Step 13: Access the Website

Copy the **Public IPv4 Address** of your EC2 instance.

Example:

```text
13.234.XX.XX
```

Open your browser and enter:

```text
http://13.234.XX.XX
```

Or:

```text
http://<PUBLIC-IP>
```

Since HTTP uses port **80**, you normally don't need to explicitly write `:80`.

You can also use:

```text
http://13.234.XX.XX:80
```

Your HTML/CSS website should now be visible in the browser.

---


---
# 🔑 One-Line Summary

```text
Local HTML/CSS Template
        ↓
       SCP
        ↓
Ubuntu EC2
        ↓
Install Nginx
        ↓
/var/www/html/
        ↓
HTTP : 80
        ↓
Public IP
        ↓
Website 🌐
```
