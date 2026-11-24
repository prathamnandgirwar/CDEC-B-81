# Introduction to AWS CLI

The **AWS Command Line Interface (CLI)** is a powerful tool that enables users to interact with AWS services using commands. It helps automate tasks and manage AWS services efficiently without using the AWS Management Console.

---

# AWS CLI Setup and Configuration

## Step 1: Install AWS CLI
Download the AWS CLI installer for your operating system.

Official Documentation:  
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

---

## Step 2: Configure AWS CLI

Run the following command to configure AWS CLI:

```bash
aws configure
```

Provide the following details:

- Access Key ID
- Secret Access Key
- Default Region (Example: `ap-south-1`)
- Output Format (`json`, `table`, `text`)

---

## Step 3: Verify Installation

Run the following command to verify the installation:

```bash
aws --version
```

---

# AWS CLI Commands for S3 Management

## 1. List S3 Buckets

```bash
aws s3 ls
```

## 2. Create a Bucket

```bash
aws s3 mb s3://<bucket-name>
```

## 3. Upload a File to S3

```bash
aws s3 cp <file-path> s3://<bucket-name>/
```

## 4. List Objects in a Bucket

```bash
aws s3 ls s3://<bucket-name>/
```

## 5. Delete an Object

```bash
aws s3 rm s3://<bucket-name>/<object-key>
```

## 6. Sync Local Folder to S3

```bash
aws s3 sync <local-folder-path> s3://<bucket-name>/
```

## 7. Empty an S3 Bucket

```bash
aws s3 rm s3://cbz14buck --recursive
```

## 8. Delete an Empty Bucket

```bash
aws s3api delete-bucket --bucket cbz14buck --region ap-south-1
```

---

# AWS CLI Commands for EC2 Management

## 1. List EC2 Instances

```bash
aws ec2 describe-instances
```

## 2. Start an EC2 Instance

```bash
aws ec2 start-instances --instance-ids <instance-id>
```

## 3. Stop an EC2 Instance

```bash
aws ec2 stop-instances --instance-ids <instance-id>
```

## 4. Terminate an EC2 Instance

```bash
aws ec2 terminate-instances --instance-ids <instance-id>
```

## 5. Create a Key Pair

```bash
aws ec2 create-key-pair --key-name <key-name>
```

---

# AWS CLI Commands for IAM Management

## 1. List IAM Users

```bash
aws iam list-users
```

## 2. Create an IAM User

```bash
aws iam create-user --user-name <user-name>
```

## 3. Attach Policy to IAM User

```bash
aws iam attach-user-policy \
--user-name <user-name> \
--policy-arn <policy-arn>
```

## 4. Create an IAM Group

```bash
aws iam create-group --group-name <group-name>
```

## 5. Add User to Group

```bash
aws iam add-user-to-group \
--user-name <user-name> \
--group-name <group-name>
```

## 6. Create Custom IAM Policy

```bash
aws iam create-policy \
--policy-name <policy-name> \
--policy-document file://<policy-document.json>
```

---

# AWS CLI Commands for VPC Management

## 1. List VPCs

```bash
aws ec2 describe-vpcs
```

## 2. Create a VPC

```bash
aws ec2 create-vpc --cidr-block <CIDR-block>
```

## 3. Create a Subnet

```bash
aws ec2 create-subnet \
--vpc-id <vpc-id> \
--cidr-block <CIDR-block>
```

## 4. Create an Internet Gateway

```bash
aws ec2 create-internet-gateway
```

## 5. Attach Internet Gateway to VPC

```bash
aws ec2 attach-internet-gateway \
--vpc-id <vpc-id> \
--internet-gateway-id <igw-id>
```

## 6. Create a Route Table

```bash
aws ec2 create-route-table --vpc-id <vpc-id>
```

## 7. Add Route to Route Table

```bash
aws ec2 create-route \
--route-table-id <route-table-id> \
--destination-cidr-block 0.0.0.0/0 \
--gateway-id <igw-id>
```

## 8. Associate Route Table with Subnet

```bash
aws ec2 associate-route-table \
--subnet-id <subnet-id> \
--route-table-id <route-table-id>
```

---

# Reference

Official AWS CLI Documentation:

https://docs.aws.amazon.com/cli/latest/

---

These hands-on tasks will help reinforce the **understanding and practical usage of AWS CLI commands** for managing AWS resources.
