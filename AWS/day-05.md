# 🚀 Amazon EC2: Comprehensive Guide

This README provides detailed information about **Amazon EC2**, covering:
- Dashboard Overview
- Instance Types
- Status Checks
- AMIs
- Launch Templates
- Purchasing Options  

---

# 📊 Amazon EC2 Dashboard Overview

The Amazon EC2 Dashboard provides a centralized interface to manage EC2 resources.

## 🔑 Key Components
- **Instances** → View and manage running instances  
- **Launch Instances** → Create new EC2 instances  
- **Instance Types** → Explore available instance types  
- **Elastic Block Store (EBS)** → Manage storage volumes  
- **Key Pairs** → Secure SSH access  
- **Security Groups** → Configure firewall rules  
- **Elastic IPs** → Allocate static public IPs  

---

# 🖥️ Instance Types

Amazon EC2 offers different instance categories based on workload needs:

## 🔹 General Purpose
- Balanced compute, memory, and storage  
- Examples: `M5`, `T2`, `T3`, `M6a`, `Mac2`

## 🔹 Compute Optimized
- Best for compute-heavy tasks  
- Examples: `C5`, `C6i`, `C7g`

## 🔹 Memory Optimized
- Ideal for high-performance databases  
- Examples: `R5`, `X1`, `X2idn`

## 🔹 Storage Optimized
- High read/write operations  
- Examples: `I3`, `D2`, `H1`

## 🔹 Accelerated Computing
- Uses GPUs / hardware accelerators  
- Examples: `P3`, `G5`, `Inf1`

## 🔹 High Performance Computing (HPC)
- Low latency & high performance  
- Examples: `Hpc6a`, `Hpc7g`

---

# ✅ Status Checks for EC2 Instances

## 🔍 Overview
Amazon EC2 continuously monitors instance health using automated checks.

## 🔹 Types of Status Checks

### 1️⃣ System Status Check
- Checks AWS infrastructure  
- Power failure  
- Hardware issues  
- Network issues  

### 2️⃣ Instance Status Check
- Checks inside OS  
- Memory exhaustion  
- File system corruption  
- Kernel issues  
- Network misconfiguration  

## ⚠️ Common Failure Causes
- Networking issues  
- Low memory  
- Corrupted file system  
- Kernel incompatibility  

## 📈 CloudWatch Alarms
- Monitor instance health  
- Trigger automated recovery actions  

---

# 📦 AMI (Amazon Machine Image)

## 🔹 Types of AMI
- **EBS-backed AMI** → Stored on Amazon EBS  
- **Instance-store AMI** → Stored on local storage  

## 🛠️ Creating an AMI
1. Go to EC2 Dashboard  
2. Select instance  
3. Click **Actions → Image → Create Image**  
4. Provide details and create  

## 🔁 Copying an AMI
- Copy AMIs across regions  
- Useful for redundancy & multi-region deployment  

---

# 📑 Launch Templates

Launch templates allow consistent configuration of EC2 instances.

## 🔹 Includes
- AMI ID  
- Instance Type  
- Security Groups  
- Key Pair  

## 🛠️ Steps to Create
1. Open EC2 Dashboard  
2. Go to **Launch Templates**  
3. Click **Create Launch Template**  
4. Fill required details  

---

# 💰 EC2 Purchasing Options

## 🔹 On-Demand
- Pay per usage  
- No commitment  
- Highest cost  
- Best for short-term workloads  

---

## 🔹 Reserved Instances
- Up to **72% discount**  
- 1 or 3-year commitment  
- Best for steady workloads  

### Types:
- Standard RI  
- Convertible RI (flexible, up to 66% discount)

---

## 🔹 Spot Instances
- Up to **90% cheaper**  
- Can be terminated anytime  
- Best for:
  - Batch jobs  
  - Data processing  
  - Flexible workloads  

---

## 🔹 Dedicated Hosts
- Physical server dedicated to you  
- Full control  
- Expensive  
- Used for:
  - Licensing  
  - Compliance  

---

## 🔹 Dedicated Instances
- Dedicated hardware (virtualized)  
- Less control than hosts  
- Extra cost  

---

## 🔹 Capacity Reservations
- Reserve capacity in a specific AZ  
- No discount  
- Pay even if unused  

---

# 🧠 How to Choose (Simple Analogy)

| Option | Example |
|------|--------|
| On-Demand | Book hotel anytime (pay full price) |
| Reserved | Book early → get discount |
| Spot | Bid for room → can be removed anytime |
| Dedicated Host | Book entire hotel |
| Capacity Reservation | Reserve room but pay even if unused |

---

# 📌 Summary

Amazon EC2 provides:
- Flexible compute options  
- Multiple pricing models  
- High scalability  
- Full control over infrastructure  

---

# 📚 References
- AWS EC2 Documentation  
- AWS Instance Types  
- AWS AMI Guide  

---
