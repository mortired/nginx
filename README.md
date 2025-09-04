# Nginx Reverse Proxy with Let's Encrypt

A Docker Compose setup for nginx reverse proxy with automatic SSL certificate management using Let's Encrypt.

## Prerequisites

- Docker
- Docker Compose
- Domain name pointing to your server

## Quick Start

### 1. Clone the Repository

```bash
git clone <repository-url>
cd nginx
```

### 2. Environment Setup

Create a `.env` file in the project directory:

```bash
echo "LETSENCRYPT_EMAIL=your-email@example.com" > .env
```

Replace `your-email@example.com` with your actual email address for Let's Encrypt notifications.

### 3. Start the Services

```bash
docker-compose up -d
```

### 4. Verify Installation

Check if containers are running:

```bash
docker-compose ps
```

## Usage

### Adding a New Service

To proxy a new service, add the following labels to your service's docker-compose.yml:

```yaml
services:
  your-app:
    # ... your app configuration
    labels:
      - "com.github.jrcs.letsencrypt_nginx_proxy_companion.nginx_proxy=true"
      - "nginx-proxy.host=your-domain.com"
      - "nginx-proxy.port=3000"  # your app's internal port
```

### SSL Certificates

SSL certificates are automatically generated and renewed by the Let's Encrypt companion container. No manual intervention required.

## Management Commands

```bash
# Start services
docker-compose up -d

# Stop services
docker-compose down

# View logs
docker-compose logs -f

# Restart services
docker-compose restart

# Update services
docker-compose pull
docker-compose up -d
```

## Troubleshooting

- **Port conflicts**: Ensure ports 80 and 443 are available
- **SSL issues**: Check that your domain DNS points to the server
- **Container logs**: Use `docker-compose logs [service-name]` to debug

## Services

- **nginx-proxy**: Main reverse proxy server
- **letsencrypt**: Automatic SSL certificate management
