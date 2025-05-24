Hello everyone! 👋


As we’ve now covered several important days in our 90 Days DevOps Challenge, it's time to showcase your learning and progress!

### Task for Today:
1.	Go to our LinkedIn [group.](https://www.linkedin.com/groups/14632188/)
2.	Create a post summarizing what you've learned so far — from Day 1 up to today (e.g., IAM, EC2, VPCs, NACLs, Linux permissions, etc.).
3.	Feel free to add:
    - Key takeaways
    - Any hands-on labs or screenshots
    - What you found interesting or challenging
4.	Tag me (@mohd-shahid-mohd) in your post.
5.	Use hashtags like:
```
#DevOpsChallenge #LearningInPublic #AWS #Linux #CloudComputing
```
🎯 Why this matters:
- It helps solidify your knowledge.
- It builds your professional presence on LinkedIn.
- You can inspire others to join and learn!


💡 Keep it short but meaningful. No need to write essays — just share your real experience and learning!
Let’s celebrate your progress. Proud of how far you all have come! 🙌


Here's a Day-wise Lab Summary you can share post on LinkedIn to encourage engagement:
---
DevOps 90-Day Challenge – Lab Summary


***Day 1: Introduction to DevOps and Cloud Computing***
#### ***Lab Tasks:***
- Understand DevOps lifecycle with real-world examples.
- Compare traditional vs DevOps workflows.
- Identify cloud providers (AWS, Azure, GCP).
- Research IaaS vs PaaS vs SaaS.
- Create a free AWS account (preparation for Day 3).
---
***Day 2: AWS Fundamentals and Services Overview***
#### ***Lab Tasks:***
- Log in to AWS Console.
- Navigate through AWS services (EC2, S3, IAM, RDS, VPC).
- Understand global infrastructure: Regions & AZs.
- Hands-on: Launch the AWS pricing calculator and estimate costs.
---
***Day 3: AWS Free Tier Account and AWS CLI Setup***
#### ***Lab Tasks:***
- Set up AWS CLI on your system.
- Configure CLI with aws configure.
- Run basic AWS CLI commands:
  -	aws s3 ls
  - aws ec2 describe-instances
- Verify CLI and Console access.
---
***Day 4: IAM (Identity and Access Management)***
#### ***Lab Tasks:***
- Create IAM Users, Groups, and Roles.
- Apply least privilege policies.
- Use AWS managed and custom policies.
- Create programmatic access credentials.
- Enable MFA for an IAM user.
---
***Day 5: Git and GitHub Basics***
#### ***Lab Tasks:***
- Install Git and configure user identity.
- Initialize a local Git repo.
- Create a repo on GitHub.
- Push local code to GitHub.
- Practice branching and merging.
---
***Day 6: Linux Basics for DevOps***
#### ***Lab Tasks:***
- Connect to EC2 Linux instance.
- Practice Linux commands: ls, cd, pwd, mkdir, rm, cat.
- Use sudo, chmod, and chown.
- Create and edit files using nano or vim.
---
***Day 7: EC2 Launch and SSH Access***
#### ***Lab Tasks:***
- Launch a new EC2 instance with proper key pair.
- Use security groups to allow SSH (port 22).
- Connect to instance using ssh -i key.pem ec2-user@ip.
- Perform basic system update and software install.
---
***Day 8: EC2 Auto Scaling and Monitoring***
#### ***Lab Tasks:***
- Create a Launch Template.
- Configure Auto Scaling Group with minimum and max instances.
- Attach CloudWatch alarm to scale based on CPU usage.
- Terminate instances and watch ASG relaunch automatically.
---
***Day 9: EBS and S3 Storage***
#### ***Lab Tasks:***
- Create and attach EBS volume to EC2.
- Mount and format EBS volume.
- Create and access S3 bucket using CLI.
- Upload/download files from EC2 to S3.
---
***Day 10: Snapshots and AMIs***
#### ***Lab Tasks:***
- Create snapshot of EBS volume.
- Create custom AMI from EC2 instance.
- Launch a new instance from the AMI.
- Restore volume from snapshot.
---
***Day 11: VPC – Subnets, Route Tables, Gateways***

#### ***Lab Tasks:***
- Create custom VPC with public and private subnets.
- Configure route tables and IGW.
- Launch EC2 in custom subnets and test connectivity.
- Set up proper routing for internet access.
---
***Day 12: Security Groups, NACLs, and VPC Peering***

#### ***Lab Tasks:***
- Create Security Groups with specific port rules.
- Create NACLs to allow/block subnet-level access.
- Create and configure VPC peering between two VPCs.
- Test connectivity using ping and telnet.
---
***Day 13: NAT Gateway, Internet Gateway, Bastion Host***

#### ***Lab Tasks:***
- Create NAT Gateway in public subnet.
- Use NAT for outbound internet access from private subnet.
- Launch Bastion Host in public subnet.
- SSH into Bastion, then into private EC2 using private IP.
---
***Day 14: Linux Deep Dive – Permissions, Processes, Services***

#### ***Lab Tasks:***
- Practice chmod, chown, ls -l on test files.
- Add users and groups; switch users and set passwords.
- Use ps, top, kill, systemctl to manage processes and services.
- Install and manage Nginx service.

---

***Day 15: Introduction to Shell Scripting***

#### ***Lab Tasks:***
1. Create and Run Your First Shell Script

- Write a basic hello.sh script using echo.
- Make it executable with chmod +x.

2. Create a Script to Add Users and Groups

- Write a shell script to add a new user and group.
- Include user switching (su) and password setup using passwd.

3. Write a Script to Monitor and Manage Processes

- Use ps, top, and kill within a script to check and stop processes.
  - Example: Automatically kill a zombie process.

4. Script to Manage System Services

- Install nginx via a script (sudo apt install nginx -y).
- Start, stop, and enable it using systemctl inside the script.

---

### ***Day 16: Introduction to AWS CloudWatch***

#### ***Lab Tasks:***

1. **Explore CloudWatch Dashboard**

   * Navigate to AWS CloudWatch from the AWS Console.
   * Review pre-configured dashboards for EC2, Lambda, etc.

2. **Create Custom CloudWatch Alarms**

   * Create an alarm to monitor EC2 instance CPU utilization.
   * Configure thresholds and email notifications (via SNS).

3. **Enable CloudWatch Agent**

   * Install and configure CloudWatch Agent on an EC2 instance.
   * Send custom system-level metrics (memory, disk, etc.).

4. **Log Group Creation & Log Shipping**

   * Create log groups and streams.
   * Configure EC2 to send application logs (e.g., nginx access logs) to CloudWatch Logs.

5. **Set Metric Filters**

   * Set filters on log groups to trigger alerts (e.g., “ERROR” or failed login attempts).

---

### ***Day 17: AWS Monitoring & Alerting – Deep Dive***

#### ***Lab Tasks:***

1. **Use Detailed Monitoring on EC2**

   * Enable detailed monitoring and review additional metrics collected every 1 minute.

2. **Custom Dashboards**

   * Build custom dashboards with widgets:

     * EC2 CPU Utilization
     * Disk usage
     * Application errors

3. **Create Composite Alarms**

   * Set multiple metric conditions (e.g., CPU > 70% AND Memory > 80%) for alerting.
   * Configure alarm actions (SNS, Lambda).

4. **Log Insights**

   * Use CloudWatch Log Insights to query log data.

     * Example: Find 5xx HTTP errors in nginx logs.
     * Example: Query logs to identify failed login attempts.

5. **Alert Automation**

   * Trigger Lambda functions on alarm (e.g., restart EC2 or notify Slack).

---

### ***Day 18: AWS CloudTrail and Centralized Logging with ELK Stack***

#### ***Lab Tasks – Part 1: AWS CloudTrail***

1. **Enable CloudTrail for All Regions**

   * Create a trail and send logs to an S3 bucket.
   * Enable log validation for tamper detection.

2. **Log Analysis with CloudTrail**

   * Use AWS CLI to query events:

     ```bash
     aws cloudtrail lookup-events --max-results 5
     ```
   * Use Athena to query logs stored in S3.

3. **Forward CloudTrail Logs to CloudWatch**

   * Integrate with CloudWatch Logs for real-time event monitoring.

---

#### ***Lab Tasks – Part 2: ELK Stack for Centralized Logging***

1. **Understand ELK Components**

   * **Elasticsearch**: Stores & indexes logs.
   * **Logstash**: Ingests and transforms logs.
   * **Kibana**: Visualizes logs and metrics.

2. **Deploy ELK on EC2 (Optional – Advanced)**

   * Install and configure Elasticsearch, Logstash, and Kibana.
   * Open ports: 9200 (ES), 5601 (Kibana), 5044 (Logstash).

3. **Ingest Logs from S3 (CloudTrail)**

   * Configure Logstash to pull logs from S3.
   * Transform JSON data and send to Elasticsearch.

4. **Visualize in Kibana**

   * Create index patterns, dashboards, and search logs.
   * Create alerts and filters for suspicious events.

---
### ***Day 19: Introduction to Docker and Containerization***

1. **Understand Docker Components**

---

### ***Day 20: Building and Running Docker Containers***

---

#### ***Lab Tasks – Part 1: Writing a Dockerfile and Building a Docker Image***

1. **Create a Simple App Directory**

   ```bash
   mkdir docker-demo && cd docker-demo
   ```

2. **Write a Simple Python App**
   Create a file named `app.py`:

   ```python
   print("Hello from inside Docker!")
   ```

3. **Write the Dockerfile**
   Create a file named `Dockerfile`:

   ```dockerfile
   # Use an official Python base image
   FROM python:3.9-slim

   # Set the working directory
   WORKDIR /app

   # Copy current directory contents into the container
   COPY . .

   # Run the app
   CMD ["python", "app.py"]
   ```

4. **Build the Docker Image**

   ```bash
      
   ```

---

#### ***Lab Tasks – Part 2: Running and Managing Docker Containers***

1. **Run a Container**

   ```bash
   docker run my-python-app
   ```

2. **Run in Detached Mode**

   ```bash
   docker run -d --name demo-container my-python-app
   ```

3. **View Running Containers**

   ```bash
   docker ps
   ```

4. **Stop and Remove Container**

   ```bash
   docker stop demo-container
   docker rm demo-container
   ```

---

#### ***Lab Tasks – Part 3: Docker Image Management Commands***

1. **View All Images**

   ```bash
   docker images
   ```

2. **Tag an Image**

   ```bash
   docker tag my-python-app shahiddevops/my-python-app:v1
   ```

3. **Commit a Running Container to an Image**

   ```bash
   docker commit <container_id> shahiddevops/custom-image:v1
   ```

4. **Login to Docker Hub**

   ```bash
   docker login
   ```

5. **Push Image to Docker Hub**

   ```bash
   docker push shahiddevops/my-python-app:v1
   ```

6. **Pull Image from Docker Hub**

   ```bash
   docker pull shahiddevops/my-python-app:v1
   ```

---

🎯 Action for Everyone:
Post your learnings in our LinkedIn group, tag me, and share any screenshots or key takeaways. Let’s build a visible DevOps learning community!
