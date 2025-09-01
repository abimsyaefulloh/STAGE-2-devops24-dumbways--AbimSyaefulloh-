```bash
TUGAS :
Sebelum mengerjakan tugas, mohon persiapkan :
- Akun Github dan buat repository dengan judul "devops24-dumbways-<nama kalian>"
- Gunakan file README.md untuk isi tugas kalian
- Buatlah langkah-langkah pengerjaan tugas beserta dokumentasinya

Gunakan vm Appserver kalian diskusikan saja ingin menggunakan vm siapa di dalam team.

Repository & Reference:
[Wayshub Backend](https://github.com/dumbwaysdev/wayshub-backend)
[Wayshub Frontend](https://github.com/dumbwaysdev/wayshub-frontend)
[Certbot](https://certbot.eff.org/instructions?ws=nginx&os=ubuntufocal)
[PM2 Runtime With Docker](https://pm2.keymetrics.io/docs/usage/docker-pm2-nodejs)
[Cloudflare](https://dash.cloudflare.com/0d0e2eb306a3b985375cf565cb4ce3fc/studentdumbways.my.id/dns/records)


Tasks :
[ Docker ]
- Rebuild ulang server BiznetGio kalian, lalu gunakan username "dumbways" yang kalian gunakan bersama,
  pastikan menggunakan login melalui ssh-key dan bukan password. (1 key untuk semua akan menjadi bonus) 
- Deploy aplikasi Web Server, Frontend, Backend, serta Database on top `docker compose`
  - Di dalam docker-compose file buat suatu custom network dengan nama **team kalian**,
    lalu pasang ke setiap service yang kalian miliki. (Nilai Bonus)
  - Untuk Web Server buatlah configurasi reverse-proxy menggunakan nginx on top docker.
    - **SSL CLOUDFLARE OFF!!!**
    - SSL sebisa mungkin gunakan wildcard
    - Untuk DNS bisa sesuaikan seperti contoh di bawah ini
      - Frontend team.studentdumbways.my.id
      - Backend api.team.studentdumbways.my.id
  - Push image ke docker registry kalian masing".
- Aplikasi dapat berjalan dengan sesuai seperti melakukan login/register.
b

# Langkah-Langkah Pengerjaan Tugas Docker
## Step 1 — Login ke Server
```bash
# Login ke server BiznetGio menggunakan SSH key yang sudah kita share untuk sesama:
ssh -i ~/.ssh/dumbways.pem dumbways@<IP-SERVER>

# Update server:
sudo apt update && sudo apt upgrade -y
```

---

## Step 1 — Arsitektur Server, Login ke Server, dan Clone Wayshub dari Github
### Arsitektur Server
```bash
# Arsitektur Server
NAMA TEAM : Batch24
Abim :
- Gateway : Reverse Proxy nginx
- Abim22 (app server 1) : frontend, backend, databases dan docker
Mas Tanu :
- tanu96 (app server 2) : CI/CD Jenkins

Domain :
batch24.studentdumbways.my.id
api.batch24.studentdumbways.my.id
```

### Login ke Server menggunakan 1 kunci ssh
- Menambahkan kunci ssh
![Fotoscr](scr/Foto-0.png)

### Clone Wayshub dari Github
```bash
# frontend
https://github.com/dumbwaysdev/wayshub-frontend
# backend
https://github.com/dumbwaysdev/wayshub-backend
```

---

## Step 2 — Install Docker & Menjalankan Docker Compose

### Install Docker melalui website docker nya
`https://docs.docker.com/engine/install/ubuntu/`
![Fotoscr](scr/Foto-1.png)  
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=$(dpkg --print-architecture)] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y

# Cek versi
docker --version
docker compose version

```

### Set up Preparation
- Set up Docker Compose  
  `docker-compose.yml`  
![Fotoscr](scr/Foto-2.png)  
- Set up Dockerfile di frontend  
![Fotoscr](scr/Foto-3.png)  
- Set up Dockerfile di backend  
![Fotoscr](scr/Foto-4.png)  
- Set up api.js di frontend  
![Fotoscr](scr/Foto-5.png)  
- Set up config.js di backend  
![Fotoscr](scr/Foto-6.png)  

### Menjalankan Docker Compose 
1. Menjalankan docker compose build di directory dumbways-app  
  `docker compose build`

2. Menjalankan docker compose up -d  
  `docker compose up -d`

3. Melihat container dan images yang sudah dibuat
  - container  
  `docker ps -a`
![Fotoscr](scr/Foto-7.png)   
  - images  
  `docker images`  
![Fotoscr](scr/Foto-8.png)  

5. melihat logs untuk monitoring container
  `docker compose logs`  
![Fotoscr](scr/Foto-9-0.png)   
![Fotoscr](scr/Foto-9-1.png) 

7. membuka databases di container
`docker compose exec mysql mysql -uabim -pdumbways`  
![Fotoscr](scr/Foto-10.png) 

```bash
# dokumentasi command docker
# 🔹 Build images
docker compose build                # build semua service
docker compose build backend        # build service backend saja
docker compose build --no-cache     # rebuild tanpa cache

# 🔹 Jalankan & stop container
docker compose up -d                # start semua service (detached mode)
docker compose up -d backend        # start backend saja
docker compose down                 # stop semua service & hapus network

# 🔹 Cek status & logs
docker compose ps                   # lihat container yg jalan
docker compose logs -f backend      # lihat log backend realtime
docker compose logs -f frontend     # lihat log frontend realtime
docker compose logs -f mysql        # lihat log mysql realtime

# 🔹 Masuk ke dalam container
docker compose exec backend sh      # masuk shell container backend
docker compose exec mysql bash      # masuk shell container mysql

# 🔹 Migrasi & seeder (pastikan sequelize-cli sudah terinstall)
docker compose exec backend sequelize db:migrate      # jalankan migrasi
docker compose exec backend sequelize db:seed:all     # jalankan semua seeder

# 🔹 Akses MySQL dari container
docker compose exec mysql mysql -uabim -pdumbways 
docker compose exec mysql mysql -uabim -pdumbways -e "SHOW DATABASES;"
docker compose exec mysql mysql -uabim -pdumbways wayshub -e "SHOW TABLES;"

# 🔹 Container & images housekeeping
docker ps -a                         # semua container (jalan & berhenti)
docker images                        # semua image
docker rm -f <container_id>          # hapus container
docker rmi <image_id>                # hapus image
docker image prune                   # hapus dangling images (<none>)

```
## Step 3 — Test di Browser
![Fotoscr](scr/Foto-11.png) 

![Fotoscr](scr/Foto-12.png) 

![Fotoscr](scr/Foto-13.png) 

![Fotoscr](scr/Foto-14.png) 


# CATATAN :

## Daftar HTTPS pake Certbot
![Fotoscr](scr/Certbot-1.png) 

## 1. Install Certbot
```bash
sudo apt update
sudo snap install --classic certbot

# membuat link binary
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
---

## 2. Wizard Certbot
```bash
sudo certbot --nginx
# menambahkan email untuk notifikasi
 ```
---
 
## 3. Generate Sertifikat HTTPS
```bash
sudo certbot --nginx -d batch24.studentdumbways.my.id
```
---

## 4. Cek Sertifikat

Kalau berhasil, coba buka:
```bash
https://batch24.studentdumbways.my.id
```

Terus tes validasi:
```bash
sudo certbot certificates
```


