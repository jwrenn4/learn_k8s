# Module 00: Setup

Before we can deploy any apps, we need a "Cluster". Since we aren't using a cloud provider (AWS, GCP, Azure), we will run a local cluster.

## 🛠️ Tools We'll Use

1. **Docker**: The engine that allows us to run containers.
2. **Kind (Kubernetes in Docker)**: A tool for running local Kubernetes clusters. It's faster and more lightweight than Minikube for most learning purposes.
3. **kubectl**: The command-line tool used to talk to the Kubernetes API.

## 🚀 Installation Guide

### 1. Install Docker
If you don't have Docker installed, download and install [Docker Desktop](https://www.docker.com/products/docker-desktop/). Ensure it is running.

### 2. Install kubectl
Depending on your OS:
- **macOS**: `brew install kubectl`
- **Windows**: `choco install kubernetes-cli`
- **Linux**: Use the binary installation from the official [K8S docs](https://kubernetes.io/docs/tasks/tools/).

### 3. Install Kind
- **macOS**: `brew install kind`
- **Windows**: `choco install kind`
- **Linux**: `curl -Lo kind https://kind.kubernetes.io/releases/stable/kind-linux-amd64` then `chmod +x kind` and move to `/bin`.

## 🏗️ Create Your First Cluster

Run the following command in your terminal:

```bash
kind create cluster --name learning-cluster
```

This will pull a node image and start a single-node cluster using Docker.

## ✅ Verifying the Setup

Once the cluster is created, verify that `kubectl` can talk to it:

```bash
kubectl cluster-info
kubectl get nodes
```

---
### 🤖 Agent Checkpoint
**Once you've run the commands above, tell the agent:**
*"I have installed Docker, kubectl, and kind. I created the 'learning-cluster'. Can you check if my cluster is healthy?"*

**What the agent will do:**
The agent will ask you to run `kubectl get nodes` and `kubectl get pods -n kube-system` and will analyze the output to ensure your Control Plane is running correctly.
