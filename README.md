
---

```markdown
# DevSecOps Pipeline Implementation for Tic Tac Toe Game

![UI Screenshot](https://github.com/user-attachments/assets/7ed79f9c-9144-4870-accd-500085a15592)
![Pipeline Screenshot](https://github.com/user-attachments/assets/5b2813a5-f493-4665-8964-77359b5be93a)

---

# 🕹️ DevSecOps Tic-Tac-Toe Application

A complete **end-to-end DevSecOps pipeline implementation** for a **TypeScript + React Tic-Tac-Toe game**, featuring automated security scanning, GitHub Actions CI/CD, optimized Docker multi-stage builds, and **GitOps-based Kubernetes deployment using ArgoCD**.

This project demonstrates how modern DevSecOps practices can be applied to a real-world frontend application—from code commit to secure production deployment.

---

## 🎯 Project Features

- 🎮 Two-player Tic-Tac-Toe game
- 📊 Real-time scoreboard tracking
- 📱 Fully responsive UI using Tailwind CSS
- ⚡ Production-ready static assets generated via Vite
- 🐳 Optimized multi-stage Docker builds (Node → Nginx)
- 🔐 Integrated security scanning throughout the CI/CD pipeline
- 🚀 GitOps-based continuous delivery with ArgoCD

---

## 🛠️ Tech Stack

| Component | Technologies |
|---------|-------------|
| Frontend | TypeScript, React, Vite, Tailwind CSS |
| Build Tools | npm, Node.js 20+ |
| Containerization | Docker (Multi-stage builds) |
| Security | Trivy (SCA), ESLint (SAST) |
| CI/CD | GitHub Actions |
| Deployment | Kubernetes, ArgoCD |
| Registry | GitHub Container Registry (GHCR) |

---

## 🏗️ Project Structure

```

.
├── src/                    # React TypeScript source files
│   ├── Square.tsx          # Game square component
│   ├── Scoreboard.tsx      # Score tracking UI
│   └── App.tsx             # Main game logic
├── tests/                  # Jest unit tests
├── kubernetes/             # Kubernetes manifests
│   └── deployment.yaml     # Auto-updated image tags
├── Dockerfile              # Multi-stage Node → Nginx build
├── cicd.yaml               # GitHub Actions DevSecOps pipeline
├── package.json            # npm scripts & dependencies
└── README.md

```

---

## 🔄 Complete DevSecOps Pipeline

Pipeline triggers on **push / pull request to `main`**  
(`kubernetes/` directory is excluded to prevent GitOps loops)

```

Push / PR
↓
Unit Tests
↓
SAST (Lint)
↓
Build
↓
Docker Build
↓
Trivy Image Scan
↓
Push to GHCR
↓
Update K8s Manifest
↓
ArgoCD Sync & Deploy

````

---

## 🔍 Pipeline Job Breakdown

1. **Unit Testing**
   - Runs `npm test`
   - Validates game logic and components

2. **Static Application Security Testing (SAST)**
   - `npm run lint`
   - Identifies code quality and security issues

3. **Build**
   - `npm run build`
   - Generates production-ready `/dist` artifacts

4. **Docker & Image Scanning**
   - Multi-stage Docker build
   - Trivy scans for vulnerabilities
   - Pushes image to:
     ```
     ghcr.io/abdur-s/devsecops-tictactoe:<commit-sha>
     ```

5. **Kubernetes Manifest Update**
   - Shell script updates `deployment.yaml`
   - Commits new image tag automatically

6. **GitOps Continuous Deployment**
   - ArgoCD detects manifest change
   - Syncs and deploys to Kubernetes cluster

---

## 🚀 Quick Start Guide

### ✅ Prerequisites

```bash
node --version    # v20.x.x
npm --version     # v10.x.x
docker --version
````

---

### 💻 Local Development

```bash
cd devsecops-tictactoe

npm install
npm run dev        # http://localhost:5137
npm run build      # Generates /dist
npm test           # Run unit tests
npm run lint       # Static analysis
```

---

### 🐳 Docker Local Testing

```bash
docker build -t tictactoe:local .
docker run -p 9099:80 tictactoe:local
```

Access the application at:
👉 [http://localhost:9099](http://localhost:9099)

---

## 🔐 GitHub Secrets Configuration

### Step 1: Create a Personal Access Token (PAT)

* GitHub → Settings
* Developer settings → Personal access tokens (classic)
* Required scopes:

  * `write:packages`
  * `read:packages`

### Step 2: Add Repository Secret

```text
Name: TOKEN
Value: <your-pat-token>
```

---

## 🐳 Multi-Stage Dockerfile

```dockerfile
# Build Stage
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Production Stage
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### ✅ Benefits

* ~90% smaller image size
* Faster CI builds
* Reduced attack surface
* Production-grade static hosting

---

## 📊 Pipeline Verification

* ✅ GitHub Actions pipeline passing
* 📦 Build artifacts (`/dist`) generated
* 🐳 Images stored in GHCR with commit SHA tags
* 🚀 Kubernetes deployment managed by ArgoCD

---

## 🎥 Learning Resources

* Reference Repository:
  [https://github.com/iam-veeramalla/devsecops-demo](https://github.com/iam-veeramalla/devsecops-demo)

---

## 👨‍💻 Author

**Abdur S**

🙏 Inspired by the DevSecOps CI/CD tutorial by **Abhishek Veeramala**

```

---


If you want **badges, diagrams, or resume bullets**, just say 👍
```
