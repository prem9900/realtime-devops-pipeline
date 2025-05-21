 # 🚀 CI/CD Pipeline Demo with GitHub Actions, Docker, GitOps, and Argo CD

This project demonstrates a  real-time CI/CD pipeline  that automates the entire flow from code push to deployment in Kubernetes using  GitHub Actions,Docker, Argo CD , and GitOps principles.



# 📌 Features

* CI/CD pipeline powered by  GitHub Actions
* Automated  Docker image build  and  push to Docker Hub
* GitOps-based deployment using  Argo CD
* Declarative Kubernetes manifests
* Real-time sync of changes between GitHub and Kubernetes via Argo CD



# ⚙️ How It Works

1. Developer pushes code to the `main` branch.
2. GitHub Actions triggers the pipeline:

   * Builds the Docker image.
   * Pushes the image to  Docker Hub.
   * Clones the GitOps repo and updates the `deployment.yaml` with the new image tag.
   * Commits and pushes changes to the GitOps repo.
3.  Argo CD detects changes in the GitOps repo automatically.
4.  Kubernetes pulls the new image and deploys the updated application.



# 📌 CI/CD Architecture Diagram

![CI/CD Pipeline Architecture](architecture/clean%20architecture%20diagram.png)



# 🧱 Technologies Used

| Tool           | Purpose                          |
| -------------- | -------------------------------- |
| GitHub Actions | CI/CD Automation                 |
| Docker         | App Containerization             |
| Docker Hub     | Docker Image Registry            |
| Argo CD        | GitOps-based Continuous Delivery |
| Kubernetes     | Container Orchestration          |
| Git            | Version Control                  |



# 🔐 Secrets Required in GitHub

Add the following  repository secrets in GitHub:

* `DOCKER_USERNAME` – Your Docker Hub username
* `DOCKER_PASSWORD` – Your Docker Hub password or access token
* `GITOPS_REPO_TOKEN` – GitHub token with access to your GitOps repo



# 🚀 Deployment Manifest  (`gitops-repo/deployment.yaml`)

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
            - containerPort: 3000
```



# 🐳 Sample Dockerfile (`docker/Dockerfile`)

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```



# 📦 GitHub Actions Workflow (`.github/workflows/frist-actions.yaml`)

This GitHub Actions workflow performs the following:

* Builds a Docker image tagged with the latest commit SHA.
* Pushes the image to Docker Hub.
* Clones and updates the GitOps repo with the new image tag.
* Argo CD automatically syncs and redeploys the new version in Kubernetes.


