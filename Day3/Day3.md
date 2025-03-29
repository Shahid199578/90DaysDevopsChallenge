**# Day 3: AWS IAM and EC2**

## **AWS IAM (Identity and Access Management)**

### **1. Introduction to IAM**
- IAM is a service that helps manage access to AWS resources securely.
- It allows users, groups, roles, and policies to control access.
- IAM is a global service (not region-specific).

### **2. IAM Users, Groups, and Roles**
- **Users**: Individual identities with access credentials.
- **Groups**: A collection of users to apply permissions collectively.
- **Roles**: Assign permissions to AWS services and users.

### **3. IAM Policies**
- JSON-based rules defining permissions.
- Can be **AWS-managed** or **customer-managed**.

### **4. IAM Best Practices**
- Enable **MFA (Multi-Factor Authentication)**.
- Follow **least privilege principle**.
- Rotate security credentials regularly.
- Use **IAM roles** instead of root credentials.

## **AWS EC2 (Elastic Compute Cloud)**

### **1. Introduction to EC2**
- Provides **scalable virtual servers** in AWS.
- Different instance types optimized for compute, memory, storage, and GPU.

### **2. Launching an EC2 Instance**
- Choose **AMI (Amazon Machine Image)**.
- Select **instance type**.
- Configure **security groups**.
- Attach **EBS volumes**.

### **3. EC2 Key Concepts**
- **Elastic IP**: Static IP for an instance.
- **Security Groups**: Firewall rules controlling inbound/outbound traffic.
- **Auto Scaling**: Automatically adjusts the number of instances.
- **Load Balancer**: Distributes traffic across instances.

### **4. EC2 Best Practices**
- Use **IAM roles** instead of storing credentials in EC2.
- **Monitor instances** using AWS CloudWatch.
- Enable **automatic backups** for EBS.


