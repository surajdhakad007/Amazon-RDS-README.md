# 🚀 Amazon RDS Database Setup and Management using AWS Console (README.md)

This project demonstrates how to create, configure, connect, and manage an **Amazon RDS MySQL database** using AWS Console, EC2, and AWS Systems Manager (SSM). It follows a beginner‑friendly, step‑by‑step workflow.

---

## 🎯 Project Overview

This guide covers the full lifecycle of an RDS instance:

* Creating an RDS subnet group
* Configuring Security Groups
* Launching the RDS instance
* Connecting from EC2 using SSM
* Running SQL queries
* Deleting the RDS instance safely

---

## 🧠 Project Purpose

The main goal is to gain hands-on AWS experience by integrating:

* **Amazon RDS** (database hosting)
* **Amazon EC2** (client connection)
* **AWS Systems Manager Session Manager** (secure access without SSH keys)

---

## 🛠️ AWS Services Used

| Service                   | Purpose                                            |
| ------------------------- | -------------------------------------------------- |
| Amazon RDS                | Host and manage a relational DB                    |
| Amazon EC2                | Connect and run SQL queries                        |
| AWS Systems Manager (SSM) | Secure browser-based access (no SSH keys required) |

---

## 🧩 Skills & Tools Used

* AWS Console
* RDS (MySQL)
* VPC & Security Groups
* EC2 Instance
* SSM Session Manager
* MySQL CLI
* Cloud networking fundamentals

---

# 🪜 Step-by-Step Implementation

## **Step 1: Login to AWS Console**

Login using your AWS credentials.

---

## **Step 2: Create an RDS Subnet Group**

A DB Subnet Group defines the subnets & AZs RDS can use.

**Steps:**

1. Go to **RDS → Subnet Groups → Create DB Subnet Group**
2. Fill in:

   * Name: **Demoproject**
   * Description: **rds-project**
   * VPC: Select your VPC
3. Select all AZs & private/public subnets
4. Click **Create**

✅ Subnet Group created successfully.

---

## **Step 3: Configure Security Group Rules**

To allow EC2 → RDS communication:

1. Go to **VPC → Security Groups → Create Security Group**
2. Details:

   * Name: **rds-demo-sg**
   * Description: RDS SG
3. Add inbound rule:

   * Type: **MySQL/Aurora**
   * Port: **3306**
   * Source: **VPC CIDR (172.31.0.0/16)**
4. Click Create

✅ RDS can now accept traffic from EC2 securely.

---

## **Step 4: Create the RDS Database**

1. Go to **RDS → Databases → Create Database**
2. Select:

   * Method: **Standard Create**
   * Engine: **MySQL**
   * Template: **Free Tier**
3. Settings:

   * Identifier: **rds-project**
   * Username: **admin**
   * Password: **myStrongRDSpwd!**
4. Instance:

   * Type: **db.t2.micro**
5. Storage: **20 GiB**, autoscaling disabled
6. Connectivity:

   * Security Group: **rds-demo-sg**
   * Remove default SG
7. Additional Config:

   * Initial DB: **rdsdemodb**
   * Disable backups & deletion protection
8. Click **Create Database**

✅ MySQL RDS instance is now provisioning.

---

## **Step 5: Start SSM Session (No SSH Required)**

1. Go to **Systems Manager → Session Manager → Start Session**
2. Select your EC2 instance
3. Click **Start Session**

✅ You now have a secure Linux shell without SSH.

---

## **Step 6: Connect to RDS and Create a Table**

### Switch to EC2 user

```
sudo -i -u ec2-user
```

### Install MySQL client

```
sudo yum -y install mysql
```

### Connect to RDS

Replace `<endpoint>` with your RDS endpoint.

```
mysql -h <endpoint> -u admin -p rdsdemodb
```

Password:

```
myStrongRDSpwd!
```

### Create a table

```
CREATE TABLE laboratory (id INT, name VARCHAR(100));
```

### Verify

```
DESC laboratory;
```

Exit:

```
quit;
```

✅ Table created successfully in RDS.

---

## **Step 7: Delete RDS Instance**

1. RDS → Databases → Select instance
2. Actions → **Delete**
3. Uncheck: Final snapshot
4. Acknowledge warning
5. Type: **delete me**
6. Click Delete

✅ RDS instance will be removed..

---

# 💡 Key Learnings

* Launch and configure RDS inside a VPC
* Access RDS securely using **SSM instead of SSH**
* Run SQL queries on cloud-hosted MySQL
* Understand AWS networking and access control

---

# 🧾 Summary

| Component       | Description                 |
| --------------- | --------------------------- |
| Database Engine | MySQL (Free Tier)           |
| Instance Type   | db.t2.micro                 |
| Storage         | 20 GiB                      |
| Access Method   | SSM Session Manager         |
| Security        | VPC + Custom Security Group |
| Tool            | MySQL CLI                   |

---

This README is GitHub‑ready. Let me know if you want to add diagrams, architecture illustrations, or SQL examples!
README.
