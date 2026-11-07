# 📌 Introduction to NFS (Network File System)

---

## 🔹 What is NFS?

**NFS = Network File System**

NFS is a protocol that allows computers to share files over a network.

Think of it like **Google Drive or OneDrive**, but for servers inside a private network.

With NFS:
- You create one central storage location
- Multiple computers (clients) connect to it
- They use it like their own local disk

---

## 🔹 How Does NFS Work?

There are two main components:

### 🖥️ NFS Server
- Stores the actual data
- Shares a directory/folder

### 💻 NFS Clients
- Connect to the server
- Mount (attach) the shared folder
- Can read/write files like a normal directory

---

## 🔹 Real-Life Example

Imagine a company office:

- The **NFS Server** is like the office filing cabinet.
- Employees (clients) do not keep separate copies.
- Everyone opens the same cabinet drawer.
- If one person updates a file, everyone sees it instantly.

---

## 🔹 Key Features of NFS

- **Centralized Storage** – Files stored in one location  
- **Shared Access** – Multiple servers access same data  
- **Scalability** – Add more clients easily  
- **Transparency** – Looks like a normal folder to users  
- **Port 2049** – Default NFS communication port  
- Uses **TCP/UDP protocol**

---

## 🔹 Why Do We Need NFS?

Without NFS:
- Each server stores its own files
- Difficult to sync data
- Hard to scale applications

With NFS:
- All servers use the same storage
- Easy collaboration
- Easier scaling

### 📌 Common Use Cases

- Hosting website on multiple servers
- Shared logs
- Centralized backups
- Shared application data

In AWS:
- **Amazon EFS (Elastic File System)** is a managed NFS service.

---

# 🔹 Versions of NFS

| Version | Description |
|----------|-------------|
| NFSv2 | Old version, basic sharing |
| NFSv3 | Supports larger files, better performance |
| NFSv4 | More secure, supports encryption & ACLs |
| NFSv4.1 | Used by AWS EFS |

---

# 📌 NFS in AWS Context

## 🔹 Is NFS Region-specific or AZ-specific?

### ✅ NFS Protocol (General Linux NFS)
- Not tied to Region
- Not tied to AZ
- Depends only on network connectivity

### ✅ Amazon EFS (Managed NFS Service)

- **Region-specific**
- **Multi-AZ within that region**
- Highly available

Instances in different AZs of the same region can mount the same EFS.

---

## ✅ Quick Summary

- NFS protocol → Needs only network connectivity
- AWS EFS →
  - Region-specific
  - Multi-AZ inside that region

👉 In AWS terms:  
**EFS is regional but accessible from multiple AZs.**

---

# 📌 Practical: Create and Mount Amazon EFS (NFS)

---

# 🔹 Step 1: Create an EFS File System

1. Open AWS Console → EFS
2. Click **Create file system**
3. Configure:
   - Name: `my-efs`
   - Select VPC
   - Select multiple AZs (for high availability)
   - Attach Mount Targets
   - Configure Security Groups (Allow port 2049)
   - Choose Performance Mode (General Purpose / Max I/O)
   - Enable Encryption (Recommended)
4. Click **Create**

---

# 🔹 Step 2: Install NFS Utilities on EC2

### For Ubuntu/Debian

```bash
sudo apt-get update
sudo apt-get install -y nfs-common
```

### For Amazon Linux / RHEL / CentOS

```bash
sudo yum install -y amazon-efs-utils
sudo yum install -y nfs-utils
```

---

# 🔹 Step 3: Mount the EFS File System

## 1️⃣ Get File System ID

Example:

```
fs-12345678
```

---

## 2️⃣ Create Mount Directory

```bash
sudo mkdir -p /mnt/efs
```

---

## 3️⃣ Mount Using NFS Protocol

```bash
sudo mount -t nfs4 -o nfsvers=4.1 fs-12345678.efs.us-east-1.amazonaws.com:/ /mnt/efs
```

---

## 4️⃣ Reload System

```bash
sudo systemctl daemon-reload
sudo mount -a
```

---

## 5️⃣ Verify Mount

```bash
df -h
```

If mounted successfully, you will see `/mnt/efs` listed.

---

# 📌 Final Summary

✔ NFS = Network File System  
✔ Allows multiple systems to share centralized storage  
✔ Uses Port 2049  
✔ AWS EFS = Managed NFS service  
✔ EFS is Regional and Multi-AZ  
✔ Easy to scale and highly available  

---

🚀 This completes the complete NFS and AWS EFS Practical Guide.
