# Learn Kubernetes: A Hands-on Journey

Welcome to the **Learn Kubernetes** repository! This repository is designed as an interactive, hands-on course to guide you from Kubernetes basics to advanced concepts using real-world practical exercises.

## 🚀 Overview

Unlike traditional tutorials, this course is built around a **Socratic teaching method**. While you can follow the instructions on your own, this repository is optimized to be used alongside an AI assistant (like Claude, GPT-4, or any LLM). The goal is to not just follow instructions, but to understand the *why* behind every command.

Each module builds upon the previous one, introducing new Kubernetes primitives, configuration strategies, and operational patterns.

## 🛠️ Prerequisites

Before you begin, ensure you have the following tools installed on your local machine:

- [Docker](https://docs.docker.com/get-docker/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [kind (Kubernetes in Docker)](https://kind.sigs.k8s.io/docs/user/quick-start/)

## 📚 Course Curriculum

The course is divided into modules that progressively increase in complexity:

| Module | Topic | Description |
| :--- | :--- | :--- |
| **00** | **Setup** | Installing the necessary tools and spinning up your first cluster with `kind`. |
| **01** | **Basics** | Understanding Pods, Containers, and the basic Kubernetes API. |
| **02** | **Config & Secrets** | Managing application configuration using ConfigMaps and Secrets. |
| **03** | **Networking** | Exploring Services, ClusterIP, NodePort, and LoadBalancers. |
| **04** | **Workloads** | Scaling and managing applications with Deployments and ReplicaSets. |
| **05** | **Scaling** | Implementing Horizontal Pod Autoscalers (HPA). |
| **06** | **Security** | Implementing security best practices in Kubernetes. |
| **07** | **Helm** | Managing Kubernetes applications using Helm charts. |
| **08** | **Observability** | Monitoring and logging your cluster. |
| **09** | **Final Project** | Putting it all together in a real-world scenario. |

## 🤖 How to use with an AI Assistant

To get the most out of this course, use an AI assistant as your tutor. 

1. **Clone the repo:** `git clone https://github.com/your-username/learn-kubernetes.git`
2. **Navigate to a module:** e.g., `cd course/01-basics`
3. **Prompt your AI:** Upload the contents of the module's files to your AI assistant and say:
   > *"I am following a Kubernetes course. I have provided the files for Module 01. Please act as my tutor. Guide me through the exercises, ask me challenging questions, and help me understand the underlying concepts if I get stuck."*

## 🏗️ Architecture

The course is structured as follows:

```text
.
├── AGENTS.md           # Instructions for AI agents
├── course/
│   ├── 00-setup/       # Environment setup instructions
│   ├── 01-basics/      # Pods, Containers, and basic commands
│   ├── 02-config-storage/ # ConfigMaps and Storage
│   ├── 03-networking/  # Services and Networking
│   ├── 04-workloads/   # Deployments and Sets
│   ├── 05-scaling/     # Scaling and HPA
│   ├── 06-security/    # Security best practices
│   ├── 07-helm/        # Helm package management
│   ├── 08-observability/ # Monitoring and Logging
│   └── 09-final-project/ # Capstone module
└── README.md           # This file
```

## 📜 License

This project is open-source and available under the MIT License.
