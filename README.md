# ProjectKomdat
Tugas Projek sesi UTS mata kuliah Komdat kelompok 4, Dapat diakses di http://34.101.90.55:8008/

Masuk dengan akun guest:
- Guest Editor : guest1@gmail.com | Guest1--
- Guest Read Only : guest2@gmail.com | Guest2--

![image](https://github.com/aamilham/ProjectKomdat/assets/88355248/bee3c882-415f-49e9-acbc-f9379bfd2551)

# Aplikasi Web Leantime

<h1 align="center"> <img src="Img/leantime-logo.png"> </h1>

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:|:---:

# Sekilas Tentang

Leantime adalah **strategic open source projet management** yang berfokus untuk membantu perusahaan dan tim yang ingin membuat project management dari awal hingga akhir. Leantime dibuat untuk non-project manager, Leantime menggabungkan perencanaan serta pekerjaan sekaligus sehingga mudah diakses dan digunakan oleh semua orang dalam tim. Leantime merupakan alternatif serta gabungan dari ClickUp, Monday, Asana, dan Trello.


# Instalasi

## Kebutuhan Sistem
- PHP 8.0+
- Web Server (Kami menggunakan Google Cloud Virtual Machine)
- MySQL 5.7+

## Langkah Instalasi

### 1. Login kedalam server menggunakan ssh
```
ssh komdatkel4@34.101.90.55
```

### 2. Instalasi terbagi 2, pertama instan menggunakan docker compose dan template yang sudah disediakan, dan yang kedua menggunakan docker run serta manual untuk mengatur databasenya

#### Cara Pertama menggunakan docker compose
```
git clone https://github.com/Leantime/docker-leantime.git
cd docker-leantime
cp sample.env .env
```
buka file .env untuk mengatur konfigurasi Leantime
```
nano .env
```
disini kita bisa mengubah pengaturan database & container

![config env](Img/config-env.png)

lalu build
```
docker compose up --build
```
jika terdapat masalah tidak bisa menyambung kedalam database lakukan
```
docker compose down -v
```
![no connection database](Img/no-connect-database.png) <br />
lalu build kembali

#### Cara kedua menggunakan docker run
buat network agar leantime dapat tersambung dengan container MySQL
```
docker network create leantime-net
```
buatlah database MySQL, ubahlah sesuai yang diinginkan
```
docker run -d --restart unless-stopped -p 3306:3306 --network leantime-net \
-e MYSQL_ROOT_PASSWORD=321.qwerty \
-e MYSQL_DATABASE=leantime \
-e MYSQL_USER=admin \
-e MYSQL_PASSWORD=321.qwerty \
--name mysql_leantime mysql:8.0 --character-set-server=UTF8MB4 --collation-server=UTF8MB4_unicode_ci
```
buatlah container untuk leantime
```
docker run -d --restart unless-stopped -p 80:80 --network leantime-net \
-e LEAN_DB_HOST=mysql_leantime \
-e LEAN_DB_USER=admin \
-e LEAN_DB_PASSWORD=321.qwerty \
-e LEAN_DB_DATABASE=leantime \
--name leantime leantime/leantime:latest
```
jalankan instalasi dengan `domain.com/install`


### 3. Pengaturan port yang diinginkan
ubah isi dari docker-compose.yml
```
nano docker-compose.yml
```
- ganti ports pada bagian leantime menjadi yang diinginkan, semisalnya **"8008:80"** atau "80:80" <br />
- buat ports pada bagian services, masukkan **"3306:3006"** agar memastikan database tersambung <br />

![ports](Img/ports.png)

### 4. Instalasi WebApp
saat kita membuka web pertama kali, yang akan muncul adalah instalasi untuk akun dari admin <br />
silahkan isi sesuai yang diinginkan, setelahnya akan diarahkan kedalam page login dan semua instalasi telah **selesai** <br />

![install](Img/instalasi.png)


# Konfigurasi

Setting server tambahan yang diperlukan untuk meningkatkan fungsi dan kinerja aplikasi, misalnya:
- batas upload file
- batas memori
- dll

Plugin untuk fungsi tambahan
- login dengan Google/Facebook
- editor Markdown
- dll

Config tambahan seperti sitename, bahasa, dan timezone
- Config dapat dilakukan dengan mengubah isi dari .env yang telah di copy sebelumnya
  ```
  nano .env
  ```

  ![config additional](Img/config-additional.png)

SMTP Config
- Leantime mensupport pengiriman email menggunakan SMTP, cukup ubah pada .env
  ```
  nano .env
  ```

  ![config smtp](Img/config-smtp.png)

Create Account untuk user lain
- As admin, pergi kedalam opsi user management, disini kita bisa melihat semua user, mengatur semuanya, dan mendaftarkan yang baru

  ![user management](Img/user-management.png)

- Pilih add user dan setting user baru sesuai yang diinginkan, serta role sang user

  ![add user](Img/add-user.png)

- Akan ada invitation link yang berisikan pengaturan password untuk akun baru

  ![create acc](Img/create-acc.png)

#  Maintenance (opsional)

Setting tambahan untuk maintenance secara periodik, misalnya:
- buat backup database tiap pekan
- hapus direktori sampah tiap hari
- dll


# Otomatisasi
- Hidupkan server menggunakan docker
  ```
  docker-compose -d
  ```
- Matikan server yang sedang berjalan
  ```
  docker-compose down
  ```


# Cara Pemakaian
Penggunaan **PS Leantime** sangat simpel, karena aplikasi ini dilengkapi dengan antarmuka yang sederhana dan mudah dipahami. Berikut ini untuk penjelasan lebih lanjut:

1. Sebelum menggunakan Leantime, kita harus login pada halaman login Leantime
   
   ![Login Page](https://github.com/aamilham/ProjectKomdat/assets/88355248/bee3c882-415f-49e9-acbc-f9379bfd2551)

2. Setelah login, kita akan masuk ke halaman **Home**. Di sini kita bisa melihat To-Dos, Kalender, dan Project kita.  
   
   ![Home Page](Img/home.png)
   
1. Menu **Project Overview/Dasboard** blablabla

   isi gambar disini
   
3. Menu **Make** blablabla

   a. **Fitur To Dos** blablabla
   
   b. **Fitur Goals** blablabla
  

   isi gambar disini
   
5. Menu **Think** blablabla
  
   a. **Fitur Ideas** blablabla

   b. **Fitur Blueprints** blablabla

   c. **Fitur Retrospectives** blablabla
   
   isi gambar disini
   
8. Menu **Data ROOM** blablabla
   
   a. **Fitur Docs** blablabla

   b. **Fitur Files** blablabla

   c. **Fitur Reports** blablabla

   isi gambar disini

3. Pada bagian pojok kanan atas, terdapat beberapa fitur yang dapat kita gunakan. **Fitur My Project** digunakan untuk melihat project apa saja yang kita miliki

   ![My Project Page](Img/myproject.png)

4. Fitur **Notification** digunakan untuk melihat notifikasi dan mention yang masuk

   ![Notification Page](Img/notification.png)
   
5. Fitur **Company**. Pada fitur ini, terdapat beberapa pilihan yaitu All Timesheets berguna untuk melihat keseluruhan waktu/jam yang sudah digunakan, All Projects berguna untuk melihat keseluruhan project yang
   ada, All client berguna untuk melihat nama klien, dan User Management berguna untuk melihat ada berapa user atau pengguna website Leantime

   ![Company Page](Img/company.png)

6. Fitur **My Profile**. Pada fitur ini kita dapat melihat account settings berupa informasi profil, keamanan, look and feel, dan notification

   ![Profile Page](Img/profile.png)
   
- Tampilan aplikasi web
- Fungsi-fungsi utama
- Isi dengan data real/dummy (jangan kosongan) dan sertakan beberapa screenshot


# Pembahasan

Leantime sebagai alat yang dirancang untuk mengelola proyek dengan lebih efektif dan efisien, memiliki beberapa kelebihan dan kekurangan sebagai berikut
  
  **Kelebihan**
  1. Antarmuka pengguna yang ramah
     - Leantime memiliki antar pengguna yang bersih dan mudah digunakan sehingga memudahkan pengguna baru dalam menggunakan aplikasi ini.
       

  
- Bandingkan dengan aplikasi web lain yang sejenis


## Referensi


1. [About Leantime](https://leantime.io/) - Website Leantime
2. [Trello](https://trello.com/) - Website Trello
3. [Zoho](https://projects.zoho.com/) - Website Zoho Projects 
4. [Saasworthy](https://www.saasworthy.com/compare/trello-vs-openproject-vs-leantime?pIds=146,2507,2592) - Compare between Trello and Leantime
5. [Sourceforget](https://sourceforge.net/software/compare/ClickUp-vs-Leantime-vs-Zoho-Projects/) - Compare between Zoho and Leantime
