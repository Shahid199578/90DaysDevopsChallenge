# Day 35 - Jenkinsfile and Declarative Pipelines
Welcome to **Day 35** of the DevOps 90-Day Challenge!
Yesterday, you built a **CI/CD pipeline for Dockerized apps**.
Today, you’ll learn to write **Jenkinsfiles** using **Declarative Pipelines**, making your automation reusable and version-controlled.

[![](https://img.youtube.com/vi/dz6fwJuwdZQ/0.jpg)](https://www.youtube.com/watch?v=dz6fwJuwdZQ)

[Watch the video](https://www.youtube.com/watch?v=dz6fwJuwdZQ)

---

## Objective

By the end of this session, you will:

* Understand the structure of a **Declarative Pipeline**.
* Create a **Jenkinsfile** inside your repository.
* Automate builds and deployments using **Pipeline as Code**.

---

## Tools Used

* **Jenkins** (Pipeline plugin)
* **GitHub** (to store Jenkinsfile with source code)
* **Docker Hub** (for image push)

---

## Project Structure

```bash
dockerized-app/
 ├── Jenkinsfile
 ├── Dockerfile
 ├── app.py
 └── requirements.txt
```

---

## Step-by-Step Guide

### 1. Create Jenkinsfile

Add this file in the **root** of your repo:

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
                sh 'docker build -t $DOCKER_IMAGE:$BUILD_NUMBER .'
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

        stage('Deploy') {
            steps {
                sh '''
                  docker rm -f myapp || true
                  docker run -d -p 5000:5000 --name myapp $DOCKER_IMAGE:$BUILD_NUMBER
                '''
            }
        }
    }

    post {
        success {
            echo "Build and deployment successful!"
        }
        failure {
            echo "Build failed. Check logs."
        }
    }
}
```

---

### 2. Configure Jenkins Job

* Go to **Jenkins → New Item → Pipeline**
* Select **Pipeline script from SCM**
* Choose **Git** and paste repo URL
* Jenkins will automatically read **Jenkinsfile** from repo

---

### 3. Test the Jenkinsfile

* Commit & push Jenkinsfile to GitHub
* Run the job → Jenkins will:
  Clone repo → Build Docker image → Push to Docker Hub → Deploy container

---

## Verification

* Jenkins console logs show pipeline execution.
* New Docker image is pushed to **Docker Hub**.
* App is accessible on `http://<EC2_PUBLIC_IP>:5000`.

---

## Bonus (Advanced Jenkinsfile Features)

* Add **parallel stages** (e.g., test + linting at same time).
* Use **when conditions** for environment-specific deployments.
* Add **post actions** for Slack/email notifications.

---

## Key Concepts Applied

| Concept            | Example Used                         |
| ------------------ | ------------------------------------ |
| Pipeline as Code   | Jenkinsfile in GitHub repo           |
| Declarative Syntax | Structured stages and steps          |
| Automation         | Build → Push → Deploy flow automated |

---

## Congratulations!

You have now moved from **manual pipelines** to **Pipeline as Code** with Jenkinsfiles

This is a **huge milestone** in becoming a DevOps engineer!

---

## Try These Next

* Add **unit tests** as a pipeline stage.
* Run multiple environments (**dev/staging/prod**) with `when` conditions.
* Store pipeline in a **shared library** for reuse.

