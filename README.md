# Kubernetes Deployment Project

## Meghana Avadhanam

### Overview

In this mini project, the aim is to deploy an nginx deployment and pod on Kubernetes, using Kubernetes manifest on Minikube. Nginx is a lightweight open-source web server that is widely used for sample pods, deployments, and ingresses. It serves as a reverse proxy and load balancer, making it very useful for Kubernetes applications.

### Prerequisites

- Minikube
- Docker
- kubectl

### Steps

1. Start Minikube:
   ```bash
   minikube start
   ```

2. Check pods:
   ```bash
   kubectl get pods
   ```

   No pods present in the cluster initially.

Notes: A deployment is an object that manages a set of identical pods.

Creating a deployment with a 'Kubernetes Manifest' yaml file.

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
        image: nginx:latest
        ports:
        - containerPort: 80
```

Apply the manifest using kubectl:
```bash
kubectl apply -f nginx.yaml
```

After deployment is created, check the following (optional):
```bash
kubectl get deployments
kubectl describe deployment nginx-deployment
```

Scale the Deployment up or down:
```bash
kubectl scale deployment <deployment-name> --replicas=<replica-count>
```

### Task 2 - Performing a Rolling Update on nginx deployment

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
        image: nginx:1.19.6   # Updated image version
        ports:
        - containerPort: 80
```

Notes: A Pod is the smallest deployable unit in Kubernetes, consisting of one or more containers that share networking and storage resources.

Run the pod:

- `kubectl get pods`: View all Pods in the cluster.
- `kubectl describe pod <pod-name>`: Get detailed information about a specific Pod.
- `kubectl logs <pod-name>`: View logs from a Pod's containers.
- `kubectl exec -it <pod-name> -- <command>`: Execute a command inside a running Pod.
