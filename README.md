# Kubernetes Projects

## Meghana Avadhanam

### Overview

In this repo, I'm publishing 3 separate, local-level projects using Kubernetes.

**Project 1**
- Deploying a "Deployment" on Kubernetes for an Nginx app and performing a rolling update on it to test the feature.

**Project 2**
- Deploying a FASTAPI app written in Python to a Pod, building its image on Docker, forwarding its port to 8080:80, and deploying a Kubernetes Pod into a local cluster on minikube.

**Project 3**
- Deploying a To-do list app using FastAPI and HTML, containerized it with a Docker Image and forwarded its port from 8000 to 80, deploying a pod onto minikube.


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

------------------------------------------------------------

**Project 2**
- Deploying a FASTAPI app written in Python to a Pod, building its image on Docker, forwarding its port to 8080:80, and deploying a Kubernetes Pod into a local cluster on minikube.

### Steps:

1. Create Python virtual environment:
   ```bash
   python3 -m venv ./venv
   ```

2. Activate virtual environment
   ```bash
   source ./venv/bin/activate
   ```
4. Install fastapi
   ```bash
   pip install fastapi
   ```
5. Install uvicorn
   ```bash
   pip install uvicorn
   ```
6. pip freeze and add the packages to requirements.txt
7. Create main.py file
8. Run the app using uvicorn
   ```bash
   uvicorn main:app --reload
   ```
9. Create dockerfile
10. Build docker file
   ```bash
   docker build -t k8s-fast-api .
   ```
11. Run the container locally to check and port-forward 8000:80
```bash
docker run -p 8000:80 k8s-fast-api
```

12. Create a new repo in dockerhub registry so kubernetes can access it
13. Push image to dockerhub registry
    ```bash
    docker push megavadh/k8s-getting-started:tagname
    ```

14. Launch cluster on CIVO/Minikube
    ```bash
    minikube start
    ```

15. Check status
    ```bash
    minikube status
    ```

16. Create a kubernetes manifest deployment.yaml file

17. Create a service.yaml file to maintain a port for incoming and outgoing traffic.

18. Run the deployment and service 
    ```bash
    kubectl apply -f .
    ```
20. Get pods
    ```bash
    kubectl get pods -w
    ```

21. Port forwarding in Kubernetes allows you to access internal cluster resources from outside the cluster.
     ```bash
    kubectl port-forward pod-name 8080:80 
    ```
The app is now on kubernetes cluster! (P.s. to expose it to external traffic from public internet, use kubernetes ingress by setting up a DNS and input into yaml ingress file.


------------------------------------------------------------

