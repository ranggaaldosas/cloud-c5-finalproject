# Laporan Final Project-c5-finalproject

---
## Authors

| Nama                                                | NRP        | Task |
| --------------------------------------------------- | ---------- | ---------- | 
| [Keisya Nabila](https://www.github.com/keisyanabila) | 5027211058 | Worker |
| [Rangga Aldo](https://www.github.com/ranggaaldosas) | 5027211059 | Database |
| [Adiba Zalfa](https://www.github.com/dibazalfa)   | 502721160 | Worker |
| [Tarisha Icha](https://www.github.com/tarishaicha)   | 502721161 | Worker |
| [Annisa Ghina](https://www.github.com/anisaghinasalsabila)   | 502721162 | Worker |
| [Dzakirozaan Uzlah Wasata](https://www.github.com/dibazalfa)   | 502721166 | Load Balancer |
| [Athaya Rayhan](https://www.github.com/reyhanqb)   | 502721167 | Load Balancer |

---
## Permasalahan
Anda adalah seorang lulusan Teknologi Informasi, sebagai ahli IT, salah satu kemampuan yang harus dimiliki adalah Kemampuan merancang, membangun, mengelola aplikasi berbasis komputer menggunakan layanan awan untuk memenuhi kebutuhan organisasi.(menurut kurikulum IT ITS 2023 😙)

Pada suatu saat teman anda ingin mengajak anda memulai bisnis di bidang digital marketing, anda diberikan sebuah aplikasi berbasis API File: app.py dengan spesifikasi sebagai berikut.

Kemudian anda diminta untuk mendesain arsitektur cloud yang sesuai dengan kebutuhan aplikasi tersebut. Apabila dana maksimal yang diberikan adalah 1 juta rupiah per bulan (65 US$) konfigurasi cloud terbaik seperti apa yang bisa dibuat?

## Rancangan Arsitektur dan Tabel Harga Spesifikasi VM
- Berikut adalah rancangan arsitektur yang telah kami buat untuk final project kami
  
![Screenshot 2023-12-14 223353](https://github.com/anisaghinasalsabila/pemrograman-integratif/assets/71119774/4147a39c-5371-4680-9815-163c89d4eb86)
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

2. Create new connection dengan string database yang sudah di-copy sebelumnya
![new connection]()

3. Buat database sesuai dengan variabel yang sudah dibuat di dalam app.py
![database app.py]()

4. Create database baru dengan collection order, add data (import json file)lalu pilih file orders.json yang berisi data-data yang akan dimasukan ke database<br>
![add data]()

5. Run app.py hingga muncul url-nya
![run app.py]()

6. Untuk mengecek database-nya bisa menggunakan postman, request ke url/orders. Jika statusnya sudah 200 ok, maka database sudah bisa berjalan dengan normal
![postman]()

7. Deploy VM untuk worker dengan installasi requirement yang diperlukan di worker
![deploy vm]()

8. Jika tidak ada error, maka worker sudah berjalan

## Hasil Pengujian Setiap Endpoint
1. Get All Orders
![get all orders]()

2. Get a Specific Orders by ID
![get order by id]()

3. Create a New Order
![create]()

4. Update an Order by ID
![update order]()

5. Delete an Order by ID
![delete]()

## Hasil Pengujian dan Analisis Loadtesting Locust
1. Endpoint Get Order
- RPS Maksimum (load testing 60 detik)
- Peak Concurrency Maksimum (spawn rate 25, load testing 60 detik)

- Peak Concurrency Maksimum (spawn rate 50, load testing 60 detik)

- Peak Concurrency Maksimum (spawn rate 100, load testing 60 detik)
![locust get order]()

2. Endpoint Create New Order
- RPS Maksimum (load testing 60 detik)
- Peak Concurrency Maksimum (spawn rate 25, load testing 60 detik)
![locust create new order]()
- Peak Concurrency Maksimum (spawn rate 50, load testing 60 detik)
![post 50]()
- Peak Concurrency Maksimum (spawn rate 100, load testing 60 detik)
![post 100]()

## Kesimpulan dan Saran
- Setelah melakukan pengecekan harga, harga untuk digital ocean lebih murah
- Setelah percobaan yang kami lakukan berulang kali, jumlah load balancer sebaiknya sama dengan jumlah worker karena ketika kami mencoba menggunakan 1 load balancer dan 3 worker terjadi down pada ketiga worker tersebut
![down]()
