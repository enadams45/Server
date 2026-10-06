# Server

A VLESS-over-WebSocket proxy server running on Xray, deployed to Google Cloud Run.

## What it does

- **VLESS protocol** on port 8080 with WebSocket transport
- **HTTP fallback** on port 8081 for health checks and a status dashboard
- **Dashboard** showing uptime, connected users, and server stats
- **One-click deployment** to Google Cloud Run

## Quick start

### Local deployment

```bash
docker build -t server .
docker run -p 8080:8080 -e PORT=8080 server
```

### Cloud Run deployment

```bash
chmod +x deploy.sh
./deploy.sh
```

Follow the prompts to configure service name, CPU, and memory, then deploy.

## Configuration

Edit `config.json` to customize:

- **UUID**: Change the `id` field under `inbounds[0].settings.clients[0].id`
- **WebSocket path**: Modify `inbounds[0].streamSettings.wsSettings.path`
- **Port**: Update `inbounds[0].port` (entrypoint.sh will override this from `PORT` env var)

## Files

- `config.json` — Xray configuration
- `Dockerfile` — Container build
- `entrypoint.sh` — Startup script
- `server.py` — Status dashboard (port 8081)
- `deploy.sh` — Google Cloud deployment automation
- `network-monitor.sh` — Health monitoring utility
