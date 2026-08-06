# 🚀 3-Tier Enterprise Web Application — GitOps & DevSecOps Pipeline

An end-to-end production-grade deployment of a 3-Tier Web Application (ReactJS Frontend, Node.js/Express Backend, and MongoDB Database) running on Kubernetes with GitOps, CI/CD automation, and full observability.

---

## 🛠️ Tech Stack & Architecture

* **Application Stack:** React.js, Node.js / Express.js, MongoDB
* **Containerization:** Docker & Docker Hub
* **CI Automation:** Jenkins Pipelines
* **CD & GitOps:** ArgoCD
* **Orchestration:** Kubernetes (Deployments, Services, ConfigMaps, PV/PVC, Namespaces)
* **Monitoring & Observability:** Prometheus & Grafana (Deployed via Helm)

---

## 🔄 End-to-End Workflow

[ Developer ] ➔ [ GitHub Repo ] ➔ [ Jenkins Pipeline ] ➔ [ Docker Hub ]
│
(Manifest Sync)
▼
[ Grafana/Prometheus ] ◄── [ Kubernetes Cluster ] ◄── [ ArgoCD ]


1. **Continuous Integration (CI):** 
   * Code push triggers the **Jenkins** pipeline.
   * Jenkins builds optimized Docker images for Frontend and Backend microservices.
   * Automated tagging and pushing of artifacts to **Docker Hub**.

2. **GitOps Continuous Delivery (CD):**
   * **ArgoCD** continuously monitors the Kubernetes manifest directory in Git.
   * Automatically detects configuration drift and syncs application state into the isolated `three-tier` K8s namespace.

3. **Kubernetes Orchestration & Persistence:**
   * **Deployments:** Managed rolling updates and zero-downtime strategy.
   * **Services:** Internal networking via ClusterIP for secure intra-pod communication.
   * **Data Persistence:** MongoDB state is preserved using Kubernetes **PersistentVolumes (PV)** and **PersistentVolumeClaims (PVC)**.

4. **Observability & Monitoring:**
   * Deployed `kube-prometheus-stack` using **Helm**.
   * **Prometheus** collects real-time pod health, CPU/Memory resource consumption, and cluster metrics.
   * **Grafana** visualizes cluster state using pre-configured Kubernetes operational dashboards.

---

## 🚀 How to Run Locally

### Prerequisites
* Kubernetes Cluster (Minikube / Docker Desktop / K3s)
* `kubectl` CLI
* `helm` package manager

### Deployment Steps

1. **Clone the Repository:**
   ```bash
   git clone [https://github.com/Tejas-Shende056/ThreeTierApp.git](https://github.com/Tejas-Shende056/ThreeTierApp.git)
   cd ThreeTierApp
Apply Kubernetes Manifests:

Bash


kubectl create namespace three-tier
kubectl apply -f k8s/ -n three-tier
Setup Monitoring Stack:

Bash


helm repo add prometheus-community [https://prometheus-community.github.io/helm-charts](https://prometheus-community.github.io/helm-charts)
helm repo update
helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring --create-namespace
Access Grafana Dashboard:

Bash


kubectl port-forward svc/prometheus-grafana 3000:80 -n monitoring
Open http://localhost:3000 in your browser.
