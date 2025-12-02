# 🚀 Jenkins Observability Stack: Prometheus + Grafana + Node Exporter

![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=Prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=Grafana&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=Jenkins&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white)

## 📖 Overview
This project establishes a complete **DevOps Observability Pipeline**. It monitors the health, performance, and build history of a Jenkins CI/CD server, alongside the real-time hardware metrics (CPU, RAM, Disk) of the underlying cloud infrastructure (Google Cloud Platform).

The stack uses **Prometheus** to scrape metrics and **Grafana** to visualize them in rich, interactive dashboards.

## 🛠️ Tech Stack
* **Jenkins:** Automation Server (CI/CD).
* **Prometheus:** Time-series database for metric collection.
* **Grafana:** Visualization dashboard.
* **Node Exporter:** Hardware metrics collector.
* **Docker & Docker Compose:** Container orchestration.
* **Google Cloud Platform (GCP):** Cloud infrastructure provider.

## 📸 Screenshots

### 1. Jenkins Build Health Dashboard
<img width="1898" height="1139" alt="node-exporter-dashboard" src="https://github.com/user-attachments/assets/ddf35138-a125-4ac5-80f7-558349b29894" />
<img width="1920" height="1200" alt="jenkins-deshboard" src="https://github.com/user-attachments/assets/3f56eb00-99c5-46cf-837c-d411dd633a93" />
*(Shows build success/fail rates and duration)*
![Jenkins Dashboard](./images/jenkins-dashboard.png)
### 2. Server Hardware Monitoring (Node Exporter )
<img width="1920" height="1200" alt="jenkins-deshboard" src="https://github.com/user-attachments/assets/0e7549f3-a8df-4f9c-91c5-361d59f717fb" />
<img width="1898" height="1139" alt="node-exporter-dashboard" src="https://github.com/user-attachments/assets/6c622eff-b29b-4008-bdd8-bc5b65dc84cd" />
*(Shows real-time CPU, Memory, and Disk usage)*
![Node Exporter Dashboard](./images/node-exporter-dashboard.png)

---

## 🏗️ Architecture

1.  **Node Exporter** runs on the server and exposes hardware metrics at port `9100`.
2.  **Jenkins** (with Prometheus plugin) exposes build metrics at port `8080`.
3.  **Prometheus** scrapes both targets every 15 seconds.
4.  **Grafana** queries Prometheus to display data on port `3000`.

---

## ⚙️ Setup & Installation

### Prerequisites
* A Linux VM (Ubuntu/Debian recommended) on AWS/GCP/Azure.
* Docker & Docker Compose installed.
* Jenkins installed and running on port `8080`.

### Step 1: Clone the Repository
```bash
git clone [https://github.com/YOUR_USERNAME/jenkins-monitoring-project.git](https://github.com/YOUR_USERNAME/jenkins-monitoring-project.git)
cd jenkins-monitoring-project


Step 2: Configure Prometheus
Open prometheus.yml and replace YOUR_SERVER_IP with your actual VM IP address.

YAML

  - job_name: 'jenkins'
    metrics_path: '/prometheus/'
    static_configs:
      - targets: ['YOUR_SERVER_IP:8080']
Step 3: Launch the Stack
Run the services using Docker Compose:

Bash

sudo docker compose up -d
Step 4: Access Grafana
Open your browser: http://<YOUR_IP>:3000

Login: admin / admin

Add Data Source: Select Prometheus -> Enter URL http://prometheus:9090

Import Dashboards:

Node Exporter Full: ID 1860

Jenkins Performance: ID 9964

📂 Configuration Files Explained
docker-compose.yml
Orchestrates the three monitoring containers.

Prometheus: Mounts the config file and listens on port 9090.

Grafana: Persists data and listens on port 3000.

Node Exporter: Mounts system paths to read hardware stats.

prometheus.yml
The "Brain" of the operation. It tells Prometheus where to look for data.

scrape_interval: Set to 15s for near real-time updates.

targets: Defines the specific IP addresses and ports to scrape.

