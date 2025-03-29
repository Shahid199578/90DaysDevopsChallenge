# Day 5: Introduction to Version Control (Git and GitHub)

## 1. Introduction to Version Control

### What is Version Control?
- A system that records changes to files over time.
- Allows you to recall specific versions later.
- Keeps track of every modification to a project.
- Helps manage collaboration and maintain project history.

### Why Use Version Control?
1. **Collaboration:** Multiple developers can work on the same project without conflicts.
2. **Version Tracking:** Keeps a detailed history of changes.
3. **Backup:** Restore any previous version when needed.
4. **Branching and Merging:** Experiment with new features without affecting the main code.
5. **Deployment Automation:** Integrate with CI/CD pipelines.

---

## 2. Git Basics

### What is Git?
- A distributed version control system developed by Linus Torvalds.
- Tracks changes in source code during software development.
- Operates locally without the need for a central server.

### What is GitHub?
- A cloud-based platform for hosting Git repositories.
- Facilitates collaboration and project management.
- Provides features like pull requests, issues, and GitHub Actions.

---

## 3. Setting Up Git

### Step 1: Install Git
- **Windows:** Download and install from [Git for Windows](https://git-scm.com/download/win).

- **Linux (Ubuntu):**
  ```sh
  sudo apt update
  sudo apt install git
  ```
- **Verify the installation:**
  ```sh
  git --version
  ```

### Step 2: Configure Git
- Set up your username and email:
  ```sh
  git config --global user.name "Your Name"
  git config --global user.email "youremail@example.com"
  ```
- Check configuration:
  ```sh
  git config --list
  ```

---

## 4. Initializing a Git Repository

### Step 1: Create a New Project Folder
```sh
mkdir devops-series
cd devops-series
```

### Step 2: Initialize Git
```sh
git init
```
- Creates a new, empty Git repository.

### Step 3: Add a README File
```sh
echo "# DevOps Series" > README.md
```

### Step 4: Track Changes
```sh
git add README.md
```
- Stages the file for the next commit.

---

## 5. Committing Changes

### Step 1: Make Your First Commit
```sh
git commit -m "Initial commit: Added README file"
```
- Records the changes to the repository.

### Step 2: Check Commit Log
```sh
git log
```
- Shows the history of commits.

---

## 6. Pushing Code to GitHub

### Step 1: Create a GitHub Repository
1. Go to GitHub and sign in.
2. Click "New" to create a new repository.
3. Set the repository name (e.g., `devops-series`).
4. Choose Public or Private visibility.
5. Click "Create repository".

### Step 2: Link Local Repository to GitHub
```sh
git remote add origin https://github.com/username/devops-series.git
```

### Step 3: Push Changes
```sh
git push -u origin master
```

---

## 7. Branching and Merging

### Step 1: Create a New Branch
```sh
git branch feature-branch
```

### Step 2: Switch to the New Branch
```sh
git checkout feature-branch
```

### Step 3: Make Changes and Commit
```sh
echo "Feature update" >> README.md
git add README.md
git commit -m "Added feature update"
```

### Step 4: Merge Branch into Master
1. Switch back to the master branch:
   ```sh
   git checkout master
   ```
2. Merge the feature branch:
   ```sh
   git merge feature-branch
   ```
3. Delete the branch after merging:
   ```sh
   git branch -d feature-branch
   ```

---

## 8. Collaborating with GitHub

### Step 1: Forking a Repository
- Fork a repository to have your own copy to make changes.

### Step 2: Cloning the Forked Repository
```sh
git clone https://github.com/username/devops-series.git
```

### Step 3: Creating Pull Requests (PRs)
1. Make changes on your local repository.
2. Push the changes to your GitHub fork:
   ```sh
   git push origin feature-branch
   ```
3. Open a Pull Request from your fork to the original repository.
4. Add a meaningful title and description.
5. Submit the PR for review.

---

## 9. Handling Conflicts

### Step 1: Identify Conflicts
- Occurs when changes from different branches affect the same line of code.
- Git will mark conflicts like this:
  ```sh
  <<<<<<< HEAD
  Code from current branch
  =======
  Code from merging branch
  >>>>>>> feature-branch
  ```

### Step 2: Resolve Conflicts
- Manually edit the file to resolve the differences.

### Step 3: Add and Commit the Resolved File
```sh
git add resolved_file.txt
git commit -m "Resolved merge conflict"
```

---

## 10. Git Best Practices

1. **Meaningful Commit Messages:**
   - Follow the format: `type(scope): description`
   - Example: `feat(auth): add login functionality`
2. **Use Branches for Features and Bug Fixes:**
   - Keeps the master branch clean.
3. **Pull Latest Changes Before Pushing:**
   ```sh
   git pull origin master
   ```
4. **Review Pull Requests Carefully:**
   - Ensure quality and consistency before merging.
5. **Backup Your Work:**
   - Push regularly to avoid losing progress.

---

## 11. Hands-On Activity

### Task 1: Version Control with Git
1. Create a new repository on GitHub.
2. Clone it to your local machine.
3. Add a README file and make some changes.
4. Push the changes to the remote repository.

### Task 2: Collaboration with GitHub
1. Fork a public repository.
2. Make changes and submit a Pull Request.
3. Resolve any conflicts and merge the PR.
