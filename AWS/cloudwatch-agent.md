# Amazon CloudWatch Agent Setup on EC2 (Amazon Linux 2023)

## ✅ CloudWatch Agent Creation (Step-by-Step)

---

## Step 1: Create IAM Role

First, create an IAM Role for the EC2 instance.

### Attach the following policies:
- `CloudWatchAgentServerPolicy`

### Steps:
- Open AWS IAM Console
- Click **Roles**
- Click **Create Role**
- Select **AWS Service**
- Choose **EC2**
- Attach required policies
- Give role name:

```text
EC2-CloudWatch-Role
```

- Click **Create Role**

---

## Step 2: Launch EC2 Instance

- Create a new EC2 instance
- Attach the IAM Role:

```text
EC2-CloudWatch-Role
```

---

## Step 3: Install CloudWatch Agent

Run the following command:

```bash
sudo yum install amazon-cloudwatch-agent -y
```

---

## Step 4: Run Configuration Wizard

CloudWatch Agent location:

```bash
ls /opt/aws/amazon-cloudwatch-agent/bin/
```

Run the configuration wizard:

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
```

### 📌 During Configuration

### Add Log File Path

```bash
/var/log/messages
```

### Give Log Group Name

```bash
ec2logs
```

---

## Step 5: Verify Configuration File

Go to the CloudWatch Agent directory:

```bash
cd /opt/aws/amazon-cloudwatch-agent/bin
```

List files:

```bash
ls
```

Check the generated configuration file:

```bash
config.json
```

### Optional: Install CollectD

```bash
sudo yum install collectd -y
```

---

## Step 6: Start CloudWatch Agent

Run the following command:

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl \
-a fetch-config \
-m ec2 \
-c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json \
-s
```

### 📌 This Command Will

- Fetch the configuration
- Start the CloudWatch Agent

---

# 🔥 Final Output

- Logs from `/var/log/messages` will be sent to CloudWatch
- Log Group Name:

```text
ec2logs
```

---

# ✅ Verify Agent Status

```bash
sudo systemctl status amazon-cloudwatch-agent
```

OR

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status
```

Expected Output:

```json
{
  "status": "running"
}
```
