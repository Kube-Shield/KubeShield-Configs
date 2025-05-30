# KubeShield-Configs
Thanks for sharing the folder structure and architecture screenshot. Based on the directory layout and your crAPI deployment, here’s an improved and customized `README.md` to reflect the multi-service Kubernetes setup you've used:

---

```markdown
# 🛡️ crAPI Kubernetes Deployment (KubeShield Configs)

This repository provides Kubernetes manifests and shell scripts for deploying OWASP's **crAPI (Completely Ridiculous API)** application. It simulates a microservice-based vulnerable API environment for practicing API security testing and exploitation.

---

## 📁 Repository Structure

Each service is configured in its own folder for modular deployment.
├── community/ # Community service configs
│ ├── config.yaml
│ ├── deployment.yaml
│ └── service.yaml
├── gateway-service/ # API Gateway configs
│ ├── config.yaml
│ ├── deployment.yaml
│ └── service.yaml
├── identity/ # Authentication service
│ ├── config.yaml
│ ├── deployment.yaml
│ └── service.yaml
├── mailhog/ # Email testing tool
│ ├── config.yaml
│ ├── deployment.yaml
│ ├── ingress.yaml
│ └── service.yaml
├── mongodb/ # MongoDB manifest
│ ├── config.yaml
│ ├── service.yaml
│ ├── statefulset.yaml
│ └── storage.yaml
├── postgres/ # PostgreSQL manifest
│ ├── config.yaml
│ ├── service.yaml
│ ├── statefulset.yaml
│ └── storage.yaml
├── rbac/ # Role-Based Access Control
│ ├── role.yaml
│ └── rolebinding.yaml
├── web/ # Frontend React app
│ ├── configmap.yaml
│ ├── deployment.yaml
│ └── ingress.yaml
├── workshop/ # Custom training scenarios
│ ├── config.yaml
│ ├── deployment.yaml
│ └── service.yaml
├── build-all.sh # Script to build images (if applicable)
├── deploy.sh # Script to apply all manifests
└── README.md # Project documentation
---

## 🚀 How to Deploy

### 🧰 Prerequisites

- Kubernetes cluster (Minikube, KIND, EKS, etc.)
- `kubectl` configured and connected
- Docker (for building custom images if needed)

---

### 📦 Build & Deploy

> You can run everything with the helper scripts:

```bash
chmod +x build-all.sh deploy.sh

# Build docker images if required
./build-all.sh

# Deploy all services
./deploy.sh
````

Or apply each component individually:

```bash
kubectl apply -f ./mongodb
kubectl apply -f ./postgres
kubectl apply -f ./identity
kubectl apply -f ./gateway-service
kubectl apply -f ./community
kubectl apply -f ./web
kubectl apply -f ./mailhog
kubectl apply -f ./rbac
kubectl apply -f ./workshop
```

---

## 🧪 Vulnerabilities to Explore

This deployment exposes several real-world API security issues:

| 🔓 Vulnerability            | 💥 Example to Break It                                  |
| --------------------------- | ------------------------------------------------------- |
| BOLA (IDOR)                 | Access another user's data via `userId` in endpoint     |
| Broken Authentication       | Bypass login with weak tokens or credential reuse       |
| Mass Assignment             | Modify user roles or internal fields via JSON input     |
| Insecure Storage            | Secrets in environment variables or unencrypted volumes |
| Lack of Rate Limiting       | Brute-force login or password reset APIs                |
| Insecure Deserialization    | Payload injection via serialized input                  |
| Insecure API Gateway Config | Access internal services directly                       |
| Misconfigured RBAC          | Gain unintended access across services                  |
| Email Takeover              | Hijack password reset functionality using mailhog       |
| SSRF                        | Exploit internal services via crafted URL requests      |

---


## 🧹 Clean Up

```bash
kubectl delete -f ./mongodb
kubectl delete -f ./postgres
...
```

---

## 📄 License

This repo contains configuration files and is MIT licensed. crAPI is under [OWASP license](https://github.com/OWASP/crAPI).

---

## 🙋 Maintainer

**Ghaith Rouahi**
💻 GitHub: [@GhaithRouahi](https://github.com/GhaithRouahi)
