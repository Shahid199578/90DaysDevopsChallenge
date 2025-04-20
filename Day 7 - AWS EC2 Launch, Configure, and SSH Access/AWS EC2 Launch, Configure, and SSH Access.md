## **1. Introduction to AWS EC2**
Amazon Elastic Compute Cloud (EC2) is a web service that provides secure, scalable compute capacity in the cloud. It allows users to launch virtual servers, called instances, to run applications on the AWS infrastructure.
Key Features of AWS EC2:
- **Scalability**: Easily scale up or down as needed.
- **Flexibility**: Choose from various instance types and configurations.
- **Reliability**: Built on AWS’s global data centers.
- **Customizability**: Fully customizable instances with different operating systems and software.
- **Cost-Efficiency**: Pay-as-you-go pricing model.
---

[![](https://img.youtube.com/vi/eVYer7367NU/0.jpg)](https://www.youtube.com/watch?v=eVYer7367NU)

[Watch the video](https://www.youtube.com/watch?v=eVYer7367NU)


---
## **2. Types of EC2 Instances**
AWS EC2 instances are classified into various families based on their use case and workload characteristics:
**A. General Purpose**
- Balanced compute, memory, and networking.
- Suitable for web servers, development environments, and small databases.

| Instance Family | Description               | Example Types         |
|-----------------|---------------------------|------------------------|
| t4g, t3, t2      | Burstable performance       | t4g.micro, t3.medium    |
| m7g, m6i, m5      | Balanced CPU and memory     | m6i.large, m5.xlarge    |

**B. Compute Optimized**
- Ideal for compute-intensive tasks such as gaming servers and scientific modeling.

| Instance Family |	Description | Example Types |
|-----------------|-------------|---------------|
| c7g, c6i, c5 |	High CPU-to-memory ratio | c6i.large, c5.xlarge |

**C. Memory Optimized**
- Designed for memory-intensive applications like in-memory databases and real-time data processing.

| Instance Family |	Description | Example Types |
|-----------------|-------------|---------------|
| r6i, r5, x2idn | High memory | r6i.large, x2idn.24xlarge |

**D. Storage Optimized**
- Suitable for workloads requiring high disk throughput, like data warehousing.

| Instance Family |	Description | Example Types |
|-----------------|-------------|---------------|
| i4i, d3, h1 | High I/O performance | i4i.large, h1.2xlarge |

**E. Accelerated Computing**
- Use hardware accelerators or GPUs for machine learning and graphics rendering.

| Instance Family |	Description | Example Types |
|-----------------|-------------|---------------|
| p4de, g5, f1 | GPU and FPGA support | p4de.24xlarge, g5.xlarge |

### **3. Launching an EC2 Instance**
**Step 1: Open the EC2 Dashboard**
1.	Sign in to the **AWS Management Console**.
2. Navigate to the **EC2 Dashboard** by:
   - Selecting **EC2** from the **Services** menu, or
   - Searching for "EC2" in the top search bar.

**Step 2: Launch an Instance**
1.	Click Launch Instance.
2.	Enter an instance name (e.g., "MyWebServer").
3.	Choose an Amazon Machine Image (AMI), such as:
    - Amazon Linux 2
    - Ubuntu Server
    - Windows Server
4.	Select an Instance Type:
    - General Purpose: t2.micro (Free Tier Eligible)
    - Compute Optimized: c5.large
5.	Click Next: Configure Instance Details.

**4. Configuring Instance Details**
- Network: Choose the VPC and Subnet.
- Auto-Assign Public IP: Enable it for direct access.
- IAM Role: Attach a role if needed.
- Shutdown Behavior: Choose between Stop or Terminate.
- User Data (Optional): Add bootstrap scripts.

**Example User Data Script (for ubuntu):**

    #!/bin/bash
    apt update -y
    apt install apache2 -y
    systemctl start apache2
    systemctl enable apache2
    echo "Welcome to My Web Server" > /var/www/html/index.html

Click **Next: Add Storage**.

### **5. Adding Storage**
1.	Specify the root volume size (e.g., 20 GB).
2.	Choose the volume type:
- General Purpose SSD (gp3, gp2): Cost-effective and suitable for general workloads.
- Provisioned IOPS SSD (io2, io1): High performance for mission-critical applications.
- Throughput Optimized HDD (st1): Low-cost HDD for frequently accessed workloads.
- Cold HDD (sc1): Lowest cost, suitable for less frequently accessed data.
3.	Click Next: Add Tags.

### **6. Adding Tags**
Add tags to identify your instance. 

For example:

- Key: Name
- Value: MyWebServer

Click **Next: Configure Security Group**.

### **7. Configuring Security Group**
1.	Create a New Security Group or Select an Existing One.
2.	Add the following rules:

| Type	| Protocol	| Port Range	| Source |
|-------|-----------|---------------|--------|
| SSH	| TCP | 22 | 0.0.0.0/0 |
| HTTP	| TCP | 80 | 0.0.0.0/0 |
| HTTPS | TCP | 443 | 0.0.0.0/0 |

Click **Review and Launch**.

### **8. Launching the Instance**
1.	Click Launch.
2.	Choose an existing key pair or create a new one.
3.	Download the key pair (.pem file) and keep it secure.
4.	Click Launch Instances.
---

### **9. Accessing EC2 via SSH**
**Step 1: Set Permissions for the Key Pair**

chmod 400 mykey.pem

**Step 2: Connect to Your Instance**

Find the Public DNS (IPv4) from the instance details and connect:

    ssh -i "mykey.pem" ec2-user@ec2-52-12-116-90.compute-1.amazonaws.com

- Replace mykey.pem with your key file name.
- Replace the DNS with your instance's public IP.
---
### **10. Verifying and Managing Your Instance**
Check Running Services

    sudo systemctl status apache2

Update the Instance

    sudo apt update -y

Restarting the Web Server

    sudo systemctl restart apache2

### **11. Stopping and Terminating Instances**

Stop an Instance

Stopping an instance preserves the data on disk.

    aws ec2 stop-instances --instance-ids i-1234567890abcdef0

Start an Instance

    aws ec2 start-instances --instance-ids i-1234567890abcdef0

Terminate an Instance

Terminating deletes the instance and attached volumes.

    aws ec2 terminate-instances --instance-ids i-1234567890abcdef0


### **12. Monitoring and Managing Instances**

View Instance Status

    aws ec2 describe-instances

Check Instance State

    aws ec2 describe-instance-status --instance-ids i-1234567890abcdef0

Reboot an Instance

    aws ec2 reboot-instances --instance-ids i-1234567890abcdef0
    
---

### **13. Troubleshooting EC2 Connectivity Issues**
### Common Issues:
#### SSH Permission Denied:
- Check the file permission of your .pem file.
- Verify that the correct key pair is being used.
#### Instance Not Reachable:
- Check security group rules for open ports.
- Verify the network ACLs and VPC settings.
#### Web Server Not Responding:
- Ensure that the HTTP or HTTPS port is open.
- Restart the web server and check logs.

### **14. Best Practices for EC2**
- Use IAM Roles: Avoid hardcoding credentials.
- Regular Backups: Use snapshots or AMIs.
- Secure Access: Restrict SSH access by IP.
- Automate Deployments: Use scripts for consistent configurations.
- Monitor Usage: Set up CloudWatch alarms.
