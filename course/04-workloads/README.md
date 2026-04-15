# Module 04: Workloads

Until now, we've mostly used Pods. But what happens if a Pod crashes? Or if we need to scale our application to 10 copies for high availability? Creating 10 Pods manually is not the way.

In this module, we'll learn about **Deployments**, **StatefulSets**, and **DaemonSets**.

## 🚀 Deployments: The Workhorse

A **Deployment** ensures that a specified number of Pods are running at all times. It manages **ReplicaSets**, which in turn manage the Pods.

### Key Features:
- **Self-Healing**: If a Pod dies, the Deployment automatically recreates it.
- **Scaling**: Easily change the number of replicas.
- **Rollouts/Rollbacks**: Update your app version without downtime.

### Hands-on: Creating a Deployment
1. Create a `deployment.yaml`:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.21
        ports:
        - containerPort: 80
```

2. Apply it:
```bash
kubectl apply -f deployment.yaml
```

3. Verify 3 pods are running:
```bash
kubectl get pods
```

4. Try "killing" a pod to see self-healing:
```bash
kubectl delete pod <pod-name-from-get-pods>
```
*(The Deployment will immediately create a new one).*

## 📦 StatefulSets: For Databases

Unlike Deployments (where Pods are interchangeable), **StatefulSets** provide a stable, unique network identity for each Pod. Pods are created in order (pod-0, pod-1, etc.) and have their own dedicated storage.

### Hands-on: StatefulSet Basic
1. Create a `statefulset.yaml`:
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql-cluster
spec:
  serviceName: "mysql-service"
  replicas: 3
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:5.7
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: "password123"
```

## 👹 DaemonSets: Ensuring Every Node Has It

A **DaemonSet** ensures that a copy of a Pod is running on every single node in the cluster. This is useful for log collectors (like Fluentd) or monitoring agents (like Prometheus Node Exporter).

### Hands-on: DaemonSet Basic
1. Create a `daemonset.yaml`:
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: log-collector
spec:
  selector:
    matchLabels:
      app: log-collector
    spec:
      template:
        metadata:
          labels:
            app: log-collector
        spec:
          containers:
          - name:Fluentd
            image: fluentd:latest
```

---
### 🤖 Agent Checkpoint
**Once you've tested the self-healing of a Deployment's pods, tell the agent:**
*"I've played with Deployments, StatefulSets, and DaemonSets. Can you explain why I would use a StatefulSet instead of a Deployment for a database like MongoDB or PostgreSQL?"*
