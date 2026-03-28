# Containerized Monitoring Stack

A self-hosted, containerized observability stack for monitoring AWS EC2 instances and NAS servers in real time. Built with Docker, Prometheus, and Grafana. The other projects were made under different Repositories

## Overview

This project sets up a lightweight monitoring stack using Docker Compose. It collects system-level metrics from a remote server using Node Exporter and visualizes them through Grafana dashboards.

## Architecture
```
Remote Server (EC2)             Local Machine
└── Node Exporter               └── docker-compose.yml
    └── :9100                       ├── Prometheus → scrapes metrics
                                    └── Grafana    → visualizes dashboards
```

## Stack

| Tool || Purpose |

| **Docker Compose** | Container orchestration |
| **Prometheus** | Metrics collection |
| **Grafana** | Dashboard visualization |
| **Node Exporter** | System metrics agent |

## Getting Started

### Prerequisites
- Docker Desktop installed
- Docker Compose v2+
- Target server with Node Exporter running

## Node Exporter Setup (on target server)
```bash
docker run -d \
  --name node-exporter \
  --net="host" \
  --pid="host" \
  -v "/:/host:ro,rslave" \
  prom/node-exporter \
  --path.rootfs=/host
```

### 1. Clone the repo
```bash
git clone [https://github.com/yourusername/monitoring-stack.git](https://github.com/P4cha-qvtek/Containerized-Monitoring-Stack.git)
cd monitoring-stack
```

### 2. Configure Prometheus
```bash
cp prometheus.yml.example prometheus.yml
```
Edit `prometheus.yml` and replace `<YOUR-EC2-IP>` with your server's public IP.

### 3. Run the stack
```bash
docker compose up -d
```

### 4. Access the dashboards
- Prometheus: `http://localhost:9090`
- Grafana: `http://localhost:3000` (default: admin/admin)

