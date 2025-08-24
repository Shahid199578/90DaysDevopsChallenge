# Day 36 - GitHub Actions Introduction
Welcome to **Day 36** of the DevOps 90-Day Challenge!
Yesterday, you learned how to write **Jenkinsfiles** and automate pipelines with Jenkins.
Today, you’ll start with **GitHub Actions** — GitHub’s native CI/CD system.

[![](https://img.youtube.com/vi/9_S2T4Wnagk/0.jpg)](https://www.youtube.com/watch?v=9_S2T4Wnagk)

[Watch the video](https://www.youtube.com/watch?v=9_S2T4Wnagk)

---

## Objective

By the end of this session, you will:

* Understand what **GitHub Actions** are.
* Learn the basic structure of a **workflow**.
* Automate your first workflow (build + test).

---

## Tools Used

* **GitHub Repository**
* **GitHub Actions** (built-in CI/CD tool)
* **YAML workflow files**

---

## Project Structure

```bash
myapp/
 ├── .github/
 │    └── workflows/
 │         └── ci.yml
 ├── app.py
 ├── requirements.txt
 └── tests/
      └── test_app.py
```

---

## Step-by-Step Guide

### 1. Create Workflow File

Inside your repo, create:

**`.github/workflows/ci.yml`**

```yaml
name: CI Pipeline

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v3

    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.9'

    - name: Install Dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Run Tests
      run: pytest
```

---

### 2. Commit and Push

```bash
git add .github/workflows/ci.yml
git commit -m "Added GitHub Actions workflow"
git push origin main
```

---

### 3. Check Workflow Execution

* Go to **GitHub → Your Repo → Actions tab**
* See pipeline running automatically on **push**

---

## Verification

* Code is checked out.
* Dependencies installed.
* Tests executed successfully.

---

## Bonus (Extra Learning)

* Add **matrix builds** (Python 3.8, 3.9, 3.10).
* Trigger workflows on **schedule** (cron jobs).
* Use **Marketplace Actions** (e.g., linting, Docker builds).

---

## Key Concepts Applied

| Concept       | Example Used                    |
| ------------- | ------------------------------- |
| Workflow      | `.github/workflows/ci.yml` file |
| Event Trigger | On push & pull\_request         |
| Job + Runner  | `runs-on: ubuntu-latest`        |
| Steps         | Checkout, Setup Python, Test    |

---

## Congratulations!

You have successfully created your **first GitHub Actions workflow**
Now, you can use GitHub Actions to **automate builds, tests, and deployments** directly in your repos.

---

## Try These Next

* Add a **linter check** (flake8).
* Add **build artifact upload** (test reports).
* Add **Docker build & push** step.

