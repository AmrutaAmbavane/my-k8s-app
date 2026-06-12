# 🚀 Containerized Web App Deployment on Local Kubernetes

A hands-on project demonstrating how to containerize a Node.js application using **Docker** and deploy it to a local **Kubernetes** cluster using **Minikube** — simulating real-world **Azure Kubernetes Service (AKS)** deployment workflows.

---

## 📌 Project Overview

This project covers the full lifecycle of containerizing and deploying a web application:

- Building a lightweight Node.js REST API
- Packaging it into a Docker container using an Alpine-based image
- Deploying to a local Kubernetes cluster (Minikube)
- Managing pods, replicas, and services via `kubectl`
- Simulating zero-downtime rolling updates

---

## 🛠 Tech Stack

| Tool         | Purpose                                      |
|--------------|----------------------------------------------|
| Node.js      | Application runtime                          |
| Express.js   | Web framework                                |
| Docker       | Containerization                             |
| Minikube     | Local Kubernetes cluster                     |
| kubectl      | Kubernetes CLI for managing resources        |

---

## 📁 Project Structure

```
my-k8s-app/
├── app/
│   ├── index.js          # Express app
│   └── package.json      # Node dependencies
├── Dockerfile            # Container image definition
├── k8s/
│   ├── deployment.yaml   # Kubernetes Deployment manifest
│   └── service.yaml      # Kubernetes Service manifest
└── README.md
```

---

## ⚙️ Prerequisites

Make sure the following tools are installed:

- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Node.js](https://nodejs.org/) (v18+)

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/my-k8s-app.git
cd my-k8s-app
```

### 2. Build the Docker Image

```bash
docker build -t my-k8s-app:v1 .
```

### 3. Test Locally with Docker

```bash
docker run -p 3000:3000 my-k8s-app:v1
```

Visit `http://localhost:3000` — you should see:
```
Hello from Kubernetes! 🚀
```

### 4. Start Minikube and Load the Image

```bash
minikube start
minikube image load my-k8s-app:v1
```

### 5. Deploy to Kubernetes

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

### 6. Verify Deployment

```bash
kubectl get pods
kubectl get deployments
kubectl get services
```

### 7. Open the App in Browser

```bash
minikube service my-k8s-app-service
```

---

## 🔄 Rolling Update (Zero Downtime)

Simulate a production-style rolling update:

```bash
# Rebuild with new version
docker build -t my-k8s-app:v2 .
minikube image load my-k8s-app:v2

# Update the deployment
kubectl set image deployment/my-k8s-app my-k8s-app=my-k8s-app:v2

# Watch the rollout
kubectl rollout status deployment/my-k8s-app
```

---

## 🔍 Useful kubectl Commands

```bash
# View pod logs
kubectl logs <pod-name>

# Describe a pod (useful for debugging)
kubectl describe pod <pod-name>

# Scale replicas up or down
kubectl scale deployment my-k8s-app --replicas=3

# Roll back to previous version
kubectl rollout undo deployment/my-k8s-app

# Delete all resources
kubectl delete -f k8s/
```

---

## ☁️ Azure Kubernetes Service (AKS) Parallel

This project is designed to mirror AKS workflows. Here's how each local component maps to Azure:

| Local (Minikube)         | Azure Equivalent                        |
|--------------------------|-----------------------------------------|
| Minikube cluster         | AKS Cluster                             |
| Docker local image       | Azure Container Registry (ACR)          |
| NodePort Service         | Azure Load Balancer / App Gateway       |
| kubectl RBAC             | AKS + Azure Active Directory RBAC       |
| PersistentVolumeClaim    | Azure Disk / Azure Files                |
| Rolling Update           | AKS Zero-Downtime Deployment            |

---

## 📈 What I Learned

- How to write and optimize a `Dockerfile` using a minimal Alpine base image
- Kubernetes core concepts: Pods, Deployments, ReplicaSets, and Services
- How `kubectl` manifests translate directly to AKS deployments
- Rolling update strategies for zero-downtime releases
- How local Kubernetes clusters simulate real cloud infrastructure

---

## 📚 References

- [Kubernetes Official Docs](https://kubernetes.io/docs/)
- [Minikube Getting Started](https://minikube.sigs.k8s.io/docs/start/)
- [Docker Getting Started](https://docs.docker.com/get-started/)
- [Azure Kubernetes Service Docs](https://learn.microsoft.com/en-us/azure/aks/)
- [Microsoft Learn — AKS](https://learn.microsoft.com/en-us/training/paths/intro-to-kubernetes-on-azure/)

---

## 🙋 Author

**Your Name**
- GitHub: [@your-username](https://github.com/your-username)
- LinkedIn: [your-linkedin](https://linkedin.com/in/your-linkedin)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
