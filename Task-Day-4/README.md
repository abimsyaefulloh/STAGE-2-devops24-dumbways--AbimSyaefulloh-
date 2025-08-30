```bash
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
