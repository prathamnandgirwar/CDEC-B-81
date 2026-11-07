# 📦 AWS EBS (Elastic Block Store) – Complete Guide

---

# 📌 What is Amazon EBS?

Amazon Elastic Block Store (EBS) provides **persistent block storage** for use with Amazon EC2 instances.

EBS volumes are:

- ✅ Highly Available  
- ✅ Reliable  
- ✅ Scalable  
- ✅ Persistent (Data remains even after instance stop)  

### Common Use Cases

- Boot (Root) Volume
- Database Storage
- Application Storage
- File Storage for EC2

---

# 📊 Types of EBS Volumes

## 1️⃣ General Purpose SSD (gp3, gp2)

- Balanced price and performance
- Suitable for:
  - Boot volumes
  - Dev/Test environments
  - Low-latency applications
- gp3 offers:
  - Predictable IOPS
  - Lower cost than gp2
  - Separate control of IOPS and throughput

**Best for:** Most common workloads

---

## 2️⃣ Provisioned IOPS SSD (io1, io2)

- Designed for I/O intensive applications
- Very high performance
- High durability
- Supports Multi-Attach

Suitable for:
- MySQL
- PostgreSQL
- Oracle
- Enterprise databases

**Best for:** Production databases & mission-critical apps

---

## 3️⃣ Throughput Optimized HDD (st1)

- Low-cost HDD
- Designed for frequently accessed data
- High throughput workloads

Examples:
- Big Data
- Log Processing
- Data Warehousing

---

## 4️⃣ Cold HDD (sc1)

- Lowest cost HDD
- For infrequently accessed data

Examples:
- Backups
- Archive storage

---

## 5️⃣ Magnetic (Standard)

- Previous generation
- Suitable for infrequently accessed workloads

---

# 🔧 Practical: Attach, Partition, Format & Mount EBS Volume

---

# 🖥️ Step 1: Attach EBS Volume to EC2

1. Go to AWS Console  
2. Open **EC2 Dashboard**  
3. Click **Volumes**  
4. Select the volume  
5. Click **Actions → Attach Volume**  
6. Choose your EC2 instance  
7. Click **Attach**

---

# 🔍 Step 2: Connect to EC2

```bash
ssh ubuntu@<your-public-ip>
```

---

# 📂 Step 3: Verify Attached Disk

```bash
lsblk
```

Example Output:

```bash
nvme0n1   100G   # Root Volume
nvme1n1   10G    # New EBS Volume
```

---

# 🧩 Step 4: Create Partition

```bash
sudo fdisk /dev/nvme1n1
```

Inside fdisk:

```
n     → new partition
p     → primary
1     → partition number
Enter → default first sector
Enter → default last sector
w     → write changes
```

Verify:

```bash
lsblk
```

Now you should see:

```
nvme1n1p1
```

---

# 💾 Step 5: Format the Partition

```bash
sudo mkfs.ext4 /dev/nvme1n1p1
```

Explanation:
- `mkfs` = Make File System
- `ext4` = Linux file system
- `/dev/nvme1n1p1` = Partition name

---

# 📁 Step 6: Create Mount Directory

```bash
sudo mkdir /mnt/ebs-volume
```

---

# 🔗 Step 7: Mount the Volume

```bash
sudo mount /dev/nvme1n1p1 /mnt/ebs-volume
```

---

# ✅ Step 8: Verify Mount

```bash
df -h
```

You should see:

```
/dev/nvme1n1p1 mounted on /mnt/ebs-volume
```

---

# 🔁 Step 9: Make Mount Persistent (After Reboot)

By default, mount disappears after reboot.

---

## Get UUID

```bash
sudo blkid /dev/nvme1n1p1
```

Example:

```
UUID=""
```

---

## Edit fstab File

```bash
sudo nano /etc/fstab
```

Add this line at bottom:

```
UUID=   /mnt/ebs-volume   ext4   defaults,nofail   0   2
```

---

## Test Configuration

```bash
sudo mount -a
```

If no error appears → Configuration is correct ✅

---

# 📋 Important Commands Summary

| Task | Command |
|------|----------|
| Check Disks | `lsblk` |
| Create Partition | `fdisk /dev/nvme1n1` |
| Format | `mkfs.ext4 /dev/nvme1n1p1` |
| Create Directory | `mkdir /mnt/ebs-volume` |
| Mount | `mount /dev/nvme1n1p1 /mnt/ebs-volume` |
| Verify Mount | `df -h` |
| Get UUID | `blkid` |
| Persistent Mount | `/etc/fstab` |

---

# 🚀 Complete Workflow

1. Create EBS Volume  
2. Attach to EC2  
3. Connect via SSH  
4. Verify using `lsblk`  
5. Create Partition  
6. Format Partition  
7. Create Mount Directory  
8. Mount Volume  
9. Configure `/etc/fstab` for persistence  

---

# 🎯 Final Result

Your EBS volume is:

- Properly attached
- Partitioned
- Formatted
- Mounted
- Persistent after reboot

Now your EC2 instance is ready to store additional data safely.
