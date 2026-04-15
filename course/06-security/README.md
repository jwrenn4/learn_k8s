# Module 06: Security

Running a cluster is great, but running it securely is critical. By default, many Kubernetes components are configured for ease of use rather than maximum security.

In this module, we'll explore **RBAC (Role-Based Access Control)**, **Network Policies**, and **Pod Security**.

## 🔑 RBAC: Who can do what?

RBAC allows you to restrict what users or service accounts can do in the cluster. It consists of four main objects:
1. **Role**: Defines permissions within a specific namespace.
2. **ClusterRole**: Defines permissions cluster-wide.
3. **RoleBinding**: Grants the permissions of a Role to a user or group in a namespace.
4. **ClusterRoleBinding**: Grants permissions of a ClusterRole cluster-wide.

### Hands-on: Creating a Read-Only User
1. Create a ServiceAccount:
```bash
kubectl create serviceaccount viewer-account
```

2. Create a Role that only allows `get`, `list`, and `watch` on pods:
```yaml
apiVersion: rbac.authorization.k8sio/v1
kind: Role
metadata:
  namespace: default
  name: pod-viewer
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
```

3. Bind the Role to the ServiceAccount:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
subjects:
- kind: ServiceAccount
  name: viewer-account
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-viewer
  apiGroup: rbac.authorization.k8s.io
```

4. Test the permissions using `auth can-i`:
```bash
kubectl auth can-i get pods --as=system:serviceaccount:default:viewer-account
# Should return "yes"
kubectl auth can-i delete pods --as=system:serviceaccount:default:viewer-account
# Should return "no"
```

## 🛡️ Network Policies: Pod-to-Pod Firewalls

By default, all pods in a cluster can talk to all other pods. **Network Policies** allow you to define which pods can communicate with each other.

### Hands-on: Isolating a Database
Imagine you have a frontend and a database. Only the frontend should be able to talk to the database.

1. Create a Network Policy that allows traffic to the `mysql` pod ONLY from pods with the label `app: frontend`:
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
  podSelector:
    matchLabels:
      app: mysql
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: frontend
```
*(Note: Network Policies require a CNI provider that supports them, like Calico or Cilium. Standard Kind clusters might need extra configuration for this to be enforced).*

## 🔒 Pod Security

Avoiding "Root" containers is a best practice. You can use security contexts to ensure pods run as non-privileged users.

### Hands-on: Security Context
Update your pod spec to forbid root:
```yaml
spec:
  securityContext:
    runAsNonRoot: true
    runAsUser: 1000
  containers:
  - name: secure-container
    image: nginx
    securityContext:
      allowPrivilegeEscalation: false
```

---
### 🤖 Agent Checkpoint
**Once you've tested the RBAC permissions and written a Network Policy, tell the agent:**
*"I've set up my security basics. Can you explain the difference between a Role and a ClusterRole, and why it's dangerous to use the 'cluster-admin' role for application service accounts?"*
