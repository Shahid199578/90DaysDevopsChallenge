# Day 31 - Jenkins and CI/CD Fundamentals

Welcome to **Day 31** of our DevOps 90-Day Challenge!
Today we are starting our journey with **Jenkins**, one of the most popular CI/CD automation tools in the DevOps ecosystem.

[![](https://img.youtube.com/vi/0J4WQqVoxHE/0.jpg)](https://www.youtube.com/watch?v=0J4WQqVoxHE)
[Watch the video](https://www.youtube.com/watch?v=0J4WQqVoxHE)

---

## Objective

By the end of this session, you will:

* Understand what Jenkins is and why it’s used in DevOps.
* Learn Jenkins architecture (Master & Agents).
* Install Jenkins on your system (Linux/Windows/Docker).
* Run your first Jenkins job.

---

## Tools Used

* **Jenkins** (Open-source CI/CD tool)
* **Java (JDK 11 or higher)**
* **Docker (optional, if you want containerized Jenkins)**
* **GitHub** (for source code integration)

---

## Step-by-Step Guide

### 1. Install Java

Jenkins requires Java. On Ubuntu:

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
java -version
```

### 2. Install Jenkins

```bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
```

Start & enable service:

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

### 3. Access Jenkins

Open in browser:
`http://localhost:8080`

Unlock Jenkins using the initial admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

### 4. Install Plugins & Setup Admin

* Install suggested plugins
* Create admin user
* Configure system

### 5. Create Your First Job

* Go to **New Item** → Select **Freestyle project**
* Add **Build Step** → `echo "Hello from Jenkins!"`
* Run the job

---

## Verification

* Jenkins is accessible on `http://localhost:8080`
* Plugins installed successfully
* First job executes and prints "Hello from Jenkins!"

---

## Key Concepts Applied

| Concept           | Example Used                  |
| ----------------- | ----------------------------- |
| CI/CD Basics      | Jenkins automates code builds |
| Jenkins Master    | Installed on local server     |
| Agents            | (Optional) run jobs remotely  |
| Freestyle Project | Simple job to test Jenkins    |

---

## Congratulations!

You’ve successfully installed Jenkins and run your very first job! From here, we’ll dive deeper into **pipelines, plugins, integrations, and automation**.

---

## Try These Next

* Install Jenkins using **Docker** instead of bare-metal
* Connect Jenkins to **GitHub repository**
* Explore Jenkinsfile for pipeline automation

---

