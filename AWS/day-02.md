# ☁️ AWS Dashboard, Regions, Availability Zones & EC2

## 📌 Overview

In this session, we will learn the basics of **Amazon Web Services (AWS)** and understand how to launch our first **Ubuntu EC2 instance**.

### Topics Covered

* Introduction to AWS Dashboard
* AWS Region
* Availability Zone (AZ)
* Introduction to EC2
* EC2 Instance
* Creating the first Ubuntu EC2 Instance

---

# 🖥️ 1. Introduction to AWS Dashboard

The **AWS Management Console** is a web-based interface that allows us to access and manage AWS services.

From the AWS Dashboard, we can create and manage services such as:

* EC2
* S3
* RDS
* VPC
* IAM
* Lambda
* CloudWatch
* EKS
* Route 53

### AWS Management Console

After logging into AWS, we can access the AWS Management Console.

The console provides:

* AWS Services
* Recently visited services
* Search bar
* Region selection
* Account information
* Billing information
* Resource information

---

# 🌍 2. AWS Region

An **AWS Region** is a geographical location where AWS has multiple data centers.

Examples:

* Mumbai → `ap-south-1`
* Singapore → `ap-southeast-1`
* N. Virginia → `us-east-1`
* Ireland → `eu-west-1`

### Example

If we select:

```text
Mumbai Region
```

The AWS services we create will generally be created in:

```text
ap-south-1
```

### Why do we need Regions?

Regions help us:

* Reduce network latency
* Choose a location closer to users
* Meet data residency requirements
* Improve application availability
* Deploy applications in different geographical locations

### Example

Suppose our users are mainly located in India.

We can deploy our application in:

```text
Mumbai Region
ap-south-1
```

This can provide lower latency compared to deploying the application in a region far away from India.

---

# 🏢 3. Availability Zone (AZ)

An **Availability Zone**, or **AZ**, is one or more physically separate data centers inside an AWS Region.

A Region contains multiple Availability Zones.

### Example

Mumbai Region:

```text
ap-south-1
│
├── ap-south-1a
├── ap-south-1b
└── ap-south-1c
```

So:

```text
Region
   ↓
Multiple Availability Zones
   ↓
Data Centers
```

### Region vs Availability Zone

| Region                           | Availability Zone                              |
| -------------------------------- | ---------------------------------------------- |
| Geographical location            | Isolated location inside a Region              |
| Contains multiple AZs            | Belongs to a Region                            |
| Example: Mumbai                  | Example: ap-south-1a                           |
| Used for geographical deployment | Used for high availability and fault isolation |

### Simple Example

Think of a **Region as a city**.

Availability Zones are like **different buildings in that city**.

If one building has a problem, other buildings can continue operating.

---

# 🔄 Region vs Availability Zone

```text
AWS
│
├── Mumbai Region
│      │
│      ├── Availability Zone 1
│      │
│      ├── Availability Zone 2
│      │
│      └── Availability Zone 3
│
└── Singapore Region
       │
       ├── Availability Zone 1
       ├── Availability Zone 2
       └── Availability Zone 3
```

### Key Point

> **Region = Geographical Location**

> **Availability Zone = Isolated location within a Region**

---

# 🖥️ 4. Introduction to Amazon EC2

**EC2** stands for:

> **Elastic Compute Cloud**

Amazon EC2 provides **virtual servers in the AWS Cloud**.

We can use EC2 to run:

* Websites
* Applications
* Backend servers
* Databases
* Docker containers
* Jenkins
* Kubernetes components
* Development environments

---

# 🖥️ 5. What is an EC2 Instance?

An **EC2 Instance** is a virtual server running in AWS.

Instead of purchasing a physical server, we can create a virtual server using EC2.

### Traditional Server

```text
Buy Physical Server
       ↓
Install OS
       ↓
Configure Network
       ↓
Install Applications
       ↓
Run Application
```

### AWS EC2

```text
Choose Instance Type
       ↓
Choose Operating System
       ↓
Configure Network
       ↓
Launch Instance
       ↓
Connect to Server
```

This makes infrastructure provisioning much faster.

---

# ⚙️ 6. Important EC2 Components

When creating an EC2 instance, we need to understand several important options.

## 1. AMI

**AMI** stands for:

> Amazon Machine Image

An AMI contains the information required to launch an EC2 instance.

Examples:

* Ubuntu
* Amazon Linux
* Windows Server
* Red Hat
* SUSE

For this lab, we will use:

```text
Ubuntu
```

---

## 2. Instance Type

Instance type determines the computing resources available to our server.

It mainly defines:

* CPU
* Memory
* Network performance
* Instance capabilities

Example:

```text
t3.micro
t3.small
t3.medium
```

For learning purposes, we can select an eligible **Free Tier-eligible instance type** available in our account/region.

---

## 3. Key Pair

A **Key Pair** is used to securely connect to an EC2 instance.

It consists of:

```text
Public Key
Private Key
```

The public key is placed on the EC2 instance.

The private key is downloaded by the user and should be kept secure.

