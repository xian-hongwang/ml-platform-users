# Larr1 ML Computing Cluster (Experimental)

Larr1 ML Computing Cluster is an **experimental, self-managed GPU computing cluster** built as a side project to support machine learning training and experimentation.

It runs on a **two-node NVIDIA DGX Spark cluster** and provides isolated, HTTPS-accessible workspaces through a simple Git-based workflow.

The goal is to make shared GPU computing **easy to use, hard to misuse**, and fun to build.

---

## Contents

- [Larr1 ML Computing Cluster (Experimental)](#larr1-ml-computing-cluster-experimental)
  - [Contents](#contents)
  - [What Is This](#what-is-this)
  - [Architecture Overview](#architecture-overview)
  - [Getting Started](#getting-started)
    - [1 Fork the User Repository](#1-fork-the-user-repository)
    - [2 Create Your Workspace YAML](#2-create-your-workspace-yaml)
    - [3 Open a Pull Request](#3-open-a-pull-request)
  - [Rules of the Game](#rules-of-the-game)
  - [Experimental Status](#experimental-status)
  - [Contact \& Feedback](#contact--feedback)

---

## What Is This

This project explores how to run a real GPU **computing cluster** using modern infrastructure tools while keeping the user experience intentionally simple.

It focuses on:

- Shared GPU computing on Kubernetes
- GitOps-driven workflow (**Argo CD + Helm**)
- Per-user isolation with minimal operational burden
- Practical, opinionated trade-offs for a small experimental cluster

The system is split into two repositories:

- **Infrastructure repository**  
  Manages Kubernetes, GPU scheduling, ingress, TLS, Argo CD, and Helm charts.

- **User repository (this repo)**  
  Where users declare *what they want*, not *how it works*.

If you can edit YAML and open a Pull Request, you can use the cluster.

---

## Architecture Overview

Below is a high-level view of how the cluster works.

![Larr1 ML Computing Cluster Architecture](./docs/architecture.png)

---

## Getting Started

Using the cluster follows a simple **fork → edit → pull request** workflow.

---

### 1 Fork the User Repository

The `main` branch is protected.

You **must fork** the repository before making changes.

---

### 2 Create Your Workspace YAML

Create **one file** under the `user/` directory.

> ⚠️ **The file extension must be `.yaml`**

Example:

```yaml
# user/aaa.yaml
#
# This file defines a personal workspace on
# Larr1 ML Computing Platform (Experimental).
#
# You only need to modify this file and open a PR.
# The platform will take care of provisioning, networking,
# GPU binding, and credentials automatically.
user:
  username: aaa
  email: aaa@example.com

profile:
# small  → 1 GPU (16GB VRAM)
# medium → 1 GPU (24GB VRAM)
# large  → 1 GPU (32GB VRAM)
  name: medium
# CUDA runtime version inside the container.
#
# Notes:
# - The platform runs NVIDIA GPU drivers on the host with backward compatibility.
# - This setting controls the user-space CUDA runtime and toolkit
#   available inside the workspace container.
# - It does NOT change the host GPU driver version.
#
cuda:
# - cuda12.8 
# - cuda12.9 
# - cuda13.0 
  version: cuda12.9
# default 100Gi
storage:
  size: 100Gi
```

---

### 3 Open a Pull Request

After approval, credentials will be sent via email.

---

## Rules of the Game

This is a **shared experimental computing cluster**.

- ML training and experimentation only
- No production services
- Respect shared resources

---

## Experimental Status

This cluster is **experimental**.

---

## Contact & Feedback

📧 **xhw.14616@gmail.com**
