# DevOps Notes & Learning Journal

> A structured knowledge base documenting my DevOps learning journey — covering containers, CI/CD, cloud infrastructure, and automation.
> Built from hands-on labs across KodeKloud, Andela's Kubernetes Training Programme, and AWS/Azure certifications.

---

## Learning Stack

| Area | Tools & Technologies |
|---|---|
| Containers | Docker, Kubernetes |
| Cloud | AWS, Microsoft Azure, Aviatrix Multicloud |
| CI/CD | GitHub Actions, CI/CD pipeline concepts |
| Scripting | Bash, Python (developing) |
| Version Control | Git, GitHub |
| Monitoring | AWS CloudWatch |
| OS | Linux (Ubuntu), Windows |

---

## Docker — Container Basics

Containers solve the classic "it works on my machine" problem by packaging an application with everything it needs to run.

### Core concepts

| Concept | Description |
|---|---|
| Image | A blueprint for a container — read only |
| Container | A running instance of an image |
| Dockerfile | Instructions to build a custom image |
| Docker Hub | Public registry for sharing images |

### Commands practised

```bash
docker pull nginx                        # pull an image from Docker Hub
docker run -d -p 80:80 nginx             # run a container in the background
docker ps                                # list running containers
docker ps -a                             # list all containers including stopped
docker stop <container_id>              # stop a running container
docker rm <container_id>                # remove a container
docker images                            # list all local images
docker rmi <image_id>                   # remove an image
docker logs <container_id>              # view container logs
docker exec -it <container_id> bash     # open a shell inside a container
```

### Sample Dockerfile

```dockerfile
FROM ubuntu:22.04
RUN apt-get update && apt-get install -y nginx
COPY index.html /var/www/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

**Key insight:** Every `RUN`, `COPY`, and `ADD` instruction creates a new image layer. Keeping layers small and combining commands reduces image size.

---

## Kubernetes — Container Orchestration

Kubernetes (K8s) manages containers at scale — handling deployment, scaling, and self-healing automatically.

### Core objects

| Object | Purpose |
|---|---|
| Pod | Smallest deployable unit — one or more containers |
| Deployment | Manages replicas and rolling updates of Pods |
| Service | Exposes Pods to network traffic (internal or external) |
| Namespace | Logical isolation between environments (dev, staging, prod) |
| ConfigMap | Store non-sensitive config data |
| Secret | Store sensitive data like passwords and API keys |

### Commands practised

```bash
kubectl get pods                          # list all pods
kubectl get pods -n kube-system           # list pods in a specific namespace
kubectl describe pod <pod-name>           # detailed info about a pod
kubectl apply -f deployment.yaml          # apply a configuration file
kubectl delete pod <pod-name>             # delete a pod
kubectl logs <pod-name>                   # view pod logs
kubectl exec -it <pod-name> -- bash       # open shell inside a pod
kubectl get services                      # list services
kubectl scale deployment myapp --replicas=3  # scale a deployment
```

### Sample Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  namespace: default
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: nginx:latest
        ports:
        - containerPort: 80
```

**Key insight:** Kubernetes does not just run containers — it watches them. If a pod crashes, K8s automatically restarts it. If traffic spikes, you scale with one command.

---

## CI/CD — Continuous Integration & Delivery

CI/CD automates the journey from code commit to deployed application.

### The pipeline concept

```
Developer pushes code
        ↓
CI runs automated tests
        ↓
Build creates an artifact (Docker image, binary, etc.)
        ↓
CD deploys to staging environment
        ↓
Approval (manual or automatic)
        ↓
CD deploys to production
```

### GitHub Actions — basic workflow structure

```yaml
name: Deploy Pipeline

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Build Docker image
        run: docker build -t myapp:latest .

      - name: Run tests
        run: docker run myapp:latest npm test
```

**Key insight:** CI/CD removes human error from deployments. The same process runs every time — no forgotten steps, no "I thought you deployed that" moments.

---

## AWS CloudWatch — Infrastructure Monitoring

Monitoring is not optional in production. If you are not watching your systems, you are flying blind.

### What I practised

- Created **log groups** to centralise application and system logs
- Set up **custom metrics** to track CPU, memory, and disk usage
- Configured **alarms** to trigger alerts when thresholds were breached
- Used **dashboards** to visualise infrastructure health at a glance

### Key CloudWatch concepts

| Feature | Purpose |
|---|---|
| Log Groups | Collect and store logs from EC2, Lambda, containers |
| Metrics | Numerical data points over time (CPU %, request count) |
| Alarms | Trigger notifications or actions when a metric crosses a threshold |
| Dashboards | Visual overview of multiple metrics in one place |
| Insights | Query language for analysing log data |

**Key insight:** Monitoring closes the feedback loop. You cannot improve what you cannot measure — and you cannot fix what you do not know is broken.

---

## Git & Version Control — Workflow

```bash
git init                          # initialise a new repo
git clone <url>                   # clone a remote repo
git status                        # check what has changed
git add .                         # stage all changes
git commit -m "descriptive msg"  # commit with a message
git push origin main              # push to remote
git pull origin main              # pull latest changes
git branch feature-branch         # create a new branch
git checkout feature-branch       # switch to a branch
git merge feature-branch          # merge into current branch
git log --oneline                 # view commit history
```

**Branching strategy practised:**
- `main` — stable, production-ready code only
- `dev` — active development branch
- `feature/` — one branch per feature or fix

---

## Progress Tracker

| Topic | Status |
|---|---|
| Docker fundamentals | ✅ Done |
| Kubernetes core objects and kubectl | ✅ Done |
| CI/CD pipeline concepts | ✅ Done |
| GitHub Actions basics | ✅ Done |
| AWS CloudWatch monitoring | ✅ Done |
| Git branching workflows | ✅ Done |
| Bash scripting for automation | 🔄 In Progress |
| Infrastructure as Code (Terraform basics) | 🔄 In Progress |
| Advanced Kubernetes (Helm, Ingress) | 🔄 In Progress |

---

## Certifications Supporting This Work

- AWS Certified Cloud Practitioner — 2025
- AWS Solutions Architect Associate Training — ALX Africa (2025)
- ACE Multicloud Network Associate — Aviatrix (In Progress)
- Microsoft Azure Fundamentals — AZ-900
- Kubernetes African Developer Training — Andela (In Progress)
- 100-Day Cloud Engineering Challenge — KodeKloud (In Progress)

---

*Part of my broader DevOps and Cloud Engineering learning journey.*
*Connect on [LinkedIn](https://www.linkedin.com/in/ifeanyi-pascal-okonkwo-6b22b1128)*
