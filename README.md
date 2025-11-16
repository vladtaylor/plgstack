🚀 **Full Observability Stack Setup Guide (PLPA)**

This repository contains a complete, lightweight, and modern observability stack for your homelab, featuring:

- **Promtail** – Log collection  
- **Loki** – Log storage  
- **Grafana** – Visualization & UI  

> **Note:** The original stack also referenced Prometheus and Alertmanager, but the current `docker-compose.yaml` is trimmed to Loki, Promtail, and Grafana only.

This stack is designed to run easily in Docker and centralize your application and system logs.

---

### 1. ⚙️ Deployment and Configuration

Follow these steps to get your logging and monitoring system running:

- **📦 Save the files**
  - Ensure all essential YAML configuration files are placed in the same directory:
    - `docker-compose.yaml`
    - `loki-config.yaml`
    - `promtail-config.yaml`

- **▶️ Start the stack**
  - Run the following command in the directory containing the files to download images and start the services in the background:

```bash
docker compose up -d
```

---

### 2. 🌐 Accessing the Web UI

Once the stack is running, you can access Grafana here:

| Service | Purpose                            | URL                                                         |
|--------:|------------------------------------|-------------------------------------------------------------|
| Grafana | Central UI for logs and dashboards | `http://localhost:3030` (or `http://<your-server-ip>:3030`) |

- **Default Grafana login**: `admin` / `strongpassword`  
  - Change this immediately after logging in.

---

### 3. 🔗 Configure Data Sources in Grafana

Grafana needs to know where to find your logs (Loki):

1. In Grafana, go to **Configuration → Data sources**.
2. **Add Loki (Logs)**:
   - Click **Add data source** and select **Loki**.
   - Under **HTTP → URL**, enter: `http://loki:3100` (this uses the Docker service name).
   - Click **Save & Test**.

---

### 4. 🔔 Basic Alerting (Optional, Loki-only)

You can build useful alerting workflows inside Grafana based on **Loki log queries**:

- Use **LogQL** to trigger alerts based on log patterns (for example, lines containing `"ERROR"`).
- Configure alert rules directly within Grafana (bell icon 🔔 in the left sidebar).

For full metrics and external alert routing (Prometheus + Alertmanager), you can later reintroduce those services and extend this README accordingly.