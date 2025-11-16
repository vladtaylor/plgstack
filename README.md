🚀 **Full Observability Stack Setup Guide (PLPA)**

This repository contains a complete, lightweight, and modern observability stack for your homelab, featuring:

- **Promtail** – Log collection  
- **Loki** – Log storage  
- **Prometheus** – Metrics collection  
- **Alertmanager** – Alert routing (via Pushover)  
- **Grafana** – Visualization & UI  

This stack is designed to run easily in Docker and centralize your application and system logs.

---

### 1. ⚙️ Deployment and Configuration

Follow these steps to get your logging and monitoring system running:

- **📦 Save the files**
  - Ensure all essential YAML configuration files are placed in the same directory:
    - `docker-compose.yaml`
    - `loki-config.yaml`
    - `promtail-config.yaml`
    - `prometheus.yaml`
    - `alertmanager.yaml`

- **▶️ Start the stack**
  - Run the following command in the directory containing the files to download images and start the services in the background:

```bash
docker compose up -d
```

---

### 2. 🌐 Accessing the Web UIs

Once the stack is running, you can access the following web interfaces:

| Service     | Purpose                                | URL                                                         |
|------------:|----------------------------------------|-------------------------------------------------------------|
| Grafana     | Central UI for logs, metrics, alerts   | `http://localhost:3030` (or `http://<your-server-ip>:3030`) |
| Prometheus  | Metrics query and status UI            | `http://localhost:9090`                                     |
| Alertmanager| Alert grouping and routing UI          | `http://localhost:9093`                                     |

- **Default Grafana login**: `admin` / `strongpassword`  
  - Change this immediately after logging in.

---

### 3. 🔗 Configure Data Sources in Grafana

Grafana needs to know where to find your logs (Loki) and metrics (Prometheus):

1. In Grafana, go to **Configuration → Data sources**.
2. **Add Loki (Logs)**:
   - Click **Add data source** and select **Loki**.
   - Under **HTTP → URL**, enter: `http://loki:3100` (this uses the Docker service name).
   - Click **Save & Test**.
3. **Add Prometheus (Metrics)**:
   - Click **Add data source** and select **Prometheus**.
   - Under **HTTP → URL**, enter: `http://prometheus:9090`.
   - Click **Save & Test**.

---

### 4. 🔔 Alerting Workflow with Pushover

Alertmanager is wired to send notifications via **Pushover**.

1. Open `alertmanager.yaml` and replace:
   - `YOUR_PUSHOVER_APP_TOKEN` with your Pushover **Application Key**.
   - `YOUR_PUSHOVER_USER_KEY` with your Pushover **User Key** or **Group Key**.
2. In Grafana, create alert rules (using the bell icon 🔔) based on:
   - **LogQL** (Loki) queries – e.g., log lines containing `"ERROR"`.
   - **PromQL** (Prometheus) queries – e.g., CPU usage > 90%.
3. Grafana forwards these alerts to Alertmanager, which then sends notifications to your Pushover devices.