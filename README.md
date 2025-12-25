# DevSecOps Pipeline Implementation for Tic Tac Toe Game

![Screenshot 2025-03-04 at 7 16 48 PM](https://github.com/user-attachments/assets/7ed79f9c-9144-4870-accd-500085a15592)

![image](https://github.com/user-attachments/assets/5b2813a5-f493-4665-8964-77359b5be93a)

```markdown
# 🕹️ DevSecOps Tic-Tac-Toe Application

Complete end-to-end pipeline implementation for a TypeScript/React Tic-Tac-Toe game with security scanning, GitHub Actions CI/CD, Docker multi-stage builds, and Kubernetes GitOps deployment using ArgoCD.

## 🎯 Project Features
- Two-player Tic-Tac-Toe with real-time scoreboard tracking
- Responsive React UI with Tailwind CSS styling
- Production-ready static assets generated via Vite build
- Multi-stage Docker optimization (Node → Nginx)
- Full DevSecOps pipeline with automated security checks

## 🛠️ Tech Stack
| Component | Technologies |
|-----------|--------------|
| Frontend | TypeScript, React, Vite, Tailwind CSS, React Icons |
| Build Tools | npm, Node.js 20+ |
| Containerization | Docker Multi-stage Builds |
| Security Scanning | Trivy (SCA), npm lint (SAST) |
| CI/CD | GitHub Actions (cicd.yaml) |
| Deployment | Kubernetes + ArgoCD + GHCR |
| Infrastructure | GitHub Container Registry |

## 🏗️ Project Structure
```
.
├── src/                    # TypeScript React source (.tsx)
│   ├── Square.tsx          # Game square component
│   ├── Scoreboard.tsx      # Score tracking UI
│   └── App.tsx             # Main game logic
├── tests/                  # Jest unit tests
├── kubernetes/             # K8s manifests
│   └── deployment.yaml     # Auto-updated image tags
├── Dockerfile              # Multi-stage Node→Nginx
├── cicd.yaml               # Complete DevSecOps pipeline
├── package.json            # npm scripts & dependencies
└── README.md
```

## 🔄 Complete DevSecOps Pipeline
Triggers on `push/PR` to `main` (excludes `kubernetes/` changes to prevent loops):

```
Push/PR → Unit Tests → SAST → Build → Docker Build → Trivy Scan → GHCR Push → Update K8s → ArgoCD Deploy
```

**Pipeline Jobs Breakdown:**
1. **Unit Testing** – `npm test` validates game logic
2. **Static Analysis** – `npm run lint` catches code issues
3. **Build** – `npm run build` → `/dist` artifacts uploaded
4. **Docker** – Multi-stage build → Trivy scan → Push `ghcr.io/abhishekveeramalla/devsecops-tictactoe:<sha>`
5. **K8s Update** – Shell script commits new image tag to `deployment.yaml`
6. **GitOps CD** – ArgoCD auto-deploys to Kubernetes

## 🚀 Quick Start Guide

### Prerequisites
```
# Install Node.js 20+
node --version  # v20.x.x
npm --version   # 10.x.x
docker --version
```

### Local Development
```
git clone https://github.com/abhishekveeramalla/devsecops-tictactoe.git
cd devsecops-tictactoe
npm install
npm run dev           # http://localhost:5137
npm run build         # Creates /dist folder
npm test              # Run unit tests
npm run lint          # Static analysis
```

### Docker Local Testing
```
docker build -t tictactoe:local .
docker run -p 9099:80 tictactoe:local
# Access: http://localhost:9099
```

## 🔐 GitHub Secrets Setup
1. **Create PAT Token**: `Settings → Developer settings → Personal access tokens → Generate new token (classic)`
2. **Scopes**: `write:packages`, `read:packages`
3. **Add Secret**: `Settings → Secrets and variables → Actions → New repository secret`
   ```
   Name: TOKEN
   Value: <your-pat-token>
   ```

## 🐳 Multi-Stage Dockerfile Breakdown
```
# Build Stage (Node 20)
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Production Stage (Nginx)
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```
**Benefits**: ~90% smaller image size, faster builds via layer caching

## 📊 Pipeline Verification
- **Actions Tab**: Monitor all job runs and logs
- **Artifacts**: Download `/dist` from Build job
- **Container Images**: `ghcr.io/abhishekveeramalla/devsecops-tictactoe:<commit-sha>`
- **Deployed App**: `<k8s-node-ip>:80` (ArgoCD managed)

## 🎥 Learning Resources
- **Tutorial Inspiration**: [DevSecOps CI/CD Pipeline - Abhishek Veeramala](https://youtu.be/Ke_Wr5zPE0A)
- **Original Demo**: [iam-veeramalla/devsecops-demo](https://github.com/iam-veeramalla/devsecops-demo)

## 👨‍💻 Author 
**Abdur S**  

Huge shoutout to Abhishek Veeramalla Bro for the world-class tutorial




**Just copy everything above the line and paste directly into your GitHub repository's README.md file! 🚀**
