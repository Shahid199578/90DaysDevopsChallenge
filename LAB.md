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


## Day 1 – Introduction to DevOps and Cloud Computing
#### Lab Tasks:
- Understand DevOps lifecycle with real-world examples.
- Compare traditional vs DevOps workflows.
- Identify cloud providers (AWS, Azure, GCP).
- Research IaaS vs PaaS vs SaaS.
- Create a free AWS account (preparation for Day 3).
---
## Day 2 – AWS Fundamentals and Services Overview
#### Lab Tasks:
- Log in to AWS Console.
- Navigate through AWS services (EC2, S3, IAM, RDS, VPC).
- Understand global infrastructure: Regions & AZs.
- Hands-on: Launch the AWS pricing calculator and estimate costs.
---
## Day 3 – AWS Free Tier Account and AWS CLI Setup
#### Lab Tasks:
- Set up AWS CLI on your system.
- Configure CLI with aws configure.
- Run basic AWS CLI commands:
  -	aws s3 ls
  - aws ec2 describe-instances
- Verify CLI and Console access.
---
## Day 4 – IAM (Identity and Access Management)
#### Lab Tasks:
- Create IAM Users, Groups, and Roles.
- Apply least privilege policies.
- Use AWS managed and custom policies.
- Create programmatic access credentials.
- Enable MFA for an IAM user.
---
## Day 5 – Git and GitHub Basics
#### Lab Tasks:
- Install Git and configure user identity.
- Initialize a local Git repo.
- Create a repo on GitHub.
- Push local code to GitHub.
- Practice branching and merging.
---
## Day 6 – Linux Basics for DevOps
#### Lab Tasks:
- Connect to EC2 Linux instance.
- Practice Linux commands: ls, cd, pwd, mkdir, rm, cat.
- Use sudo, chmod, and chown.
- Create and edit files using nano or vim.
---
## Day 7 – EC2 Launch and SSH Access
#### Lab Tasks:
- Launch a new EC2 instance with proper key pair.
- Use security groups to allow SSH (port 22).
- Connect to instance using ssh -i key.pem ec2-user@ip.
- Perform basic system update and software install.
---
## Day 8 – EC2 Auto Scaling and Monitoring
#### Lab Tasks:
- Create a Launch Template.
- Configure Auto Scaling Group with minimum and max instances.
- Attach CloudWatch alarm to scale based on CPU usage.
- Terminate instances and watch ASG relaunch automatically.
---
## Day 9 – EBS and S3 Storage
#### Lab Tasks:
- Create and attach EBS volume to EC2.
- Mount and format EBS volume.
- Create and access S3 bucket using CLI.
- Upload/download files from EC2 to S3.
---
## Day 10 – Snapshots and AMIs
#### Lab Tasks:
- Create snapshot of EBS volume.
- Create custom AMI from EC2 instance.
- Launch a new instance from the AMI.
- Restore volume from snapshot.
---
## Day 11 – VPC – Subnets, Route Tables, Gateways

#### Lab Tasks:
- Create custom VPC with public and private subnets.
- Configure route tables and IGW.
- Launch EC2 in custom subnets and test connectivity.
- Set up proper routing for internet access.
---
## Day 12 – Security Groups, NACLs, and VPC Peering

#### Lab Tasks:
- Create Security Groups with specific port rules.
- Create NACLs to allow/block subnet-level access.
- Create and configure VPC peering between two VPCs.
- Test connectivity using ping and telnet.
---
## Day 13 – NAT Gateway, Internet Gateway, Bastion Host

#### Lab Tasks:
- Create NAT Gateway in public subnet.
- Use NAT for outbound internet access from private subnet.
- Launch Bastion Host in public subnet.
- SSH into Bastion, then into private EC2 using private IP.
---
## Day 14 – Linux Deep Dive – Permissions, Processes, Services

#### Lab Tasks:
- Practice chmod, chown, ls -l on test files.
- Add users and groups; switch users and set passwords.
- Use ps, top, kill, systemctl to manage processes and services.
- Install and manage Nginx service.

---

## Day 15 – Introduction to Shell Scripting

#### Lab Tasks:
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

## Day 16 – Introduction to AWS CloudWatch

#### Lab Tasks:

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

## Day 17 – AWS Monitoring & Alerting – Deep Dive

#### Lab Tasks:

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

## Day 18 – AWS CloudTrail and Centralized Logging with ELK Stack

