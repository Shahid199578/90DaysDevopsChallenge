# Day 38 - Advanced GitHub Actions with Secrets and Artifacts
Welcome to **Day 38** of the DevOps 90-Day Challenge!
Yesterday, you built multi-job workflows with GitHub Actions.
Today, we’ll dive into **advanced features**: managing **secrets** and using **artifacts** for sharing files between jobs.

[![](https://img.youtube.com/vi/L3tYdqmvQw0/0.jpg)](https://www.youtube.com/watch?v=L3tYdqmvQw0)

[Watch the video](https://www.youtube.com/watch?v=L3tYdqmvQw0)
---

## Objective

By the end of this session, you will:

* Store and use **GitHub Secrets** securely.
* Upload and download **artifacts** between jobs.
* Automate end-to-end CI/CD with sensitive data handling.

---

## Tools Used

* **GitHub Actions**
* **GitHub Secrets**
* **Artifacts (actions/upload-artifact, actions/download-artifact)**

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

### 1. Add Secrets in GitHub

* Go to **Repo → Settings → Secrets → Actions → New repository secret**
* Example:

  * `DOCKER_USERNAME`
  * `DOCKER_PASSWORD`
  * `API_KEY`

---

### 2. Using Secrets in Workflow

```yaml
  build-and-push:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Docker Login
        run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin
      - name: Build & Push Docker Image
        run: docker build -t myapp:latest .
```

---

### 3. Upload Artifacts Between Jobs

* Save test results or build outputs as artifacts:

```yaml
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run Tests
        run: pytest --junitxml=result.xml
      - name: Upload Test Results
        uses: actions/upload-artifact@v3
        with:
          name: test-results
          path: result.xml

  analyze:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - uses: actions/download-artifact@v3
        with:
          name: test-results
          path: ./results
      - name: Show Test Results
        run: cat ./results/result.xml
```

---

### 4. Full Workflow Example

```yaml
name: CI with Secrets and Artifacts

on:
  push:
    branches: [ "main" ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run Tests
        run: pytest --junitxml=result.xml
      - name: Upload Test Results
        uses: actions/upload-artifact@v3
        with:
          name: test-results
          path: result.xml

  build-and-push:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - uses: actions/checkout@v3
      - name: Docker Login
        run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin
      - name: Build & Push Docker Image
        run: docker build -t myapp:latest .
      - name: Download Test Results
        uses: actions/download-artifact@v3
        with:
          name: test-results
```

---

## Verification

* Secrets used securely, not printed in logs.
* Artifacts available in downstream jobs.
* Docker image built only after tests pass.

---

## Bonus (Advanced)

* Use **environment secrets** for multi-environment pipelines.
* Encrypt additional sensitive files with GitHub Actions.
* Integrate **Slack notifications** for artifact uploads.

---

## 🧠 Key Concepts Applied

| Concept          | Example Used                                  |
| ---------------- | --------------------------------------------- |
| Secrets          | `DOCKER_USERNAME`, `DOCKER_PASSWORD`          |
| Artifacts        | `actions/upload-artifact` & download-artifact |
| Job Dependencies | `needs: test`                                 |
| Secure CI/CD     | Sensitive info handled safely                 |

---

## Congratulations!

You’ve mastered **advanced GitHub Actions** features!
Now your workflows can safely handle secrets and share artifacts between jobs, just like production pipelines.

---

## Try These Next

* Add **multi-environment secrets** (dev/staging/prod).
* Store build logs or coverage reports as artifacts.
* Trigger deploy jobs only on **successful artifact upload**.

