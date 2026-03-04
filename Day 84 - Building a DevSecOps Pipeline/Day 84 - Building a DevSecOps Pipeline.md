# Day 84 - Building a DevSecOps Pipeline

Welcome to **Day 84** of the DevOps 90-Day Challenge!
Security cannot be an afterthought ("We'll pentest it before launch"). It must be integrated into the pipeline. This is **DevSecOps**.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Integrate **SAST** (Static Application Security Testing).
* Integrate **DAST** (Dynamic Application Security Testing).
* Scan Docker images for vulnerabilities.
* Scan Infrastructure as Code (Terraform) for misconfigurations.

---

## Tools Used

* **SonarQube / SonarCloud** (SAST)
* **OWASP ZAP** (DAST)
* **Trivy** (Container & IaC Scan)
* **Checkov** (Terraform Scan)

---

## Key Concepts

### 1. Shift Left
Moving security checks to the *left* (beginning) of the timeline. Finding a bug in Dev costs $10. Finding it in Prod costs $10,000.

### 2. The Scanners
*   **SAST**: specific checking of source code. "You have a hardcoded password variable." (SonarQube).
*   **SCA (Software Composition Analysis)**: "You are using `lodash v1.0` which has a known vulnerability." (Snyk/Dependabot).
*   **DAST**: "I tried to attack your running app with SQL Injection and it worked." (OWASP ZAP).
*   **IaC Scan**: "Your S3 bucket is public." (Checkov/Trivy).

### 3. Breaking the Build
If a *Critical* vulnerability is found, the pipeline fails. The code *cannot* go to production.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Quality Gate** | Setting SonarQube to fail if Code Coverage < 80%. |
| **Reporting** | Generating a PDF report of vulnerabilities for compliance auditors. |
| **Auto-Fix** | Using Dependabot to automatically open PRs that upgrade vulnerable libraries. |

---

## Bonus (Extra Learning)

*   Run **Trivy** on your local machine before pushing code via a Git Hook.
*   Explore **GitGuardian** to scan for secrets in your git history.

---

## Congratulations!

You are now a DevSecOps Engineer. You don't just ship code; you ship *secure* code.

---

## Try These Next

*   Set up a weekly scheduled scan for long-running containers.
*   Implement Container Runtime Security (Falco).
