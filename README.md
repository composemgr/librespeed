## 👋 Welcome to librespeed 🚀

Lightweight web-based speed test

## 📋 Description

LibreSpeed is a self-hosted bandwidth test with a web frontend, optional
results sharing, and a results viewer for admins. It runs as a single container
with no external dependencies, using a local SQLite database.

## 🚀 Services

- **app**: ghcr.io/librespeed/speedtest:latest

## 📦 Installation

### Option 1: Quick Install

```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/librespeed/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone

```bash
git clone "https://github.com/composemgr/librespeed" ~/.local/srv/docker/librespeed
cd ~/.local/srv/docker/librespeed
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr

```bash
composemgr install librespeed
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
APP_ORG_NAME=LibreSpeed
APP_ADMIN_PASS=replace-with-a-random-password
EMAIL_SERVER_MAIL_FROM=no-reply@example.com
IPINFO_APIKEY=replace-with-your-ipinfo-api-key
```

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64233` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

The proxy variants publish no host ports. The app is reachable only through the
proxy network.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64233

The admin results viewer needs `EMAIL` and `PASSWORD` set in `app.env` before the
first start, otherwise there is no way to log in to it later.

## 📂 Volumes

- `./volumes/data/librespeed` - SQLite results database
- `./volumes/config/librespeed` - LibreSpeed configuration

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

A speed test is bandwidth-intensive. Running one on a metered or shared uplink
will slow down other traffic while it runs, so this is best kept on a server
with headroom.

`REDACT_IP_ADDRESSES` is set to `false`, which means stored results keep visitor
IP addresses. Set it to `true` in the compose file before enabling the results
viewer on a public instance.

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
