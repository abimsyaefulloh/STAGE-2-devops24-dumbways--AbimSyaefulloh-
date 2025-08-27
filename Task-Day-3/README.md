```bash
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
```

# Langkah-Langkah Pengerjaan Tugas Docker
## Step 1 — Login ke Server
```bash
# Login ke server BiznetGio menggunakan SSH key yang sudah kita share untuk sesama:
ssh -i ~/.ssh/dumbways.pem dumbways@<IP-SERVER>

# Update server:
sudo apt update && sudo apt upgrade -y
```

---

## Step 2 — Clone Wayshub dari Github dan Arsitektur Server
### Clone Wayshub dari Github
```bash
# frontend
https://github.com/dumbwaysdev/wayshub-frontend
# backend
https://github.com/dumbwaysdev/wayshub-backend
```
### Arsitektur Server
```bash
Arsitektur Server
Server Abim (kamu): frontend + gateway (Nginx reverse proxy).
Server Tanu: backend + database (MySQL).

DNS:
batch24.studentdumbways.my.id → server Abim.
api.batch24.studentdumbways.my.id → server Tanu.
```

---

Step 2 — Install Docker & Menjalankan Docker Compose