For Linux/macOS, the private key is commonly used with SSH:

```bash
ssh -i my-key.pem ubuntu@<PUBLIC-IP>
```

> ⚠️ Never share your private key with anyone.

---

## 4. Security Group

A **Security Group** acts as a virtual firewall for an EC2 instance.

It controls which traffic is allowed to reach the instance.

Example rules:

| Protocol | Port | Purpose             |
| -------- | ---: | ------------------- |
| SSH      |   22 | Remote Linux access |
| HTTP     |   80 | Web traffic         |
| HTTPS    |  443 | Secure web traffic  |

For our Ubuntu server, we usually need:

```text
SSH → Port 22
```

---

## 5. Storage

EC2 instances use storage such as **EBS (Elastic Block Store)**.

Storage is used for:

* Operating System
* Application files
* Logs
* Configuration files
* User data

Example:

```text
Root Volume → 8 GB
```

The exact size depends on the requirements of the application.

---

# 🚀 7. Create Your First Ubuntu EC2 Instance

Now let's create our first EC2 instance.

## Step 1: Login to AWS

Open the AWS Management Console and log in to your AWS account.

---

## Step 2: Select Region

From the AWS Console, select the required Region.

For example:

```text
Asia Pacific (Mumbai)
ap-south-1
```

> Always check the selected Region before creating resources.

---

## Step 3: Open EC2

Search for:

```text
EC2
```

Open the **EC2 service**.

---

## Step 4: Launch Instance

Click:

```text
Launch instance
```

---

## Step 5: Enter Instance Name

Provide a name for the instance.

Example:

```text
ubuntu-server
```

---

## Step 6: Select AMI

Under **Application and OS Images**, select:

```text
Ubuntu
```

Choose an appropriate supported Ubuntu AMI.

---

## Step 7: Select Instance Type

Choose an instance type suitable for learning.

Example:

```text
t3.micro
```

> The available Free Tier benefits and eligible instance types depend on your AWS account and current AWS terms. Always verify the pricing/free-tier eligibility shown in your console.

---

## Step 8: Create or Select Key Pair

Create a new key pair if you don't already have one.

Example:

```text
Key pair name:
ubuntu-key
```

Download the private key file.

For example:

```text
ubuntu-key.pem
```

### Important

Keep the `.pem` file safe.

Do not upload it to:

* GitHub
* Public websites
* Chat groups
* Shared drives

---

# 🔐 8. Configure Security Group

Create or select a security group.

Allow:

```text
SSH
Port: 22
```

For learning purposes, SSH access may be temporarily allowed from your current IP address.

### Recommended

Use:

```text
My IP
```

instead of:

```text
Anywhere 0.0.0.0/0
```

when possible.

---

# 💾 9. Configure Storage

For a basic Ubuntu learning server, the default storage configuration may be sufficient.

Example:

```text
Root Volume
8 GiB
gp3
```

---

# 🚀 10. Launch Instance

Review the configuration.

Then click:

```text
Launch instance
```

AWS will create the EC2 instance.

---

# 🔎 11. Check EC2 Instance

Go to:

```text
EC2 → Instances
```

You should see your instance.

Example:

```text
Name: ubuntu-server
Instance State: Running
Instance Type: t3.micro
Public IPv4 Address: xx.xx.xx.xx
```

---

# 🔑 12. Connect to Ubuntu EC2 Instance

Select the instance and click:

```text
Connect
```

Choose:

```text
SSH Client
```

AWS will show the SSH connection instructions.

---

## Linux/macOS

First, move to the directory containing your key:

```bash
cd ~/Downloads
```

Change the key permissions:

```bash
chmod 400 ubuntu-key.pem
```

Then connect:

```bash
ssh -i ubuntu-key.pem ubuntu@<PUBLIC-IP>
```

Example:

```bash
ssh -i ubuntu-key.pem ubuntu@13.234.XX.XX
```
---

# 🛑 15. Stop or Terminate the Instance

When you finish your practical, always check your EC2 resources.

### Stop

Stopping an instance shuts down the instance while preserving its configuration and attached EBS volumes.

You can start it again later.

```text
Instance
   ↓
Stop instance
```

### Terminate

Terminating an instance permanently removes the instance.

```text
Instance
   ↓
Terminate instance
```

> ⚠️ Be careful with **Terminate** because it is not the same as Stop.

---

# 💡 Important Points to Remember

* **AWS Region** represents a geographical location.
* **Availability Zone** is an isolated location within a Region.
* A Region contains multiple Availability Zones.
* **EC2** provides virtual compute servers.
* An **EC2 Instance** is a virtual server.
* **AMI** defines the operating system and initial software configuration.
* **Instance Type** determines CPU, memory, and other compute characteristics.
* **Key Pair** is used for secure authentication.
* **Security Group** works as a virtual firewall.
* **EBS** provides persistent block storage for EC2.
* **SSH uses port 22** by default.
* Always check your AWS Region before creating resources.
* Stop or terminate unused resources to avoid unexpected charges.
