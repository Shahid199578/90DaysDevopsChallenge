# Day 78 - GitOps with ArgoCD and FluxCD

Welcome to **Day 78** of the DevOps 90-Day Challenge!
We touched on GitOps before, but today we compare the two giants: **ArgoCD** vs **FluxCD**. Both are amazing, but they work differently.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the core GitOps principles (Declarative, Versioned, Automated, Reconciled).
* Install **FluxCD** (The "other" GitOps tool).
* Compare ArgoCD (UI-centric) vs Flux (CLI/Controller-centric).
* Deploy an app using Flux Kustomizations.

---

## Tools Used

* **ArgoCD**
* **FluxCD**
* **Git**

---

## Key Concepts

### 1. ArgoCD
*   **Pros**: Beautiful UI, easy to visualize topology, supports Helm/Kustomize/Jsonnet, huge community.
*   **Cons**: Can be resource heavy. Manage via UI can lead to drift if not careful.

### 2. FluxCD
*   **Pros**: Lightweight, "Kubernetes-native" feel (no UI by default), amazing Helm Controller, multi-tenancy.
*   **Cons**: No built-in visual dashboard (needs Weave GitOps), steeper learning curve for debugging.

### 3. The Controller Pattern
Both tools use a Controller.
1.  Read Git Repo.
2.  Read Cluster State.
3.  Diff.
4.  Apply (if diff exists).

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Bootstrapping** | `flux bootstrap github ...` installs Flux *and* commits its own manifests to the repo in one command. |
| **HelmRepository** | Flux Custom Resource that tells the cluster where to find Helm charts (e.g., maintain generic helm repos). |
| **Reconciliation** | Setting `interval: 1m` to force the cluster to check Git every minute. |

---

## Bonus (Extra Learning)

*   Install **Weave GitOps** to get a UI for Flux.
*   Use Flux's "Image Automation" to automatically update the Git repo when a new Docker image is pushed (Automated PRs).

---

## Congratulations!

You now know the two main players in the GitOps space. Choosing between them is a matter of preference (and whether you need a UI).

---

## Try These Next

*   Set up a multi-cluster deployment with Flux.
*   Migrate an app from ArgoCD to Flux.