#### Lab Tasks – Part 1: AWS CloudTrail

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

#### Lab Tasks – Part 2: ELK Stack for Centralized Logging

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
## Day 19 – Introduction to Docker and Containerization

1. **Understand Docker Components**

---

## Day 20 – Building and Running Docker Containers

---

#### Lab Tasks – Part 1: Writing a Dockerfile and Building a Docker Image

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
   docker build -t flask-app .
   ```

---

#### Lab Tasks – Part 2: Running and Managing Docker Containers

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

#### Lab Tasks – Part 3: Docker Image Management Commands

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

## Day 21 – Docker Networking, Volumes, and Compose Projects

### Part 1: Docker Networking

#### 🔹 Task 1: Create and Use a Custom Bridge Network

* Create a bridge network.
* Run two Alpine containers on this network.
* Test communication between the containers using container names.

#### 🔹 Task 2: Host Network Mode (Linux only)

* Run an Nginx container in `--network host` mode.
* Access the Nginx web server via `localhost`.

#### 🔹 Task 3: Overlay Network (Docker Swarm)

* Initialize Docker Swarm.
* Create an overlay network.
* Deploy an Nginx service with 2 replicas on the overlay network.
* List and inspect service and network details.

### Part 2: Docker Volumes and Data Persistence

#### 🔹 Task 1: Named Volume

* Create a named volume.
* Mount it into a container.
* Add data to the volume and verify it from another container.

#### 🔹 Task 2: Bind Mount from Host

* Create a directory and a file on the host.
* Bind mount the host directory into a container.
* Read the file from inside the container.

#### 🔹 Task 3: tmpfs (In-Memory Mount)

* Run a container with a `tmpfs` mount.
* Write and read data inside the `tmpfs` directory.
* Verify data does not persist after the container stops.

### Part 3: Multi-Container App with Docker Compose

#### Folder Structure:

```
multi-app/
├── app.py
├── Dockerfile
├── requirements.txt
└── docker-compose.yml
```

#### 🔹 Step 1: Create a Flask App (`app.py`)

* Create a simple web app using Flask.
* Use Redis to store a counter for page views.

#### 🔹 Step 2: Define Dependencies (`requirements.txt`)

* Add necessary Python packages.

#### 🔹 Step 3: Write a Dockerfile

* Use Python base image.
* Copy application files and install dependencies.
* Set the container's startup command.

#### 🔹 Step 4: Define `docker-compose.yml`

* Define `web` and `redis` services.
* Configure ports, networks, and dependencies.

#### 🔹 Step 5: Build and Run

* Use Docker Compose to build and launch the application.
* Access the app in a web browser.

#### Cleanup Tasks

* Stop and remove containers, volumes, and networks.
* Leave Docker Swarm mode.

---

## Day 25 – Kubernetes Services, Ingress, and Load Balancing
#### Lab Tasks:
- Deploy a basic NGINX Deployment.
- Create a NodePort Service to expose it.
- Install `nginx-ingress` and configure an Ingress resource.
- Update your `/etc/hosts` file and test the routing.

---

## Day 26 – Kubernetes Volumes, ConfigMaps, and Secrets
#### Lab Tasks:
- Create and mount a PersistentVolume and PersistentVolumeClaim.
- Use ConfigMap to provide configuration values to a Pod.
- Inject Secrets into a Pod and print them from the container logs.

---

## Day 27 – Kubernetes Monitoring (Prometheus + Grafana)
#### Lab Tasks:
- Manually deploy Prometheus and Grafana in your cluster.
- Access both UIs via port forwarding.
- Configure Prometheus as Grafana data source.
- Create at least 3 panels in a custom dashboard.
- (Optional) Add a basic alert rule.

---

## Day 28 – Kubernetes Logging and Troubleshooting
#### Lab Tasks:
- Deploy a sample app and view logs using `kubectl logs`.
- Use sidecar logging pattern with a log-collector container.
- Install EFK (Elasticsearch, Fluentd, Kibana) or Loki + Grafana.
- Practice debugging failing pods (`kubectl describe`, `kubectl exec`).

---

## Day 29 – Helm Charts and Application Packaging
#### Lab Tasks:
- Add Bitnami repo.
- Install Redis with custom password.
- Upgrade Redis to enable persistence.
- Roll back the release.
- Uninstall the release.

---

## Day 30 – Real-World Kubernetes Deployment Example
#### Lab Tasks:
- Package a Node.js app into a Docker image.
- Deploy it on Kubernetes using Deployment, Service, ConfigMap, Secret.
- Add Horizontal Pod Autoscaler.
- Configure Ingress for domain routing.
- Validate with curl or browser.

---

## Day 31 – Jenkins and CI/CD Fundamentals
#### Lab Tasks:
- Learn about Continuous Integration and Continuous Delivery.
- Understand Jenkins architecture.
- Install Jenkins locally using Docker.
- Explore Jenkins UI, jobs, and build history.
- Run a freestyle job.

---

## Day 32 – Installing Jenkins on AWS EC2
#### Lab Tasks:
- Launch Ubuntu EC2 instance.
- Install Java and Jenkins.
- Open port 8080 in security groups.
- Access Jenkins dashboard in browser.
- Configure admin user and basic plugins.

---

## Day 33 – Jenkins + GitHub Integration
#### Lab Tasks:
- Connect Jenkins with GitHub using webhooks.
- Create a Jenkins job triggered by GitHub push.
- Clone and build code automatically.
- View triggered builds in Jenkins UI.

---

## Day 34 – CI/CD for Dockerized Apps
#### Lab Tasks:
- Create Dockerfile for a sample app.
- Write Jenkins pipeline to build Docker image.
- Push image to Docker Hub.
- Deploy container on server.
- Automate the entire pipeline.

---

## Day 35 – Jenkinsfile and Declarative Pipelines
#### Lab Tasks:
- Learn Jenkins Declarative Pipeline syntax.
- Write a Jenkinsfile and commit to GitHub repo.
- Automate pipeline with stages (Build, Test, Deploy).
- Use environment variables and post actions.

---

## Day 36 – GitHub Actions Introduction
#### Lab Tasks:
- Learn GitHub Actions workflow syntax.
- Create `.github/workflows/ci.yml`.
- Add job to run tests on push.
- Observe workflow runs in GitHub UI.

---

## Day 37 – Building Workflows with GitHub Actions
#### Lab Tasks:
- Add multiple jobs in workflow.
- Implement job dependencies.
- Use matrix builds for different Node.js versions.
- Reuse workflow templates.

---

## Day 38 – Advanced GitHub Actions with Secrets and Artifacts
#### Lab Tasks:
- Store secrets in GitHub repo.
- Use secrets in workflows securely.
- Upload build artifacts.
- Download artifacts in another job.
- Implement approval step.

---

## Day 39 – Introduction to Terraform and IaC
#### Lab Tasks:
- What is Infrastructure as Code?
- Install Terraform CLI.
- Write a Terraform config to provision EC2.
- Run `terraform init`, `apply`, and `destroy`.
- Manage infrastructure lifecycle.

---

## Day 40 – Writing Terraform for AWS (EC2, S3, IAM)
#### Lab Tasks:
- Create EC2 instance with Terraform.
- Create S3 bucket with versioning.
- Create IAM user with policy.
- Use variables and outputs.

---

## Day 41 – Terraform State Management and Workspaces
#### Lab Tasks:
- Understand Terraform state file.
- Use `terraform state list`, `show`.
- Create remote backend with S3 + DynamoDB.
- Work with multiple workspaces (dev, prod).

---

## Day 42 – Advanced Terraform Concepts (Modules, Remote Backends)
#### Lab Tasks:
- Write reusable Terraform module.
- Publish module locally.
- Use remote backend (S3/DynamoDB).
- Configure remote module source.

---

## Day 43 – Terraform + Jenkins CI/CD Integration
#### Lab Tasks:
- Write Jenkins pipeline for Terraform.
- Lint and validate Terraform configs.
- Plan and apply infrastructure changes.
- Use Jenkins credentials for AWS auth.

---

## Day 44 – AWS CloudFormation Basics and YAML Templates
#### Lab Tasks:
- Write a basic CloudFormation template in YAML.
- Deploy stack via AWS Console.
- Create EC2 + Security Group.
- Validate template using `cfn-lint`.

---

## Day 45 – Writing Reusable CloudFormation Templates
#### Lab Tasks:
- Use parameters and mappings.
- Add conditions and outputs.
- Create nested stacks.
- Manage templates in Git repo.

---

## Day 46 – Automated Infrastructure Provisioning Pipeline
#### Lab Tasks:
- Combine Terraform and CloudFormation.
- Build Jenkins pipeline to deploy infra.
- Test infra provisioning automatically.
- Implement rollback on failure.
---
## Day 47 – Introduction to Ansible and Configuration Management
#### Lab Tasks:
- Install Ansible on Control Node.
- Setup Passwordless SSH to managed nodes.
- Run Ad-Hoc commands (ping, uptime).
---
## Day 48 – Writing Playbooks and Ansible Roles
#### Lab Tasks:
- Write first YAML Playbook.
- Refactor Playbook into Role structure.
- Use Ansible Galaxy to init roles.
---
## Day 49 – Ansible + Jenkins Integration
#### Lab Tasks:
- Install Ansible plugin in Jenkins.
- Trigger Playbook execution from Jenkins Job.
- Automate configuration updates.
---
## Day 50 – Ansible Best Practices
#### Lab Tasks:
- Use Ansible Vault to encrypt secrets.
- Optimize Playbook execution speed.
---
## Day 51 – Serverless Architecture
#### Lab Tasks:
- Create Hello World Lambda Function.
- Test Function execution in Console.
---
## Day 52 – Writing Lambda Functions
#### Lab Tasks:
- Create Lambda with S3 Trigger.
- Process file uploads automatically.
---
## Day 53 – CICD for Serverless
#### Lab Tasks:
- Deploy Lambda using Serverless Framework/SAM.
- Automate deployment with CodePipeline.
---
## Day 54 – Monitoring Serverless
#### Lab Tasks:
- View Lambda CloudWatch Logs.
- Debug execution errors.
---
## Day 55 – Logging with CloudWatch for Lambda
#### Lab Tasks:
- Set up CloudWatch Logs for Lambda functions.
- Create Log Groups and Retention policies.
---
## Day 56 – Real-World Serverless Automation Example
#### Lab Tasks:
- deploy a serverless user creation script.
- Automate IAM permission management.
---
## Day 57 – AWS API Gateway Deep Dive
#### Lab Tasks:
- Create REST API with API Gateway.
- Integrate API Gateway with Lambda backend.
- Set up API Keys and Usage Plans.
---
## Day 58 – Automating Backups and Notifications
#### Lab Tasks:
- Automate EBS Snapshots using Lambda + CloudWatch Events.
- Send SNS notifications on backup completion.
---
## Day 59 – Advanced Monitoring and Logging Pipelines
#### Lab Tasks:
- Build a centralized logging pipeline (CloudWatch -> Kinesis -> OpenSearch).
- Analyze logs in real-time.
---
## Day 60 – Observability with OpenTelemetry
#### Lab Tasks:
- Instrument an application with OpenTelemetry auto-instrumentation.
- Export traces to a backend (Jaeger or X-Ray).
---
## Day 61 – APM with Datadog and AWS Integrations
#### Lab Tasks:
- Integrate Datadog with AWS account.
- Monitor EC2 and Lambda metrics in Datadog Dashboard.
---
## Day 62 – Security IAM Best Practices
#### Lab Tasks:
- Audit IAM roles using Access Analyzer.
- Implement MFA enforcement policies.
---
## Day 63 – AWS Secrets Manager and Parameter Store
#### Lab Tasks:
- Store database credentials in Secrets Manager.
- Retrieve secrets programmatically in Python/Node.js.
---
## Day 64 – Network Security (WAF, Shield, NACLs)
#### Lab Tasks:
- Configure AWS WAF to block SQL injection and XSS.
- Understand AWS Shield for DDoS protection.
- Implement NACLs to block specific IPs at the subnet level.
---
## Day 65 – Compliance Tools (AWS Config, Security Hub, Trusted Advisor)
#### Lab Tasks:
- Set up AWS Config to audit resource configurations (e.g., S3 public access).
- Enable Security Hub and check CIS Benchmark score.
- Review Trusted Advisor for cost and security recommendations.
---
## Day 66 – Cost Optimization Strategies
#### Lab Tasks:
- implementation of Savings Plans and Reserved Instances.
- Analyze Cost and Usage Reports (CUR).
---
## Day 67 – Monitoring Cost with AWS Budgets
#### Lab Tasks:
- Set up AWS Budgets for monthly spend.
- Configure alerting for forecasted overruns.
---
## Day 68 – Tagging and Resource Management
#### Lab Tasks:
- Implement a consistent Tagging Policy.
- Use Resource Groups to manage tagged resources.
---
## Day 69 – Disaster Recovery and High Availability
#### Lab Tasks:
- Design a Multi-Region DR strategy (Pilot Light vs Warm Standby).
- Test Route53 Failover routing.
---
## Day 70 – Backup and Snapshot Automation
#### Lab Tasks:
- Configure AWS Backup policies for EC2 and RDS.
- Automate cross-region snapshot copies.
---
## Day 71 – Multi-Cloud Deployments (AWS + Azure)
#### Lab Tasks:
- Provision resources on AWS and Azure using Terraform.
- Manage multiple providers in main.tf.
---
## Day 72 – EKS Cluster Setup with Terraform
#### Lab Tasks:
- Create EKS Cluster using Terraform (or eksctl).
- Verify kubectl connectivity and node groups.
---
## Day 73 – Jenkins Pipelines for Kubernetes
#### Lab Tasks:
- Write Jenkinsfile for Push-based CD.
- Build Docker image and update K8s deployment.
---
## Day 74 – Serverless ETL Pipeline
#### Lab Tasks:
- Create Lambda function triggered by S3 upload.
- Process CSV data and insert into DynamoDB.
---
## Day 75 – Logging and Monitoring for Production Apps
#### Lab Tasks:
- Install CloudWatch Agent.
- Monitor Custom Metrics (Memory, Disk Space).
---
## Day 76 – Real-Time Dashboards with Grafana + Loki
#### Lab Tasks:
- Deploy PLG Stack (Promtail, Loki, Grafana).
- Visualize logs in Grafana.
---
## Day 77 – Automating EC2/Container Backups
#### Lab Tasks:
- Install Velero for Kubernetes backups.
- Backup and Restore a namespace.
---
## Day 78 – GitOps with ArgoCD and FluxCD
#### Lab Tasks:
- Install ArgoCD on K8s.
- Connect to Git repo and sync applications.
---
## Day 79 – CICD for Microservices
#### Lab Tasks:
- Strategies for Monorepo vs Polyrepo.
- Build independent pipelines for services.
- Smart Change Detection.
---
## Day 80 – AWS CodePipeline + CodeDeploy
#### Lab Tasks:
- Create buildspec.yml and appspec.yml.
- Native AWS CI/CD pipeline creation.
---
## Day 81 – X-Ray for Tracing Microservices
#### Lab Tasks:
- Instrument application with X-Ray SDK.
- Visualize service map and latency.
---
## Day 82 – Handling Multi-Environment Deployments
#### Lab Tasks:
- Manage Dev, Staging, Prod configs.
- Parameterize build specs.
---
## Day 83 – End-to-End Infrastructure Automation
#### Lab Tasks:
- Terraform + UserData for full stack provisioning.
- Bootstrap application from scratch.
---
## Day 84 – Building a DevSecOps Pipeline
#### Lab Tasks:
- Integrate Trivy image scanner in Jenkins.
- Fail builds on security vulnerabilities.
---
## Day 85 – High Availability Setup on AWS
#### Lab Tasks:
- Configure Auto Scaling Groups (ASG) and Application Load Balancer (ALB).
- Test failover across Availability Zones.
---
## Day 86 – Real-Time Alerts and Notifications
#### Lab Tasks:
- Configure SNS and Lambda for Slack notifications.
- Alert on specific keywords.
---
## Day 87 – Debugging and Troubleshooting Production Systems
#### Lab Tasks:
- Debugging Crashing Pods (CrashLoopBackOff).
- Root Cause Analysis methodologies.
---
## Day 88 – Final Real-World Deployment Project
#### Lab Tasks:
- **Full Stack Deployment**: Node.js App + MongoDB.
- **Tools**: EKS, Jenkins, ArgoCD, Terraform, Prometheus.
- The ultimate test of your 90-day journey.
---
## Day 89 – Portfolio and Resume Building
#### Lab Tasks:
- Build a GitHub Portfolio Page.
- Document projects with README.md.
- Mock Interview preparation.
---
## Day 90 – Career Roadmap and Final Review
#### Lab Tasks:
- Certification Path (Solutions Architect / DevOps Professional).
- Continuous Learning roadmap.
- Final course wrap-up.
---

🎯 Action for Everyone:
Post your learnings in our LinkedIn group, tag me, and share any screenshots or key takeaways. Let’s build a visible DevOps learning community!

---
