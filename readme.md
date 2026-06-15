# Monitoring & Alerting System with Prometheus, Grafana & Alertmanager

A production-style monitoring stack built with **Prometheus**, **Grafana**, **Node Exporter**, **cAdvisor**, and **Alertmanager** running in Docker containers. This project provides real-time infrastructure monitoring, visualization dashboards, and automated email alerting.

---

## Project Overview

This project demonstrates how to build a complete monitoring and alerting solution commonly used in DevOps and Site Reliability Engineering (SRE) environments.

The stack monitors:

* Server CPU utilization
* Memory usage
* Disk usage
* Network statistics
* Docker container metrics
* Prometheus health
* Custom alert rules

When predefined thresholds are exceeded, Prometheus triggers alerts which are routed through Alertmanager and delivered via email.

---

## Architecture

```text
                    ┌───────────────────┐
                    │   Node Exporter   │
                    └─────────┬─────────┘
                              │
                    ┌─────────▼─────────┐
                    │    Prometheus     │
                    │ Metrics Collection│
                    └─────────┬─────────┘
                              │
            ┌─────────────────┴─────────────────┐
            │                                   │
            ▼                                   ▼
   ┌─────────────────┐              ┌─────────────────┐
   │    Grafana      │              │ Alertmanager    │
   │ Visualization   │              │ Email Alerts    │
   └─────────────────┘              └─────────────────┘
```

---

## Technologies Used

* Docker
* Docker Compose
* Prometheus
* Grafana
* Alertmanager
* Node Exporter
* cAdvisor
* Gmail SMTP

---

## Project Structure

```text
monitoring-system/
│
├── docker-compose.yml
│
├── prometheus/
│   ├── prometheus.yml
│   └── alert.rules.yml
│
├── alertmanager/
│   └── alertmanager.yml
│
├── grafana/
│   └── provisioning/
│
├── docs/
│   ├── architecture.png
│   ├── dashboards.png
│   └── alerts.png
│
├── .env
│
└── README.md
```

---

## Features

### Metrics Collection

Prometheus scrapes metrics from:

* Prometheus Server
* Node Exporter
* cAdvisor

### Dashboard Visualization

Grafana provides:

* Server Health Dashboard
* CPU Monitoring
* Memory Monitoring
* Disk Utilization
* Container Metrics
* Historical Performance Trends

### Email Alerting

Alertmanager sends email notifications when:

* CPU usage exceeds threshold
* Memory usage exceeds threshold
* Services become unavailable
* Custom test alerts are triggered

---

## Prerequisites

Install the following:

### Docker

```bash
docker --version
```

### Docker Compose

```bash
docker compose version
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/yourusername/monitoring-system.git

cd monitoring-system
```

---

## Environment Variables

Create a `.env` file in the project root:

```env
SMTP_TO=your-email@gmail.com
SMTP_FROM=your-email@gmail.com
SMTP_USERNAME=your-email@gmail.com
SMTP_PASSWORD=your-gmail-app-password
```

### Gmail App Password

1. Enable Two-Factor Authentication.
2. Create a Google App Password.
3. Use the generated password as `SMTP_PASSWORD`.

---

## Start the Stack

```bash
docker compose up -d
```

Verify containers:

```bash
docker ps
```

Expected services:

```text
prometheus
grafana
alertmanager
node-exporter
cadvisor
```

---

## Access the Services

### Grafana

```text
http://localhost:3000
```

Default credentials:

```text
Username: admin
Password: admin
```

---

### Prometheus

```text
http://localhost:9090
```

---

### Alertmanager

```text
http://localhost:9093
```

---

## Configure Grafana

### Add Prometheus Data Source

Navigate to:

```text
Connections → Data Sources → Add Data Source
```

Select:

```text
Prometheus
```

URL:

```text
http://prometheus:9090
```

Click:

```text
Save & Test
```

---

## Import Dashboard

Import Grafana Dashboard ID:

```text
1860
```

Dashboard Name:

```text
Node Exporter Full
```

This dashboard provides comprehensive Linux server monitoring.

---

## Alert Rules

### High CPU Usage

```yaml
alert: HighCPUUsage
```

Triggers when:

```text
CPU Usage > 80%
```

for:

```text
2 minutes
```

---

### High Memory Usage

```yaml
alert: HighMemoryUsage
```

Triggers when:

```text
Memory Usage > 85%
```

for:

```text
2 minutes
```

---

## Testing Alerts

Create a test alert:

```yaml
groups:
  - name: test-alerts
    rules:
      - alert: TestAlert
        expr: vector(1)
        for: 10s
        labels:
          severity: critical
        annotations:
          summary: Test Alert
          description: This is a test alert
```

Reload Prometheus:

```bash
docker compose restart prometheus
```

Verify:

```text
Prometheus → Alerts
```

Alert should transition:

```text
PENDING → FIRING
```

Then verify delivery:

```text
Alertmanager → Alerts
```

and check your email inbox.

---

## Troubleshooting

### Prometheus Keeps Restarting

Validate configuration:

```bash
docker exec -it prometheus cat /etc/prometheus/prometheus.yml
```

Check logs:

```bash
docker logs prometheus
```

---

### Alertmanager Email Authentication Failed

Common error:

```text
535 Username and Password not accepted
```

Solution:

* Use a Gmail App Password
* Do not use your Gmail login password
* Verify SMTP credentials in `.env`

---

### Grafana Cannot Connect to Prometheus

Incorrect:

```text
http://localhost:9090
```

Correct:

```text
http://prometheus:9090
```

when Grafana is running in Docker.

---

## Screenshots

### Architecture Diagram

Add:

```text
docs/architecture.png
```

---

### Grafana Dashboard

Add:

```text
docs/dashboards.png
```

---

### Alert Notification

Add:

```text
docs/alerts.png
```

---

## Skills Demonstrated

* Linux Administration
* Docker & Docker Compose
* Infrastructure Monitoring
* Metrics Collection
* Observability
* Alerting & Incident Detection
* Prometheus
* Grafana
* Alertmanager
* YAML Configuration
* SMTP Integration
* DevOps Best Practices

---

## Future Improvements

* Slack Notifications
* Microsoft Teams Integration
* PagerDuty Integration
* Kubernetes Monitoring
* Blackbox Exporter
* Loki Log Aggregation
* Grafana Alerting
* Docker Secrets Integration
* AWS Cloud Monitoring

---

## Author

**Sadiq Abdulrahaman**

DevOps Engineer | Linux Administrator | Cloud Enthusiast

GitHub: [https://github.com/Ramsoon](https://github.com/Ramsoon)

LinkedIn: [https://linkedin.com/in/sadiq247](https://linkedin.com/in/sadiq247)

