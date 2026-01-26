## 👋 Welcome to librespeed 🚀

Self-hosted librespeed application

## 📋 Description

Self-hosted librespeed application

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
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install librespeed
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
APP_ORG_NAME=Libre
EMAIL_SERVER_MAIL_FROM=no-reply@${BASE_DOMAIN_NAME:-${BASE_HOST_NAME
APP_ADMIN_PASS=changeme_admin_password
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:62000

## 📂 Volumes

- `./rootfs/data/librespeed` - Data storage
- `./rootfs/config/librespeed` - Data storage

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
