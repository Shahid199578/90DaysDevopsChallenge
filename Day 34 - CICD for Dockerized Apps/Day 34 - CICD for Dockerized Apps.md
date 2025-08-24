# Day 34 - CI/CD for Dockerized Apps
Welcome to **Day 34** of the DevOps 90-Day Challenge!
Yesterday, you integrated **Jenkins with GitHub**.
Today, you’ll take it a step further by building a **CI/CD pipeline for Dockerized applications**.

[![](https://img.youtube.com/vi/pAsUEqQ1eKI/0.jpg)](https://www.youtube.com/watch?v=pAsUEqQ1eKI)

[Watch the video](https://www.youtube.com/watch?v=pAsUEqQ1eKI)
---

## Objective

By the end of this session, you will:

* Build and push a **Docker image** with Jenkins.
* Run a container automatically after code changes.
* Automate end-to-end CI/CD for containerized apps.

---

## Tools Used

* **Jenkins** (with Docker plugin installed)
* **Docker Hub** (registry for images)
* **GitHub Repository** (Dockerized app)
* **AWS EC2 (Jenkins host)**

---

## Project Structure

```bash
dockerized-app/
 ├── Dockerfile
 ├── app.py
 └── requirements.txt
```

**Dockerfile Example**

```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
```

---

## Step-by-Step Guide

### 1. Install Docker on Jenkins Server

```bash
sudo apt update
sudo apt install docker.io -y
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

*(Logout & re-login to apply group changes)*

---

### 2. Create Docker Hub Credentials in Jenkins

* Go to **Manage Jenkins → Credentials → Global**
* Add new credentials:

  * ID: `docker-hub`
  * Username: `<your-dockerhub-username>`
  * Password: `<your-dockerhub-password>`

---

### 3. Jenkins Pipeline Script (CI/CD)

Create a **Pipeline job** and use this script:

```groovy
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "your-dockerhub-username/dockerized-app"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/<username>/dockerized-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE:$BUILD_NUMBER .'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                      echo "$PASS" | docker login -u "$USER" --password-stdin
                      docker push $DOCKER_IMAGE:$BUILD_NUMBER
                    '''
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name myapp $DOCKER_IMAGE:$BUILD_NUMBER'
            }
        }
    }
}
```

---

### 4. Test the Pipeline

* Push code changes to GitHub
* Jenkins should:
  Pull code → Build Docker image → Push to Docker Hub → Run container

Check running container:

```bash
docker ps
```

Access app via `http://<EC2_PUBLIC_IP>:5000`

---

## Verification

* Confirm image is available on **Docker Hub**.
* App is running inside a container.
* Jenkins pipeline runs automatically on code push.

---

## Key Concepts Applied

| Concept          | Example Used              |
| ---------------- | ------------------------- |
| CI/CD Automation | Jenkins Pipeline          |
| Dockerization    | Build & Push Docker Image |
| Deployment       | Run container after build |

---

## Congratulations!

You’ve built your **first Dockerized CI/CD pipeline** with Jenkins
Now, every code push can ship a new container image!

---

## Try These Next

* Replace **Freestyle jobs** with **Declarative Pipelines**.
* Deploy app on a **Kubernetes cluster** instead of EC2.
* Add **version tags** (e.g., `latest`, `v1.0.0`).

