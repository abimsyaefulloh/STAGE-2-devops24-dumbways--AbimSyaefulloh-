# devops24-dumbways-`<nama-kalian>`{=html}

## Ringkasan

Implementasi tugas Minggu 2: deploy Wayshub (frontend, backend,
database) di atas Docker Compose dengan reverse-proxy Nginx, SSL
wildcard (Cloudflare OFF), custom network, dan push image ke registry.

## Arsitektur

-   reverse-proxy (Nginx, HTTPS) → frontend (static) & backend (Node.js)
-   database (Postgres/MySQL) → diakses backend
-   custom network: `<nama-tim>-net`

## Prasyarat

-   VM Appserver (Ubuntu), user `dumbways` (SSH key-only)
-   Docker & Docker Compose
-   Cloudflare DNS (DNS only)
-   Let's Encrypt wildcard cert

## Checklist Deliverables

-   [ ] Rebuild VM (hostname/IP, OS, screenshot)
-   [ ] User `dumbways` + SSH key-only login
-   [ ] Docker & Compose terinstal
-   [ ] DNS Cloudflare (DNS only)
-   [ ] Wildcard SSL aktif
-   [ ] Compose dengan custom network
-   [ ] Nginx reverse-proxy ke FE/BE (HTTPS)
-   [ ] Aplikasi bisa register/login
-   [ ] Image dipush ke registry

## Langkah Singkat

1.  Rebuild VM, buat user & ssh key-only
2.  Install Docker & Compose
3.  Konfigurasi DNS (team & api)
4.  Ambil wildcard cert (DNS-01)
5.  Build image frontend/backend
6.  Setup Nginx reverse-proxy + TLS
7.  Jalankan `docker compose up -d --build`
8.  Uji aplikasi & DB
9.  Push image ke registry

## Konfigurasi

### Contoh `nginx.conf`

``` nginx
server {
    listen 80;
    server_name team.studentdumbways.my.id api.team.studentdumbways.my.id;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl http2;
    server_name team.studentdumbways.my.id;

    ssl_certificate /etc/letsencrypt/live/team.studentdumbways.my.id/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/team.studentdumbways.my.id/privkey.pem;

    location / {
        proxy_pass http://frontend:3000;
    }
}

server {
    listen 443 ssl http2;
    server_name api.team.studentdumbways.my.id;

    ssl_certificate /etc/letsencrypt/live/team.studentdumbways.my.id/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/team.studentdumbways.my.id/privkey.pem;

    location / {
        proxy_pass http://backend:5000;
    }
}
```

### Contoh `compose.yml`

``` yaml
services:
  reverse-proxy:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./reverse-proxy/nginx.conf:/etc/nginx/nginx.conf:ro
      - /etc/letsencrypt:/etc/letsencrypt:ro
    depends_on:
      - frontend
      - backend
    networks:
      - team-net

  frontend:
    build: ./frontend
    expose:
      - "3000"
    networks:
      - team-net

  backend:
    build: ./backend
    expose:
      - "5000"
    networks:
      - team-net

  db:
    image: postgres:15-alpine
    expose:
      - "5432"
    networks:
      - team-net

networks:
  team-net:
    driver: bridge
```
