# Day 49 - Ansible + Jenkins Integration

Welcome to **Day 49** of the DevOps 90-Day Challenge!
Today, we’ll integrate our **Configuration Management** tool (Ansible) with our **CI/CD** tool (Jenkins) to build a seamless deployment pipeline.

[![](https://img.youtube.com/vi/eJIu2ehF098/0.jpg)](https://www.youtube.com/watch?v=eJIu2ehF098)

[Watch the video](https://www.youtube.com/watch?v=eJIu2ehF098)

---

## Objective

By the end of this session, you will:

* Install and configure the **Ansible Plugin** in Jenkins.
* Trigger **Ansible Playbooks** directly from a Jenkins Pipeline.
* Automate the deployment of an application using CI/CD.

---

## Tools Used

* **Jenkins** (CI Server)
* **Ansible** (Configuration Management)
* **Git** (Version Control)
* **Remote Hosts** (Target Servers)

---

## Key Concepts

### 1. Why Integrate?

* **Continuous Deployment**: Jenkins builds artifacts; Ansible deploys them.
* **Consistency**: Automated runs ensure the same configuration every time.
* **Visibility**: Jenkins logs provide clear output of Ansible runs.

### 2. Jenkinsfile Sample

```groovy
pipeline {
    agent any

    stages {
        stage('SCM Checkout') {
            steps {
                git 'https://github.com/myuser/my-ansible-repo.git'
            }
        }
        
        stage('Deploy with Ansible') {
            steps {
                ansiblePlaybook(
                    playbook: 'site.yml',
                    inventory: 'inventory/prod.ini',
                    credentialsId: 'ssh-private-key'
                )
            }
        }
    }
}
```

### 3. Handling Secrets

Use **Jenkins Credentials** to securely store the SSH private keys needed by Ansible to connect to managed nodes.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Pipeline-as-Code** | Defining the deployment logic in a `Jenkinsfile`. |
| **Jenkins Plugin** | `Ansible` plugin used to execute `ansible-playbook`. |
| **Credentials Binding** | Injecting SSH keys safely into the pipeline. |

---

## Bonus (Extra Learning)

* Try passing **Build Parameters** from Jenkins to Ansible as "Extra Variables".
* Set up a **Webhook** to trigger deployment on Git push.

---

## Congratulations!

You’ve successfully integrated **Ansible with Jenkins**!
Your pipeline now bridges the gap between Code (Git) and Operations (Server Config).

---

## Try These Next

* Add a **Test Stage** that verifies the application is up (`curl localhost`) after deployment.
* Implement a **Rollback** stage in case of failure.
