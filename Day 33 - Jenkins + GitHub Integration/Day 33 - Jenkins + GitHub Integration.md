# Day 33 - Jenkins + GitHub Integration
Welcome to **Day 33** of our DevOps 90-Day Challenge!
Yesterday, you installed Jenkins on AWS EC2.
Today, we’ll integrate Jenkins with **GitHub** so your pipelines can trigger automatically when code changes are pushed.

[![](https://img.youtube.com/vi/3LUGdzzitgw/0.jpg)](https://www.youtube.com/watch?v=3LUGdzzitgw)

[Watch the video](https://www.youtube.com/watch?v=3LUGdzzitgw)

---

## Objective

By the end of this session, you will:

* Connect **Jenkins** with **GitHub**.
* Configure **GitHub Webhooks**.
* Automate Jenkins builds on code push events.

---

## Tools Used

* **Jenkins (Day 32 setup on EC2)**
* **GitHub Repository** (sample app)
* **Jenkins Git Plugin**
* **GitHub Webhooks**

---

## Step-by-Step Guide

### 1. Install Git Plugin in Jenkins

* Go to: **Manage Jenkins → Plugins → Available Plugins**
* Search: **Git Plugin**
* Install & Restart Jenkins

---

### 2. Create a GitHub Repository

* Create a sample repo (e.g., `hello-jenkins`)
* Add a simple `index.html` or code project
* Push code to GitHub

---

### 3. Configure Git in Jenkins

On your Jenkins server:

```bash
sudo apt install git -y
git --version
```

---

### 4. Create Jenkins Job

* New Item → **Freestyle Project** → Name: `github-integration-demo`
* Source Code Management → **Git**

  * Repo URL: `https://github.com/<username>/hello-jenkins.git`
* Build Triggers → Select **GitHub hook trigger for GITScm polling**
* Save

---

### 5. Configure GitHub Webhook

* Go to your GitHub repo → **Settings → Webhooks → Add Webhook**
* Payload URL: `http://<EC2_PUBLIC_IP>:8080/github-webhook/`
* Content type: `application/json`
* Events: Select **Push Events**
* Save

---

### 6. Test the Integration

* Make a small change in your repo:

```bash
echo "Hello Jenkins Integration" >> index.html
git add .
git commit -m "Testing Jenkins GitHub integration"
git push origin main
```

* Jenkins job should trigger automatically

---

## Verification

* Jenkins build is triggered instantly after GitHub push.
* Build logs show the updated commit.
* No manual build click needed.

---

## Bonus (Advanced)

* Use **GitHub Personal Access Token** for private repos.
* Integrate with **Jenkinsfile** instead of Freestyle job.
* Send build status back to GitHub PR.

---

## Key Concepts Applied

| Concept          | Example Used                          |
| ---------------- | ------------------------------------- |
| CI/CD Automation | Auto-trigger build on GitHub push     |
| SCM Integration  | Jenkins Git plugin                    |
| Webhooks         | GitHub webhook triggering Jenkins job |

---

## Congratulations!

You’ve now connected **Jenkins with GitHub**
From here, you can build pipelines that automatically deploy whenever your code changes!

---

## Try These Next

* Create a **Pipeline job** using `Jenkinsfile`.
* Integrate with **GitHub Actions** as comparison.
* Add **Slack notifications** for build success/failure.

