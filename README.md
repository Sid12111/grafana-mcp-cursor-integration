## 🤖 Grafana + MCP + Cursor Integration Project
This project demonstrates how to connect:

Cursor AI → MCP Server → Grafana → Prometheus

It allows Cursor AI to automatically:
- 📊 Create dashboards
- 🧩 Update panels
- 📡 Query Prometheus metrics
- 🛠 Manage Grafana programmatically

---

## 📦 Project Structure
```
grafana-mcp-cursor-integration/
│
├── docker-compose.yml
├── prometheus/
│   └── prometheus.yml
├── cursor/
│   └── mcp.json
├── .env
├── README.md
```

---

## 🧠 Architecture Overview
```
Your Browser
   ↓
localhost:3000
   ↓
Grafana
   ↓
Prometheus
   ↓
Node Exporter

Cursor AI
   ↓
MCP Server (Docker container)
   ↓
Grafana REST API
```

---

## 🛠 Prerequisites
Ensure you have:
- ✅ Docker installed
- ✅ Docker Compose installed
- ✅ Cursor installed
- ✅ Internet connection

Verify Docker:
```bash
docker --version
docker compose version
```

---

## 🚀 STEP 1 — Clone or Download Project

```bash
git clone https://github.com/Sid12111/grafana-mcp-cursor-integration.git
cd grafana-mcp-cursor-integration
```

---

## 🚀 STEP 2 — Start Monitoring Stack
```bash
docker compose up -d
```
Starts:
- node-exporter
- prometheus
- grafana

Check containers:
```bash
docker ps
```

---

## 🌍 STEP 3 — Open Grafana
Open browser:
http://localhost:3000

Login:
- **Username:** admin
- **Password:** admin123

---

## 🔑 STEP 4 — Create Grafana API Key
1. Go to ⚙️ Settings
2. Service Accounts
3. Create Service Account: `mcp-admin`
4. Role: Admin
5. Generate Token
6. Copy and save the token

---

## 🤖 STEP 5 — Configure MCP in Cursor
Replace `mcp.json` with:
```json
{
  "mcpServers": {
    "grafana": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "-e", "GRAFANA_URL",
        "-e", "GRAFANA_API_KEY",
        "mcp/grafana",
        "-t", "stdio"
      ],
      "env": {
        "GRAFANA_URL": "http://host.docker.internal:3000",
        "GRAFANA_API_KEY": "PASTE_YOUR_API_KEY_HERE"
      }
    }
  }
}
```

---

## 🧪 STEP 6 — Test MCP Connection
Cursor should show **Connected**.

If not:
- Restart Cursor
- Check Docker
- Verify API key

---

## 🎯 STEP 7 — Use AI to Create Dashboard
Try in Cursor:
```
Create a dashboard showing:
- CPU usage
- Memory usage
- Targets up/down
```

Check Grafana at http://localhost:3000

---

## 📊 Example AI Commands
- Create dashboard: `Create dashboard for Prometheus overview`
- Add panel: `Add panel showing 95th percentile scrape duration`
- List dashboards: `List all dashboards`
- Delete dashboard: `Delete dashboard named test-dashboard`

---

## 🔍 Troubleshooting
### Grafana not opening?
```bash
docker ps
docker compose up -d
```

### MCP not connecting?
- Docker running?
- API key correct?
- Using host.docker.internal?

### Prometheus not scraping?
Go to:
http://localhost:9090 → Status → Targets

---

## 🔐 Security Notes
- Use HTTPS in production
- Do not commit API keys
- Use Docker secrets
- Use reverse proxy

---

## 🧹 Stop Everything
```bash
docker compose down
docker compose down -v
```

---

## 👨‍💻 Author
**Siddharth**
DevOps • Cloud • Security
