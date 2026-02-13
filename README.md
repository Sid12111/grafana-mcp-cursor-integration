# 🤖 Grafana + MCP + Cursor Integration Project

This project demonstrates how to connect:

Cursor AI → MCP Server → Grafana → Prometheus

It allows Cursor AI to automatically:
- Create dashboards
- Update panels
- Query Prometheus metrics
- Manage Grafana programmatically

This is an DevOps + AI integration project.

---

📦 Project Structure
grafana-mcp-cursor-integration/
│
├── docker-compose.yml
├── prometheus/
│   └── prometheus.yml
├── cursor/
│   └── mcp.json
├── .env
├── README.md

# 🧠 Architecture Overview

Your Browser
|
localhost:3000
|
Grafana
|
Prometheus
|
Node Exporter

Cursor AI
|
MCP Server (Docker container)
|
Grafana REST API


---

# 🛠 Prerequisites

Make sure you have:

- ✅ Docker installed
- ✅ Docker Compose installed
- ✅ Cursor installed
- ✅ Internet connection (to pull Docker images)

To verify Docker:

```bash
docker --version
docker compose version

🚀 STEP 1 — Clone or Download Project

Option A: Clone

git clone https://github.com/YOUR_USERNAME/grafana-mcp-cursor-integration.git
cd grafana-mcp-cursor-integration


Option B: Download ZIP from GitHub and extract it.

🚀 STEP 2 — Start Monitoring Stack

Run:

docker compose up -d


This will start:

node-exporter

prometheus

grafana

Check containers:

docker ps


You should see 3 containers running.

🌍 STEP 3 — Open Grafana

Open in browser:

http://localhost:3000


Login:

Username:

admin


Password:

admin123


If prompted to change password, you may skip for now.

🔑 STEP 4 — Create Grafana API Key 

Cursor connects to Grafana using an API key.

Inside Grafana:

Click ⚙️ Settings

Go to "Service Accounts"

Click "Create Service Account"

Name it: mcp-admin

Role: Admin

Click Create

Click "Generate Token"

Copy the token immediately

⚠️ Save this token. You will not see it again.

🤖 STEP 5 — Configure MCP in Cursor

Open Cursor.

Go to:

File → Preferences → Cursor Settings
OR
Cmd/Ctrl + Shift + P → Search "Cursor Settings"

Find:

Tools & Integrations → MCP Servers

Click:

"New MCP Server"

This opens your mcp.json.

Replace contents with:

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


IMPORTANT:

Replace:

PASTE_YOUR_API_KEY_HERE


with your real token.

❗ Why host.docker.internal?

Because:

Cursor runs on your computer (host machine)

MCP runs inside Docker

Grafana runs inside Docker

host.docker.internal allows Docker container to access host services.

DO NOT use:

http://localhost:3000


inside MCP configuration.

🧪 STEP 6 — Test MCP Connection

Save mcp.json.

Cursor should show:

✅ Connected
or
Green indicator

If not:

Restart Cursor

Ensure Docker is running

🎯 STEP 7 — Use AI to Create Dashboard

Open Cursor AI chat.

Try:

Create a dashboard showing:
- CPU usage
- Memory usage
- Targets up/down


You should see:

Ran update_dashboard:grafana


Now check:

http://localhost:3000

Your new dashboard should appear 🎉

📊 Example AI Commands

Create dashboard:

Create dashboard for Prometheus overview


Add panel:

Add panel showing 95th percentile scrape duration


List dashboards:

List all dashboards


Delete dashboard:

Delete dashboard named test-dashboard

🔍 Troubleshooting
❌ Grafana not opening?

Check:

docker ps


If not running:

docker compose up -d

❌ MCP not connecting?

Check:

Docker running?

API key correct?

Using host.docker.internal?

Restart Cursor

❌ Prometheus not scraping?

Open:

http://localhost:9090


Go to:

Status → Targets

All targets should be UP.

🔐 Security Notes

This project is for local development.

For production:

Use HTTPS

Restrict API token permissions

Do not commit API keys to GitHub

Use Docker secrets

Use reverse proxy

🧹 Stop Everything
docker compose down


To remove volumes:

docker compose down -v

👨‍💻 Author

Siddharth 
DevOps | Cloud | Security 
