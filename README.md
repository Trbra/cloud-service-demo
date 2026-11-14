# Cloud Service Demo

## Purpose

This project is a small example of a web page that could be deployed as a cloud-hosted service. It demonstrates a simple homepage and the value of container orchestration in cloud environments.

## Files

- `README.md` — describes the project and its files.
- `index.html` — the demo homepage.
- `Dockerfile` — packages the web page into an Nginx container image.
- `kubernetes/deployment.yaml` — creates the Kubernetes Deployment.
- `kubernetes/service.yaml` — exposes the Deployment through a NodePort Service.

Version control helps a cloud project by recording changes, making it easier to collaborate, review updates, and restore an earlier version when needed.

## Running with Docker

Docker is a platform for packaging and running applications in isolated environments. A Docker image is a packaged template containing an application and what it needs to run. A Docker container is a running instance of an image.

Build the image from this project, then start a container and access the homepage at `http://localhost:8080`:

```sh
docker build -t cloud-service-demo:1.0 .
docker run -d --name cloud-demo-container -p 8080:80 cloud-service-demo:1.0
```

## Kubernetes Overview

Kubernetes is a container orchestration platform used to deploy, scale, and manage applications across containers. It helps keep the required number of application instances running, handles restarts, and provides stable service access. In cloud and DevOps workflows, Kubernetes is used to automate deployment, scaling, and recovery.

### Kubernetes objects

- `Pod`: The smallest deployable unit in Kubernetes. It runs one or more containers and represents a single application instance.
- `Deployment`: Manages a set of Pods and ensures the desired number of replicas are running.
- `Service`: Provides a stable network endpoint for selecting and accessing a group of Pods.

### Minikube and Docker image setup

```sh
minikube start --driver=docker
minikube image load cloud-service-demo:1.0
```

### Apply the Kubernetes configuration

```sh
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml
```

### Access the application

```sh
kubectl port-forward service/cloud-service-demo 8080:80
```

Then open `http://localhost:8080` in a browser to view the Cloud Service Demo page.

### Scaling the Deployment

```sh
kubectl scale deployment cloud-service-demo --replicas=2
kubectl get deployments
kubectl get pods
kubectl get endpoints cloud-service-demo
```

This demonstrates how Kubernetes can manage multiple copies of the same application and distribute traffic through the Service.