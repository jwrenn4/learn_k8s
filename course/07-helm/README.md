# Module 07: Helm

As your application grows, managing 20 different YAML files for a single application becomes a nightmare. **Helm** is the "package manager" for Kubernetes.

Helm allows you to define a "Chart" (a template), and then provide a "values.yaml" file to customize it without changing the templates.

## 📦 What is a Helm Chart?

A Chart is a collection of templates that define an application, its Service, Ingress, and Deployment.

### Structure:
- `Chart.yaml`: Metadata about the chart.
- `values.yaml`: Default configuration values.
- `templates/`: The actual YAML templates.

## 🛠️ Getting Started with Helm

### 1. Installation
Depending on your OS:
- **macOS**: `brew install helm`
- **Windows**: `choco install helm`
- **Linux**: `curl https://raw.githubusercontent.com/helm/helm/main/scripts/install-helm-sh.tar.gz | tar xz`

### 2. Using a Public Chart
Let's install a standard Prometheus monitoring stack using Helm.

1. Add the Prometheus community repository:
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

2. Install the chart:
```bash
helm install my-prometheus prometheus-community/prometheus
```

3. Verify the installation:
```bash
kubectl get pods
```

## 🏗️ Creating Your Own Chart

1. Create a new chart:
```bash
helm create my-app-chart
```

2. Look at the `templates/` folder. You'll notice that `{{ .Values.image.repository }}` instead of hardcoded values.

3. Customize the deployment in `values.yaml`:
```yaml
image:
  repository: nginx
  tag: latest
  pullPolicy: IfNotAlwaysPull
  replicaCount: 3
```

4. Install your customized chart:
```bash
```bash
helm install my-release ./my-app-chart
```

5. Upgrade your app:
```bash
# Change replicaCount in values.yaml, then:
helm upgrade my-release ./my-app-chart
```

---
### 🤖 Agent Checkpoint
**Once you've installed a public chart and created a basic custom chart, tell the agent:**
*"I've started using Helm. Can you explain the concept of 'templated' YAML files, and how Helm makes it easier to manage different environments (like development, staging, and production)?"*
