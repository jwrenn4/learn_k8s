# Module 02: Config & Storage

In Module 01, we deployed a Pod. However, that Pod was "hardcoded." If we wanted to change the Nginx welcome page or a database password, we'd have to rebuild the image or edit the Pod YAML. 

In this module, we'll learn how to separate **Configuration** from **Code** and how to handle **Persistent Data**.

## ⚙️ Configuration: ConfigMaps and Secrets

### ConfigMaps
A **ConfigMap** is used to store non-confidential data in key-value pairs. You can inject these as environment variables or mount them as files in a pod.

### Secrets
**Secrets** are similar to ConfigMaps but are used for sensitive data (passwords, tokens, keys). In a real cluster, Secrets are encrypted at rest; in Kind, they are base64 encoded.

### Hands-on: Using a ConfigMap
1. Create a `configmap.yaml`:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_COLOR: "blue"
  APP_MODE: "development"
```

2. Create a `pod-with-config.yaml` that uses this ConfigMap:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: config-pod
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    env:
    - name: UI_COLOR
      valueFrom:
        configMapKeyRef:
          name: app-config
          key: APP_COLOR
```

3. Apply both and check the env variable inside the pod:
```bash
kubectl apply -f configmap.yaml
kubectl apply -f pod-with-config.yaml
kubectl exec config-pod -- env | grep UI_COLOR
```

## 💾 Storage: Volumes, PVs, and PVCs

Pods are ephemeral. If a pod is deleted, all data written to its local container filesystem is lost. To save data, we use **Volumes**.

### The Storage Hierarchy
1. **PersistentVolume (PV)**: A piece of storage in the cluster (like a physical disk).
2. **PersistentVolumeClaim (PVC)**: A request by a user for storage. "I need 1Gi of space."
3. **StorageClass**: A way to dynamically provision PVs.

### Hands-on: Persistent Storage
1. Create a `pvc.yaml`:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: task-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

2. Create a `pod-with-storage.yaml` that mounts this PVC:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: storage-pod
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    volumeMounts:
    - mountPath: "/usr/share/nginx/html"
      name: storage-volume
  volumes:
  - name: storage-volume
    persistentVolumeClaim:
      claimName: task-pvc
```

3. Apply and test:
```bash
kubectl apply -f pvc.yaml
kubectl apply -f pod-with-storage.yaml
# Create a file inside the pod
kubectl exec storage-pod -- sh -c "echo 'Hello from Persistent Storage' > /usr/share/nginx/html/index.html"
# Delete the pod and recreate it
kubectl delete pod storage-pod
kubectl apply -f pod-with-storage.yaml
# Verify the data survived!
kubectl exec storage-pod -- cat /usr/share/nginx/html/index.html
```

---
### 🤖 Agent Checkpoint
**Once you've verified that your data survived the pod deletion, tell the agent:**
*"I've completed the storage exercise. Can you explain why we use a PVC instead of just pointing the Pod directly to a PV?"*
