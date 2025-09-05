```bash
Task:
- Dengan mendaftar akun free tier AWS/GCP/Azure,
buatlah Infrastructre dengan terraform menggunakan registry yang sudah ada.
dengan beberapa aturan berikut :
   - Buatlah 2 buah server dengan OS ubuntu 24 dan debian 11 (Untuk spec menyesuaikan)
   - attach vpc ke dalam server tersebut
   - attach ip static ke vm yang telah kalian buat
   - pasang firewall ke dalam server kalian dengan rule {allow all ip(0.0.0.0/0)}
   - buatlah 2 block storage di dalam terraform kalian,
     lalu attach block storage tersebut ke dalam server yang ingin kalian buat.
     (pasang 1 ke server ubuntu dan  1 di server debian)
   - test ssh ke server
- Buat terraform code kalian serapi mungkin
 - simpan script kalian ke dalam github dengan format tree sebagai berikut:
```sh
  Automation  
  |  
  | Terraform
  └─|  └── gcp
          │ └── main.tf
          │ └── providers.tf
          │ └── etc
          ├── aws
          │ └── main.tf
          │ └── providers.tf
          │ └── etc
          ├── azure
          │ └── main.tf
          │ └── providers.tf
          │ └── etc

Reference :
[Amazon Web Services (AWS)](https://aws.amazon.com/free/)
[Google Cloud Platform (GCP)](https://cloud.google.com/free)
[Microsoft Azure](https://azure.microsoft.com/en-us/pricing/free-services)
```
Tentu! Berikut saya buatkan langkah-langkah pengerjaan tugas Day 5 (Terraform) dan Day 6 (Ansible) secara terpisah tanpa kode, sesuai permintaanmu.

---

## Langkah-langkah Tugas Day 5 - Terraform (Infrastruktur Cloud)

1. **Persiapan Akun Cloud**  
   - Daftar akun free tier di AWS, GCP, atau Azure  
   - Siapkan kredensial akses (API key, secret, service account) untuk Terraform

2. **Setup Project dan Struktur Folder**  
   - Buat folder `Automation/Terraform/<provider>` (misal `aws`, `gcp`, atau `azure`)  
   - Siapkan file konfigurasi utama seperti `main.tf`, `providers.tf`, dan folder `etc` jika diperlukan

3. **Definisikan Provider Terraform**  
   - Konfigurasi provider cloud yang dipilih dengan kredensial dan region

4. **Buat Resource VPC dan Network**  
   - Definisikan VPC (Virtual Private Cloud) untuk jaringan server  
   - Buat subnet dan konfigurasi jaringan lain jika perlu

5. **Provision Server VM**  
   - Buat 2 VM:  
     - 1 dengan OS Ubuntu 24  
     - 1 dengan OS Debian 11  
   - Sesuaikan spesifikasi VM sesuai kebutuhan

6. **Assign IP Static ke VM**  
   - Buat dan attach IP static (Elastic IP atau equivalent) ke masing-masing VM

7. **Setup Firewall Rules**  
   - Buat aturan firewall yang mengizinkan akses dari semua IP (0.0.0.0/0)  
   - Attach firewall ke VM atau subnet sesuai provider

8. **Buat dan Attach Block Storage**  
   - Buat 2 block storage terpisah  
   - Attach 1 block storage ke VM Ubuntu  
   - Attach 1 block storage ke VM Debian

9. **Inisialisasi dan Deploy Terraform**  
   - Jalankan `terraform init` untuk inisialisasi  
   - Jalankan `terraform plan` untuk melihat rencana provisioning  
   - Jalankan `terraform apply` untuk membuat resource di cloud

10. **Testing dan Verifikasi**  
    - Coba SSH ke kedua server menggunakan IP static yang sudah dibuat  
    - Pastikan server berjalan dan storage sudah terpasang

11. **Dokumentasi dan Commit**  
    - Dokumentasikan langkah dan konfigurasi di `README.md`  
    - Commit dan push seluruh file Terraform ke GitHub dengan struktur folder yang sudah ditentukan

---
