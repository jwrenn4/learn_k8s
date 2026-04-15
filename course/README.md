# Comprehensive Kubernetes Learning Path

Welcome to the Kubernetes (K8S) self-paced course. This repository is designed to take you from zero to a proficient K8S practitioner using entirely local tools.

## 🎓 How to use this course
Each section is designed to be a "module". 
1. **Read the Guide**: Start with the `README.md` in each folder.
2. **Hands-on Labs**: Follow the provided exercises.
3. **Agent Interaction**: When you hit a "Checkpoint", you can call upon your AI agent to:
   - Review your YAML files.
   - Help you debug a Pod that won't start.
   - Explain a concept in more detail.
   - Verify that your cluster state matches the goal.

## 🗺️ Course Syllabus

### [00 Setup](./00-setup)
- Installing local clusters (Kind/Minikube).
- Installing `kubectl`.
- Verifying your environment.

### [01 Basics](./01-basics)
- What is K8S? (The Architecture).
- Pods: The smallest unit of deployment.
- Nodes and Clusters.
- Basic `kubectl` commands.

### [02 Config & Storage](./02-config-storage)
- ConfigMaps: Managing environment variables.
- Secrets: Handling sensitive data.
- Volumes & PersistentVolumes (PV/PVC).
- Storage Classes.

### [03 Networking](./03-networking)
- ClusterIP: Internal communication.
- NodePort: Exposing services to the host.
- LoadBalancer: (Local implementation).
- Ingress Controllers: Routing traffic.

### [04 Workloads](./04-workloads)
- Deployments: Maintaining desired state.
- ReplicaSets: Scaling pods.
- StateFulSets: Handling stateful apps (databases).
- DaemonSets: Running pods on every node.
- Jobs & CronJobs.

### [05 Scaling & Resource Management](./05-scaling)
- Resource Requests & Limits (CPU/RAM).
- Horizontal Pod Autoscaler (HPA).
- Vertical Pod Autoscaler (VPA).
- Node Autoscaling concepts.

### [06 Security](./06-security)
- RBAC (Role Based Access Control).
- Service Accounts.
- Network Policies (Locking down traffic).
- Pod Security Standards.

### [07 Helm](./07-helm)
- What is Helm? (The Package Manager).
- Creating your first Chart.
- Managing releases and versions.

### [08 Observability](./08-observability)
- Liveness & Readiness Probes.
- Logging (kubectl logs).
- Monitoring basics (Prometheus/Grafana introduction).

### [09 Final Project](./09-final-project)
- Architecting and deploying a multi-tier application locally.
- Implementing scaling, security, and networking.

---
**Ready to start?** Head over to [`00-setup`](./00-setup)!
