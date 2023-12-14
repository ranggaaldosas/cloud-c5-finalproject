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
1. Buat database dan copy connection string
![database]()

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
