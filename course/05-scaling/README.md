# Module 05: Scaling & Resource Management

Your application is now running in a cluster. But what if you suddenly get 10,000 users? Or what if one of your Pods starts consuming 100% of the CPU, causing other Pods to crash?

In this module, we'll learn about **Resource Quotas**, **Requests & Limits**, and **HPA**.

## ⚖️ Requests and Limits

Kubernetes needs to know how much CPU and RAM your application needs to avoid "noisy neighbor" problems.

- **Requests**: The minimum amount of resources the pod is guaranteed. The scheduler uses this to decide which node can fit the pod.
- **Limits**: The maximum amount of resources a pod can consume. If a pod exceeds its memory limit, it is **OOMKilled** (Out of Memory).

### Hands-on: Setting Resource Limits
1. Edit your `deployment.yaml` from Module 04 and add a `resources` section:
```yaml
        resources:
          requests:
            memory: "64Mi"
            cpu: "250m"
          limits:
            memory: "128Mi"
            cpu: "500m"
```
*(Note: `250m` means 250 millicores, or 25% of one CPU core).*

2. Re-apply the deployment:
```bash
kubectl apply -f deployment.yaml
```

## 📈 Horizontal Pod Autoscaler (HPA)

The **HPA** automatically increases or decreases the number of replicas based on CPU utilization (or other metrics).

### Setting up HPA
1. First, you must have a **Metrics Server** installed in your cluster. (Kind clusters often need this manually installed).
```bash
kubectl apply -f https://github.com/kubernetes-sig-metrics-server/metrics-server/deploy/sig-silent-ci---+s)releas-cluster-metrics.yaml
```
*(Note: The metrics server might need specific flags like `--kubelet-configurable=true` for local clusters).*

2. Create an HPA resource:
```bash
kubectl autoscale deployment nginx-deployment --cpu-percent=50 --min=1 --max=10
```

3. Stress test your pod to trigger scaling:
```bash
# Run a loop that curls the nginx pod from another pod
kubectl run -i --tty --rm load-generator --image=curlimages/curl -- \
  sh -c "while true; do curl -s http://nginx-deployment; done"
```

4. Watch the replicas increase:
```bash
kubectl get hpa
```

---
### 🤖 Agent Checkpoint
**Once you've successfully set resource limits and seen the HPA trigger a scale-up event, tell the agent:**
*"I've set up HPA and resource limits. Can you explain what happens if I set my memory limit too low, and how I can identify if a pod was OOMKilled?"*
