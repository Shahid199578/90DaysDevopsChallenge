# Day 37 - Building Workflows with GitHub Actions
Welcome to **Day 37** of the DevOps 90-Day Challenge!
Yesterday, you created your **first GitHub Actions workflow**.
Today, you’ll go deeper by building **advanced workflows** with:

* Multiple jobs
* Matrix builds
* Job dependencies

[![](https://img.youtube.com/vi/7-J8UjY7-Tw/0.jpg)](https://www.youtube.com/watch?v=7-J8UjY7-Tw)

[Watch the video](https://www.youtube.com/watch?v=7-J8UjY7-Tw)
---

## Objective

By the end of this session, you will:

* Write **multi-job workflows**.
* Create **matrix builds** for testing across environments.
* Understand **job dependencies** (`needs:`).

---

## Tools Used

* **GitHub Actions**
* **YAML workflows**
* **Python App Example**

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

### 1. Multi-Job Workflow

Update `.github/workflows/ci.yml`:

```yaml
name: Multi-Job CI Pipeline

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install flake8
        run: pip install flake8
      - name: Run Linter
        run: flake8 .

  test:
    runs-on: ubuntu-latest
    needs: lint   # test runs only after lint
    steps:
      - uses: actions/checkout@v3
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: "3.9"
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run Tests
        run: pytest
```

---

### 2. Matrix Builds

Run tests on **multiple Python versions**:

```yaml
  test:
    runs-on: ubuntu-latest
    needs: lint
    strategy:
      matrix:
        python-version: [3.8, 3.9, 3.10]
    steps:
      - uses: actions/checkout@v3
      - name: Setup Python ${{ matrix.python-version }}
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run Tests
        run: pytest
```

---

### 3. Add a Build Job

After tests pass, add a **build job**:

```yaml
  build:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - uses: actions/checkout@v3
      - name: Docker Build
        run: docker build -t myapp:latest .
```

---

## Verification

* Lint → Test → Build runs in sequence.
* Tests run across **multiple Python versions**.
* Build job only runs if **previous jobs succeed**.

---

## Bonus (Extra Learning)

* Use **caching** (`actions/cache`) for faster builds.
* Add **conditional jobs** (`if:` syntax).
* Run jobs in **parallel** vs **sequentially**.

---

## Key Concepts Applied

| Concept              | Example Used                 |
| -------------------- | ---------------------------- |
| Multiple Jobs        | lint, test, build            |
| Dependencies         | `needs: lint`, `needs: test` |
| Matrix Builds        | Python 3.8, 3.9, 3.10        |
| Sequential Execution | Lint → Test → Build pipeline |

---

## Congratulations!

You’ve built an **advanced GitHub Actions workflow** with:

* Multi-job pipelines
* Dependencies
* Matrix builds

This is exactly how real-world projects maintain **cross-version compatibility** and enforce **code quality**.

---

## Try These Next

* Add a **deploy job** after build (to AWS/GCP).
* Add **scheduled workflows** (run daily).
* Experiment with **self-hosted runners**.

