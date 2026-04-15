# Module 03: Networking

In the previous modules, we launched Pods. But Pods are ephemeral; their IP addresses change every time they are restarted. If you have a frontend Pod that needs to talk to a backend Pod, you can't rely on the IP.

This is where **Services** and **Ingress** come in.

## 🌐 Kubernetes Services

A Service is an abstraction that defines a logical set of Pods and a policy by which to access them. It provides a **stable IP address and DNS name**.

### Service Types
1. **ClusterIP (Default)**: Exposes the service on an internal IP in the cluster. Only reachable from within the cluster.
2. **NodePort**: Exposes the service on each Node's IP at a static port. This allows external traffic to reach your service.
3. **LoadBalancer**: Exposes the service externally using a cloud provider's load balancer. (In Kind, this is often handled by tools like MetalLB or simply doesn't work as expected without extra setup).

### Hands-on: Creating a Service
1. Create a `deployment.yaml` (we'll see Deployments in the next module, but for now, let's just use a Pod):
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: backend-pod
  labels:
    app: backend
spec:
  containers:
  - name: redis
    image: redis:latest
```

2. Create a `service.yaml` to expose the redis pod:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: backend-service
spec:
  selector:
    app: backend
  ports:
    - protocol: TCP
      port: 6379
      targetPort: 6379
  type: ClusterIP
```

3. Apply and test DNS:
```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
# Run a temporary pod to test the DNS resolution
kubectl run curl-test --image=curlimages/curl -i --tty --rm -- \
  curl http://backend-service:6379
```
*(Note: Redis doesn't speak HTTP, so curl will return a response or an error, but the fact that it tries to connect proves DNS is working).*

## 🚪 Ingress: The Gateway

While Services handle internal routing, **Ingress** manages external access to the services, typically HTTP/HTTPS. It acts as a smart router (like Nginx or HAProxy) that can route traffic based on hostnames or paths.

### Hands-on: Setting up Ingress in Kind
Kind has a specific way of handling Ingress. 

1. To use Ingress in Kind, you typically need to create the cluster with specific port mappings. (If you didn't, the Ingress controller might not be reachable from your host machine).
2. Here is a basic Ingress resource:
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: main-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /test
        pathType: Prefix
        backend:
          service:
            name: backend-service
            port:
              number: 6379
```

---
### 🤖 Agent Checkpoint
**Once you have successfully created a service and tested it via another pod, tell the agent:**
*"I've set up my first Service. Can you explain the difference between a ClusterIP and a NodePort, and when I would use one over the other?"*
