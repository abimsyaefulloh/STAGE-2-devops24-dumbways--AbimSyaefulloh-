```bash
TUGAS :
Sebelum mengerjakan tugas, mohon persiapkan :
- Akun Github dan buat repository dengan judul "devops24-dumbways-<nama kalian>"
- Gunakan file README.md untuk isi tugas kalian
- Buatlah langkah-langkah pengerjaan tugas beserta dokumentasinya

Repository & Reference:
[Jenkins Installation](https://www.jenkins.io/doc/book/installing/)
[wget spider](https://www.labnol.org/software/wget-command-examples/28750/)


Tasks :
[ Jenkins ]
- Reverse Proxy Jenkins
  - gunakan domain ex. pipeline-team.studentdumbways.my.id
- Buatlah beberapa Job untuk aplikasi kalian
  - Job Frontend
  - Job Backend
- Buat Jenkinsfile dengan proses seperti ini :
     - Pull dari repository
     - Dockerize/Build aplikasi kita
     - Test application
     - Deploy aplikasi on top Docker
     - Push ke Docker Hub
- Auto trigger setiap ada perubahan di SCM (setiap repository berubah, otomatis menjalankan build)
```
# Insatall Jenkins di App Server 2
### Membuat direktori jenkins dan Insatall jenkins lewat dokumntasi di github  
`https://github.com/jenkinsci/docker/blob/master/README.md`  
![Fotoscr](scr/Foto-01.png)
`docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 --restart=on-failure jenkins/jenkins:lts-jdk17`  
Ini akan menjalankan Jenkins dalam mode terpisah dengan penerusan porta dan penambahan volume.  
Anda dapat mengakses log dengan perintah 'docker logs CONTAINER_ID' untuk memeriksa token login pertama.  
ID kontainer akan dikembalikan dari keluaran perintah di atas.

### Mengecek jenkins yang jalan di container 
![Fotoscr](scr/Foto-0.png)

### Konfigurasi Jenkins
- Unlock Jenkins, masuk ke dalam logs container jenkinsnya untuk melihat passwordnya  
  ![Fotoscr](scr/Foto-1.png)  
  ![Fotoscr](scr/Foto-2.png)  
- Customize Jenkins  
  `select plugin to install` 
  ![Fotoscr](scr/Foto-3.png)
- Organiztion and Adiministration, di centang semua
  ![Fotoscr](scr/Foto-4.png) 
- Build Features, centang bagian SSH Agent 
- Source Code Management, centang bagian Git
  ![Fotoscr](scr/Foto-5.png) 
- Tampilan setup instalasinya
  ![Fotoscr](scr/Foto-6.png)  
- Create First Admin User  
  menggunakan username 
 `admin`  
  dan password jenkins sebelumnya 
  `1953f41f04c04db68faafa8d799605f3`
  ![Fotoscr](scr/Foto-7.png)  
- Instace Configuration,
  untuk mengatur jenkins url bisa menggunakan domain yang sudah terdaftar atau ip address 
  ![Fotoscr](scr/Foto-8.png)  
- Jenkins is ready, 
  ![Fotoscr](scr/Foto-9.png)  
- Login ke Jenkins dan Konfigurasi  
  ![Fotoscr](scr/Foto-10.png)
- Masuk kedalam setting
  ![Fotoscr](scr/Foto-11.png)
- Masuk kekonfigurasi credentials
  ![Fotoscr](scr/Foto-12.png)
- Masuk ke system
  ![Fotoscr](scr/Foto-13.png)
- Masuk ke Global Credential
  ![Fotoscr](scr/Foto-14.png)
- Add Credential
  ![Fotoscr](scr/Foto-15.png)

- Mengisi Username server with private key server
  ![Fotoscr](scr/Foto-17.png)
  ![Fotoscr](scr/Foto-17-1.png)
- Membuat Job baru
  ![Fotoscr](scr/Foto-18.png)
- Memilih project, memilih pipeline
  ![Fotoscr](scr/Foto-19.png)
- Konfigurasi pipeline, menambahkan Github hook trigger (memastikan koneksi github ke jenkins itu aman)
  ![Fotoscr](scr/Foto-20.png)
- Memasukan repositori URL dari github kita  
  ssh private key  
  Mengatur brance  
  Mengatur Sript file sesuai nama di repositori kita  
  ![Fotoscr](scr/Foto-21.png)  
- Stelah selesai mengatur akan muncul table seperti berikut
  ![Fotoscr](scr/Foto-22.png)  

# Hubungkan GitHub → Jenkins (auto trigger)
### sudah ada file Jenkins didirektori 
  ![Fotoscr](scr/Foto-23.png)  
### Pastikan server sudah terhubung ke Github
  ![Fotoscr](scr/Foto-24.png)  
### Push ke Github
```bash
# Inisialisasi git (kalau belum)
git init

# Tambahkan semua file
git add .

# Commit
git commit -m "Initial commit frontend"

# cek remote
git memote -v

# kalau misal mau mengganti remotenya bisa dihapus dulu
git remote remove

# Tambah remote SSH
git remote add origin git@github.com:USERNAME/wayshub-frontend.git

# Push ke branch main
git branch -M main
git push -u origin main
```
### Mengecek Consol Outputnya 
  ![Fotoscr](scr/Foto-25.png)  
  ![Fotoscr](scr/Foto-26.png)  

### 














































