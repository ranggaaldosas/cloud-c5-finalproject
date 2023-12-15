# Laporan Final Project-c5-finalproject

## Authors

| Nama                                                         | NRP        | Task          |
| ------------------------------------------------------------ | ---------- | ------------- |
| [Keisya Nabila](https://www.github.com/keisyanabila)         | 5027211058 | Worker        |
| [Rangga Aldo](https://www.github.com/ranggaaldosas)          | 5027211059 | Database      |
| [Adiba Zalfa](https://www.github.com/dibazalfa)              | 502721160  | Worker        |
| [Tarisha Icha](https://www.github.com/tarishaicha)           | 502721161  | Worker        |
| [Annisa Ghina](https://www.github.com/anisaghinasalsabila)   | 502721162  | Worker        |
| [Dzakirozaan Uzlah Wasata](https://www.github.com/dibazalfa) | 502721166  | Load Balancer |
| [Athaya Rayhan](https://www.github.com/reyhanqb)             | 502721167  | Load Balancer |

---

## 1. Permasalahan

Anda adalah seorang lulusan Teknologi Informasi, sebagai ahli IT, salah satu kemampuan yang harus dimiliki adalah Kemampuan merancang, membangun, mengelola aplikasi berbasis komputer menggunakan layanan awan untuk memenuhi kebutuhan organisasi.(menurut kurikulum IT ITS 2023 😙)

Pada suatu saat teman anda ingin mengajak anda memulai bisnis di bidang digital marketing, anda diberikan sebuah aplikasi berbasis API File: app.py dengan spesifikasi sebagai berikut.

Kemudian anda diminta untuk mendesain arsitektur cloud yang sesuai dengan kebutuhan aplikasi tersebut. Apabila dana maksimal yang diberikan adalah 1 juta rupiah per bulan (65 US$) konfigurasi cloud terbaik seperti apa yang bisa dibuat?

## Rancangan Arsitektur dan Tabel Harga Spesifikasi VM

- Berikut adalah rancangan arsitektur yang telah kami buat untuk final project kami.

  Terdapat 3 rancangan arsitektur yang kami buat:

  1. Database dan Worker

  ![Screenshot 2023-12-15 140515](https://github.com/anisaghinasalsabila/pemrograman-integratif/assets/71119774/dc0ef4b6-842f-4ef8-8495-b8b41dbe9645)

  2. Database, Worker 1, Worker 2, dan Load Balancer (Costum Droplet)

  ![Screenshot 2023-12-15 140610](https://github.com/anisaghinasalsabila/pemrograman-integratif/assets/71119774/439ab4da-2dfe-4b2d-962b-7d876cb24398)

  3. Database, Worker 1, Worker 2, dan Load Balancer (Digital Ocean)

  ![Screenshot 2023-12-15 140715](https://github.com/anisaghinasalsabila/pemrograman-integratif/assets/71119774/61a54b9a-ea38-4379-a2d7-5c95dfbfc93d)

- Kami memilih untuk menggunakan Digital Ocean sebagai lingkungan cloud yang akan kami gunakan. Berikut adalah tabel harga spesifikasi VM yang kami buat <br>

  ![Screenshot 2023-12-14 230921](https://github.com/anisaghinasalsabila/pemrograman-integratif/assets/71119774/ddac15e6-6d78-4025-ab05-7d078e95e0eb)

## Langkah Implementasi dan Konfigurasi Teknologi

### Setup Database

klik tombol create dan pilih yang databases

<img width="363" alt="Untitled" src="https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107627453/07bf63c7-b699-4bb6-8a55-3c1c7d92d94a">

kemudian pilih datacenter terdekat, disini kami pilih singapura dan untuk database enginenya kami pilih mongodb

<img width="1280" alt="Untitled 1" src="https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107627453/a7e7cc6b-4e10-4280-bcad-96646a13ab6d">

selanjutnya kita select budget sesuai dengan rancangan arsitekturnya yaitu $15

<img width="421" alt="Untitled 2" src="https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107627453/7a635393-28fe-4ce2-9156-2a4b1d934d2a">

Selanjutnya klik Create Database Cluster. Lalu masukkan IP Worker dan masukkan IP laptop yang digunakan untuk mengakses. Untuk mengecek IP laptop bisa menggunakan link berikut [https://whatismyipaddress.com/](https://whatismyipaddress.com/)

Masukkan pada restricted inbound connections seperti berikut

<img width="1000" alt="Untitled 3" src="https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107627453/a2164faf-9e04-48f3-a2e0-5a0f61258f2a">

Lalu pada connection details ganti settingan pada connection string dan klik copy

<img width="462" alt="Untitled 4" src="https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107627453/0a8760b4-221e-4994-ad30-116854a1e815">

Jangan lupa untuk mengganti <replace-with-your-password> dengan password yang didapatkan saat membuat database. Kemudian install mongo DBCompass pada link berikut [https://www.mongodb.com/products/tools/compass](https://www.mongodb.com/products/tools/compass) . Setelah selesai instalasi, bukalah mongoDB compass dan buatlah new connection. Kemudian, masukkan connection string beserta password yang sudah kita copy tadi seperti berikut dan klik connect.

<img width="601" alt="Untitled 5" src="https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107627453/870d209d-f78f-4970-93ab-66b1fa30dd21">

Jangan lupa masukkan nama database (myDatabases) dan nama collection (orders_db) Apabila sudah database akan tersimpan seperti berikut

![Untitled 6](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107627453/998623c4-4a63-4815-808d-a407186b9394)

Terakhir, untuk menggunakan connection string untuk worker database yang sebelumnya admin bisa diubah dengan myDatabases yang sudah dibuat sebelumnya

<img width="455" alt="Untitled 7" src="https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107627453/14a796a0-50ce-4a15-a420-111cbc88db86">

## Hasil Pengujian Setiap Endpoint

1. Get All Orders
   ![WhatsApp Image 2023-12-15 at 12 05 40 AM](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107459188/24b8b371-f645-42d9-b258-f860334701c4)

2. Get a Specific Orders by ID
   ![WhatsApp Image 2023-12-15 at 12 06 25 AM](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107459188/3ee7e35d-7df9-4ea0-9d58-e01b1f1e1947)

3. Create a New Order
   ![WhatsApp Image 2023-12-15 at 12 07 01 AM](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107459188/f5d0d0bc-99df-49bd-ba5d-151993529b44)

4. Update an Order by ID
   ![WhatsApp Image 2023-12-15 at 12 07 33 AM](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107459188/c81ce927-6fd7-420c-aec7-6e3783fa2ad2)

5. Delete an Order by ID
   ![WhatsApp Image 2023-12-15 at 12 08 04 AM](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/107459188/06451e4d-245e-4fc6-a3b2-5eb8b871fb3a)

## Hasil Pengujian dan Analisis Loadtesting Locust

Berikut ini merupakan hasil dari 3 rancangan arsitektur kelompok kami

<p align="center">
    <img src="https://i.ibb.co/bXd5DF0/Screenshot-20.png" width=500 length=500>

Hasil terbaik didapatkan oleh rancangan arsitektur pertama yaitu

<p align="center">
    <img src="https://i.ibb.co/LSrpW85/Screenshot-21.png" width=500 length=500>

Berikut ini adalah hasil screenshot dari testing arsitektur pertama

1. Endpoint /order

- RPS Maksimum (load testing 60 detik)
- Peak Concurrency Maksimum (spawn rate 25, load testing 60 detik)
<p align="center">
    <img src="https://i.ibb.co/kyrXyFJ/sr-25.jpg" width=480 length=200>

- Peak Concurrency Maksimum (spawn rate 50, load testing 60 detik)
<p align="center">
    <img src="https://i.ibb.co/8rjk3nn/sr-50.jpg" width=480 length=200>

- Peak Concurrency Maksimum (spawn rate 100, load testing 60 detik)
<p align="center">
    <img src="https://i.ibb.co/PDGv5Vg/sr-100.jpg" width=480 length=200>

## Kesimpulan dan Saran

- Setelah melakukan perbandingan harga digital ocean dan azure, harga untuk digital ocean lebih murah
- Setelah percobaan yang kami lakukan berulang kali dengan menggunakan 3 topologi yang berbeda, kita mendapat kesimpulan:

a.) Topologi 1
menggunakan worker yang spesifikasinya sangat tinggi sehingga dapat menangani request user yang banyak

b.) Topologi 2
menggunakan load balancer custom dapat mudah untuk melakukan config yang dimana dapat meningkatkan performa rps, tetapi dari kelompok kami mendapat kendala kurangnya config untuk menghilangkan cache atau meningkatkan performa pada load balancer sehingga dari uji coba kelompok kami mendapat banyak failure ketika Concurrency tinggi walaupun rps terbilang cukup bagus

c.) Topologi 3
menggunakan load balancer milik vendor digital ocean lebih mudah untuk digunakan tetapi sulit untuk meningkatkan performa karena tidak dapat diconfig melalui ssh, dan juga jika ingin meningkatkan performa kita perlu mengeluarkan biaya tambahan. Untuk hasil uji coba kita mendapatkan rps yang lebih stabil dan mendapat 0 failure untuk keseluruhan percobaan (1000-2000 Concurrency)

Kesimpulan
Dilihat dari data yang didapat, jika dilihat dari performa untuk yang lebih baik adalah topologi 1, tetapi jika dilihat dari environment yang lebih sehat, stabil, dan pada umumnya digunakan adalah topologi 3

Saran
jumlah load balancer sebaiknya sama dengan jumlah worker karena ketika kami mencoba menggunakan 1 load balancer dan 3 worker terjadi down pada ketiga worker tersebut
![down](https://i.ibb.co/0C4Mzhz/image.png)
