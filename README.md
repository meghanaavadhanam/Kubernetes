# Kubernetes Projects

## Meghana Avadhanam

### Overview

In this repo, I'm publishing 3 separate, local-level projects using Kubernetes.

Project 1 - Deploying a "Deployment" on Kubernetes for an Nginx app and performing a rolling update on it to test the feature.

Project 2 - Deploying a FASTAPI app written in Python to a Pod, building its image on Docker, forwarding its port to 8080:80 and deploying a Kubernetes Pod into a local cluster on minikube.

Project 3 - Deploying a To-do list app with a preexisting Docker Image and forwarding its port from 3000 to 80, deploying a pod on to minikube.

#### Project 1 : Nginx - Docker - Kubernetes
I deploy an nginx deployment and pod on Kubernetes, using a yaml manifest file on Minikube. Nginx is a lightweight open-source web server that is widely used for sample pods, deployments, and ingresses. It serves as a reverse proxy and load balancer, making it very useful for Kubernetes applications.

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

3. Creating a deployment with a 'Kubernetes Manifest' yaml file.

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

4. Apply the manifest using kubectl:
```bash
kubectl apply -f nginx.yaml
```

5. After deployment is created, check the following (optional):
```bash
kubectl get deployments
kubectl describe deployment nginx-deployment
```

6. Scale the Deployment up or down:
```bash
kubectl scale deployment <deployment-name> --replicas=<replica-count>
```

7. Perform a Rolling Update on nginx deployment image

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

