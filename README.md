# 📡 RTMP Streamer Secure

A modular, Dockerized RTMP/HLS streaming stack with SSL encryption, login protection, and browser-friendly playback. Built for private matchday broadcasts, telemetry overlays, and reproducible deployment.

## 🔧 Features

- RTMP ingest via OBS or compatible encoder  
- HLS playback with `.m3u8` streaming  
- NGINX RTMP module inside Docker  
- SSL encryption via Dockerized Certbot  
- Login protection with basic auth  
- Modular splash page served via NGINX  
- Reverse proxy ready for HTTPS termination and multi-service routing

## 🚀 Quick Start

```bash
git clone https://github.com/mowaxuk/rtmp-streamer-secure.git
cd rtmp-streamer-secure
docker compose up -d
```

Then visit your stream portal at:  
**https://stream-mowaxuk.hopto.org**

## 📁 File Structure

```
rtmp-streamer-secure/
├── docker-compose.yml
├── nginx/
│   ├── nginx.conf
│   └── certs/ (mounted via Certbot)
├── html/
│   └── index.html (splash page)
├── .gitignore
└── LICENSE
```

## 🔐 SSL Setup

Certbot container auto-generates and renews certificates.  
Make sure ports 80/443 are free during initial challenge.

```bash
docker compose run certbot certonly --standalone \
  -d stream-mowaxuk.hopto.org \
  --email your@email.com --agree-tos --no-eff-email
```

## 🔒 Basic Auth

Set credentials via `.htpasswd` or NGINX config.  
Only authenticated users can access the stream portal.

## 🧱 Reverse Proxy (Optional)

Deploy a second NGINX container to terminate HTTPS and route traffic:

```nginx
location /stream/ {
  proxy_pass http://rtmp-container:8080/;
  auth_basic "Restricted";
  auth_basic_user_file /etc/nginx/.htpasswd;
}
```

## 🧠 Reproducibility

This stack is built for clarity and handoff:
- Modular configs
- Dockerized deployment
- Public documentation
- Swagger baked in

## 🧾 Attribution

Built by [**Wayne**](https://github.com/mowaxuk)  
Gateshead’s own encrypted broadcaster and telemetry architect.
