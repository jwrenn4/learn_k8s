# Module 09: Final Project

Congratulations! You have traveled from installing a single Pod to managing a complex, scaled, and observable application stack.

## 🎯 The Goal

Build a **Three-Tier Application** (Frontend, Backend, Database) and deploy it to your Kind cluster using the concepts learned in all previous modules.

### Application Architecture:
1. **Frontend**: A simple web server (Nginx) that serves a static page.
2. **Backend**: A simple API (Node.js or Python) that connects to the Database.
3. **Database**: A persistent storage database (MongoDB or PostgreSQL).

## 🛠️ Requirements

Your project must implement the following:

1. **Separation of Config**: Use a `ConfigMap` or `Secret` for the database connection string.
2. **Persistent Storage**: Database must use a `PersistentVolumeClaim`.
3. **Networking**: 
    - The Frontend must connect to the Backend via a `Service` (ClusterIP).
    - The Backend must connect to the Database via a `Service` (ClusterIP).
4. **Workloads**:
    - Use a `Deployment` for the Frontend and Backend.
    - Use a `StatefulSet` for the Database.
5. **Scaling**:
    - Set `requests` and `requests` for all pods.
    - Configure an `HPA` for the Frontend deployment.
6. **Security**:
    - Use a `NetworkPolicy` to ensure that only the Backend can talk to the Database.
7. **Deployment**:
    - Package the entire application using a **Helm Chart**.

## 🏁 Final Checklist

- [ ] Application is fully functional.
- [ ] Database data persists after pod restart.
- [ ] Frontend is reachable via `kubectl port-forward` or Ingress.
- [ ] Database is isolated from the Frontend (Network Policy).
- [ ] Resource limits are które are correctly set.

---
### 🤖 Agent Checkpoint
**Once you've completed the project and you're ready for a final review, tell the agent:**
*"I've finished the Final Project. Can you review my Helm chart and YAML files to see if I've applied all the best practices we've covered?"*
