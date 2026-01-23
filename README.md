# Larr1 ML Computing Cluster (Experimental)

Larr1 ML Computing Cluster is an **experimental, self-managed GPU computing cluster** built as a side project to support machine learning training and experimentation.

It runs on a **two-node NVIDIA DGX Spark cluster** and provides isolated, HTTPS-accessible workspaces through a simple Git-based workflow.

The goal is to make shared GPU computing **easy to use, hard to misuse**, and fun to build.

---

## More About This Project

This project explores:

- Running a real GPU **computing cluster** on Kubernetes
- Managing ML workspaces via **GitOps (Argo CD + Helm)**
- Providing per-user isolation without exposing infrastructure complexity
- Operating shared GPU resources responsibly

The system is split into two repositories:

- **Infrastructure repo**  
  Handles Kubernetes, GPU scheduling, ingress, TLS, Argo CD, and Helm charts.

- **User repo**  
  Where users declare *what they want*, not *how things work*.

If you can write YAML and open a PR, you can use the cluster.

---

## Getting Started

Using the cluster is intentionally simple.

### 1 Clone the User Repository

```bash
git clone <user-repo-url>
cd user-repo
```

---

### 2 Add Your Workspace YAML

Create a YAML file under the `user/` directory.

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
  # your name
  username: aaa

  # Email address to receive:
  # - Workspace ready notification
  email: aaa@example.com


profile:
  # Resource profile of this workspace.
  #
  # Choose ONE of the following:
  #
  # small  → 1 GPU (16GB VRAM)
  # medium → 1 GPU (24GB VRAM)
  # large  → 1 GPU (32GB VRAM)
  #
  # CPU and memory are managed automatically by the platform.
  # You only need to care about GPU memory size here.
  name: medium        # small | medium | large


cuda:
  # CUDA runtime version inside the container.
  #
  # Notes:
  # - The platform runs NVIDIA GPU drivers on the host with backward compatibility.
  # - This setting controls the user-space CUDA runtime and toolkit
  #   available inside the workspace container.
  # - It does NOT change the host GPU driver version.
  #
  # Recommended:
  # - cuda12.9 → default and most stable
  # - cuda13.0 → newer features, experimental
  version: cuda12.9   # cuda12.8 | cuda12.9 | cuda13.0


storage:
  # default 
  size: 100Gi
```

---

### 3 Open a Pull Request

- Commit your YAML
- Open a PR
- After approval, the cluster takes care of the rest

Once ready, you’ll receive an email with:

- Workspace URL
- Username
- Initial password

---

## 🎮 Rules of the Game

This is a **shared experimental computing cluster**.

Please:

- Use it for **ML training, experiments, and research**
- Be mindful of GPU, CPU, and memory usage
- Clean up resources you no longer need

Please **do not**:

- Run production services or public APIs
- Bypass resource limits
- Use the cluster as a general-purpose hosting platform

If something breaks, it’s probably part of the experiment 🙂

---

## Experimental Status

This cluster is **actively evolving**.

- Features may change
- Tooling is still being improved
- Some rough edges are expected

Feedback is very welcome.

---

## Contact & Feedback

If you hit issues, have suggestions, or just want to give feedback:

📧 **xhw.14616@gmail.com**

Please include your workspace name if applicable.
