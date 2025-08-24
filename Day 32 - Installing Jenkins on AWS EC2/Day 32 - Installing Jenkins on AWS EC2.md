# Day 32 - Installing Jenkins on AWS EC2
Welcome to **Day 32** of our DevOps 90-Day Challenge!
Yesterday, you learned Jenkins basics and created your first job.
Today, we’ll take it a step further and **install Jenkins on AWS EC2**, so you can run it in a cloud environment accessible to your team.

[![](https://img.youtube.com/vi/3zseHbWNs4w/0.jpg)](https://www.youtube.com/watch?v=3zseHbWNs4w)

[Watch the video](https://www.youtube.com/watch?v=3zseHbWNs4w)

---

## Objective

By the end of this session, you will:

* Launch an **AWS EC2 instance** for Jenkins.
* Install and configure Jenkins on EC2.
* Open required ports with a **Security Group**.
* Access Jenkins publicly.

---

## Tools Used

* **AWS Account**
* **EC2 Instance (Ubuntu 22.04 preferred)**
* **Jenkins** (installed on EC2)
* **SSH Client (Terminal or PuTTY)**

---

## Step-by-Step Guide

### 1. Launch an EC2 Instance

* Go to **AWS Console → EC2 → Launch Instance**
* Select **Ubuntu 22.04 LTS AMI**
* Instance type: `t2.micro` (Free Tier eligible)
* Create a **Key Pair** (download `.pem` file)
* Configure Security Group:

  * Allow SSH (22) from your IP
  * Allow HTTP (80) from anywhere
  * Allow Custom TCP (8080) from anywhere (for Jenkins)

### 2. Connect to EC2

```bash
ssh -i mykey.pem ubuntu@<EC2_PUBLIC_IP>
```

### 3. Install Java

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
java -version
```

### 4. Install Jenkins

```bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
```

Enable & Start Jenkins:

```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

### 5. Open Jenkins in Browser

* Get Public IP of EC2 → `http://<EC2_PUBLIC_IP>:8080`
* Unlock Jenkins:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

* Install suggested plugins
* Create admin user

---

## Verification

* Access Jenkins from **browser over the internet**.
* Jenkins dashboard loads successfully.
* Plugins install without issues.

---

## Bonus (Advanced)

* Map EC2 **Elastic IP** so Jenkins IP doesn’t change.
* Configure **Nginx Reverse Proxy** for domain → `http://jenkins.mydevops.com`.
* Secure with **Let’s Encrypt SSL**.

---

## Key Concepts Applied

| Concept              | Example Used                           |
| -------------------- | -------------------------------------- |
| Cloud Infrastructure | AWS EC2 as Jenkins host                |
| Security             | Security Groups for ports 22, 80, 8080 |
| CI/CD Setup          | Jenkins running on a public server     |

---

## Congratulations!

You now have Jenkins running on AWS EC2! 
From this point, you can start using Jenkins as a **centralized CI/CD server**.

---

## Try These Next

* Attach an **Elastic IP** and test persistence.
* Install Jenkins on **Docker inside EC2**.
* Secure Jenkins with **Nginx + SSL**.


