# Module 01: Basics

Now that your cluster is running, let's understand how Kubernetes works and deploy your first workload.

## 🧠 Core Concepts

### What is a Pod?
A **Pod** is the smallest deployable unit in Kubernetes. It represents a single instance of a running process in your cluster. A Pod can contain one or more containers (usually just one) that share the same network and storage.

### Nodes and Clusters
- **Node**: A physical or virtual machine (in our case, a Docker container managed by Kind).
- **Cluster**: A group of nodes managed by a **Control Plane**.

## 🛠️ Hands-on Workshop

### Exercise 1: Your First Pod
We will create a simple pod running Nginx.

1. Create a file named `pod.yaml`:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

2. Apply the configuration:
```bash
kubectl apply -f pod.yaml
```

3. Verify the pod is running:
```bash
kubectl get pods
```

### Exercise 2: Exploring the Pod
Try these commands to interact with your pod:
- **Describe**: `kubectl describe pod nginx-pod` (See events, IP, and status).
- **Logs**: `kubectl logs nginx-pod` (See the Nginx server logs).
- **Exec**: `kubectl exec -it nginx-pod -- /bin/bash` (Jump inside the container).

## 🧼 Cleanup
To remove the pod:
```bash
kubectl delete -f pod.yaml
```

---
### 🤖 Agent Checkpoint
**Once you've successfully run the pod and executed a command inside it, tell the agent:**
*"I've deployed my first Nginx pod. Can you explain the difference between a Pod and a Container, and tell me why we use Pods instead of just containers in K8S?"*
