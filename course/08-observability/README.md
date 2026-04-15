# Module 08: Observability

You've deployed your app, it's scaling, it's secure, and it's managed by Helm. Now, the million-dollar question: **Is it actually working?**

Observability in Kubernetes usually consists of three pillars: **Metrics**, **Logs**, and **Tracing**.

## 📊 Metrics (The "What")

Metrics tell you how many requests your app is handling, how much CPU it's using, and if the error rate is increasing.

### Tools: Prometheus & Grafana
- **Prometheus**: Scrapes metrics from your pods.
- **Grafana**: Visualizes those metrics in beautiful dashboards.

### Hands-on: Exploring Metrics
If you've installed Prometheus via Helm in Module 07, you can now view the metrics.

1. Use `kubectl port-forward` to access the Prometheus UI:
```bash
kubectl port-forward svc/my-prometheus-server 8080:1511 # Replace with actual service name
```
2. Browse to `http://localhost:8080` and see the system-wide metrics.

## 📜 Logs (The "Why")

Logs provide the detailed context of why a specific error happened.

### Tools: Fluentd, Loki, ELK Stack
- **Loki** (Grafana's "logging" database) is excellent for K8S.
- **ELK** (Elasticsearch, Logstash, Kibana) is the industry standard.

### Hands-on: Centralized Logging
Since we are on a local cluster, we'll use `kubectl logs`. 

1. Try to intentionally crash a pod by giving it an image that doesn't exist:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: crash-pod
spec:
  containers:
  - name: nginx
    image: nginx:non-existent-version
```
2. apply it, then run:
```bash
kubectl describe pod crash-pod
# Look at the 'Events' section. This is the "observability" of the K8S control plane.
```

## 🕵️ Tracing (The "Where")

Tracing allows you to follow a single request as it travels across multiple services (e.g., Frontend -> Backend -> Database).

### Tools: Jaeger, OpenTelemetry
Tracing is require's a change in your application code (instrumentation).

---
### 🤖 Agent Checkpoint
**Once you've explored the Prometheus UI and analyzed a crash event using `kubectl describe`, tell the agent:**
*"I've looked at my metrics and logs. Can you explain the difference between a 'Metric' and a 'Log', and why do we need both for effective debugging?"*
