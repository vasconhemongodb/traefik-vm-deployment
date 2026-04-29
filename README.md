# Shared Infrastructure (EC2)

This repository manages the Traefik reverse proxy and the shared `web-proxy` network for all applications on a given EC2 instance.

## Setup Instructions

1. **Initialize Certificate Storage:**
   ```bash
   touch traefik/data/acme.json
   chmod 600 traefik/data/acme.json
   ```

2. **Configure Environment:**
   ```bash
   cp .env.example .env
   # Edit .env and add your email for Let's Encrypt
   ```

3. **Start the Proxy:**
   ```bash
   docker compose up -d
   ```
