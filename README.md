Full Observability Stack Setup Guide (PLPA)

This stack is now a PLPA setup (Promtail, Loki, Prometheus, Alertmanager) integrated with Grafana. This gives you both logs and metrics capabilities.

1. Deployment and Configuration

Save the files: Ensure all five YAML files (docker-compose.yaml, loki-config.yaml, promtail-config.yaml, prometheus.yaml, and alertmanager.yaml) are saved in the same directory.

CRITICAL PUSHOVER SETUP: Before starting, open alertmanager.yaml and replace the placeholder values (YOUR_PUSHOVER_APP_TOKEN and YOUR_PUSHOVER_USER_KEY) with your actual Pushover Application Key and User Key. This centralizes all your notifications.

Start the stack: Run the following command from that directory:

docker compose up -d


This launches all five services.

2. Accessing the Web UIs

Grafana (Web UI, Logs, Metrics, Alerts): http://localhost:3000 (or http://<your-server-ip>:3000)

Default Login: admin/strongpassword

Prometheus (Metrics UI): http://localhost:9090

Alertmanager (Alert Routing UI): http://localhost:9093

3. Configure Data Sources in Grafana

Grafana needs to connect to both Loki (Logs) and Prometheus (Metrics):

In Grafana, hover over the gear icon (Configuration) in the left sidebar and click Data Sources.

Add Loki (Logs):

Click Add data source and select Loki.

Under HTTP > URL, enter: http://loki:3100

Click Save & Test.

Add Prometheus (Metrics):

Click Add data source and select Prometheus.

Under HTTP > URL, enter: http://prometheus:9090

Click Save & Test.

4. Alerting is Centralized

Because Alertmanager is now included, all alerting is managed through it:

Pushover: The Alertmanager service (alertmanager.yaml) handles the connection to Pushover.

Alert Rules: You create all alert rules within Grafana (using the bell icon in the sidebar). You can write rules based on both Loki logs (LogQL) or Prometheus metrics (PromQL). Grafana forwards these rules to Alertmanager, which handles the grouping, silencing, and sending the final notification to Pushover.
