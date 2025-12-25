```
---

```markdown
# DevSecOps Pipeline Implementation for Tic Tac Toe Game

![UI Screenshot](https://github.com/user-attachments/assets/7ed79f9c-9144-4870-accd-500085a15592)
![Pipeline Screenshot](https://github.com/user-attachments/assets/5b2813a5-f493-4665-8964-77359b5be93a)

---

# 🕹️ DevSecOps Tic-Tac-Toe Application

A complete **end-to-end DevSecOps pipeline implementation** for a **TypeScript + React Tic-Tac-Toe game**, featuring automated security scanning, GitHub Actions CI/CD, optimized Docker multi-stage builds, and **GitOps-based Kubernetes deployment using ArgoCD**.

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
| Containerization | Docker (Multi-stage) |
| Security | Trivy (SCA), ESLint (SAST) |
| CI/CD | GitHub Actions |
| Deployment | Kubernetes, ArgoCD |
| Registry | GitHub Container Registry |

---

## 🏗️ Project Structure

```
.
├── src/
│   ├── Square.tsx
│   ├── Scoreboard.tsx
│   └── App.tsx
├── tests/
├── kubernetes/
│   └── deployment.yaml
├── Dockerfile
├── cicd.yaml
├── package.json
└── README.md
```

---

## 🔄 Complete DevSecOps Pipeline

Pipeline triggers on **push / pull request to `main`**  
(`kubernetes/` excluded to avoid GitOps loops)

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
Trivy Scan
↓
Push to GHCR
↓
Update K8s Manifest
↓
ArgoCD Sync & Deploy
```

---

## 🚀 Quick Start

### Local Development

```bash
npm install
npm run dev
npm test
npm run lint
```

---

## 🐳 Docker

```bash
docker build -t tictactoe:local .
docker run -p 9099:80 tictactoe:local
```

👉 http://localhost:9099

---

## 🔐 GitHub Secrets

```
Name: TOKEN
Value: <PAT with write:packages>
```

---

## 👨‍💻 Author

**Abdur S**

🙏 Inspired from **Abhishek Veeramala**
```

---

