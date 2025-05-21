* 🚀 CI/CD Pipeline Demo with GitHub Actions, Docker, GitOps, and Argo CD

This project demonstrates a  real-time CI/CD pipeline that automates the entire flow from code push to deployment in Kubernetes using GitHub Actions, Docker, Argo CD, and GitOps principles.



* 📁 Project Structure
ci-cd-pipeline-demo/
├── README.md # Project overview and architecture explanation
├── .github/
│ └── workflows/
│ └── ci-cd-pipeline.yaml # GitHub Actions CI/CD workflow
├── docker/
│ └── Dockerfile # Dockerfile to build application image
├── gitops-repo/
│ └── deployment.yaml # Kubernetes manifest updated by the pipeline
└── architecture/
└── ci-cd-architecture.png # Visual architecture of the pipeline



* 📌 Features

- CI/CD pipeline built using GitHub Actions
- Automated **Docker build** and push to Docker Hub
- GitOps-based deployment using Argo CD
- Declarative Kubernetes manifests
- Real-time sync of changes via GitHub and Argo CD

* ⚙️ How It Works

1.   Developer pushes code  to the `main` branch.
2.   GitHub Actions  triggers the pipeline:
   - Builds Docker image.
   - Pushes image to Docker Hub.
   - Clones GitOps repo and updates the `deployment.yaml` with the new image tag.
   - Commits and pushes changes to GitOps repo.
3.   Argo CD  automatically detects changes in GitOps repo.
4.   Kubernetes pulls the new image and deploys the updated app.

---

* 📌 CI/CD Architecture Diagram

![CI/CD Pipeline Architecture](architecture/ci-cd-architecture.png)



* 🧱 Technologies Used

| Tool          | Purpose                            |
|---------------|-------------------------------------|
|  GitHub Actions | CI/CD automation               |
|  Docker         | Containerization of the app   |
|   Docker Hub       | Image Registry                |
|   Argo CD          | GitOps Continuous Delivery    |
|   Kubernetes       | Container Orchestration       |
|   Git              | Version Control               |

---

 * 🔐 Secrets Required in GitHub

Make sure to add the following secrets to your GitHub repository:

- `DOCKER_USERNAME` – Your Docker Hub username
- `DOCKER_PASSWORD` – Your Docker Hub password or access token
- `GITOPS_REPO_TOKEN` – GitHub token to push changes to your GitOps repo



* 🚀 Deployment Manifest (`gitops-repo/deployment.yaml`)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
  namespace: default
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app
          image: yourdockerhub/my-app:<image-tag>
          ports:
            - containerPort: 3000 ```


