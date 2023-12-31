# Laporan Final Project-c5-finalproject

## Authors

| Nama                                                         | NRP        | Task          |
| ------------------------------------------------------------ | ---------- | ------------- |
| [Keisya Nabila](https://www.github.com/keisyanabila)         | 5027211058 | Worker        |
| [Rangga Aldo](https://www.github.com/ranggaaldosas)          | 5027211059 | Database      |
| [Adiba Zalfa](https://www.github.com/dibazalfa)              | 502721160  | Worker        |
| [Tarisha Icha](https://www.github.com/tarishaicha)           | 502721161  | Worker        |
| [Anisa Ghina](https://www.github.com/anisaghinasalsabila)   | 502721162  | Worker        |
| [Dzakirozaan Uzlah Wasata](https://www.github.com/dibazalfa) | 502721166  | Load Balancer |
| [Athaya Reyhan](https://www.github.com/reyhanqb)             | 502721167  | Load Balancer |

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

### Set Up Worker

Pada digital ocean, klik tombol create dan pilih droplets

![WhatsApp Image 2023-12-15 at 13 11 31_83e71d96](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/5c44c5b2-99e3-4fc7-9ca8-6eb515c40f2f)

Region yang dipilih adalah Singapura karena merupakan negara terdekat

![WhatsApp Image 2023-12-15 at 13 14 04_ececae17](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/ce15fae6-6079-41b9-a31b-5c1266958e6c)

Kemudian, pilih Image. Image yang kami gunakan adalah Ubuntu versi 22.04 (LTS) x64

![WhatsApp Image 2023-12-15 at 13 14 16_0ffa9122](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/3daed0a5-c9cd-4e5d-a004-4893b086da83)

Selanjutnya, pilih Size. Di sini, kami menentukan Droplet Type dan CPU untuk droplet yang akan dijadikan worker. Sesuai dengan rancangan, kami memilih droplet dengan spesifikasi 2GB/2CPUs seharga $12

![WhatsApp Image 2023-12-15 at 14 06 52_c02f7135](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/5b919633-6daa-4705-9c55-4d21e75183e8)

Untuk authentication mode, kami memilih menggunakan password

![WhatsApp Image 2023-12-15 at 13 19 36_c0ee6351](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/1c881d72-16ea-418a-82e5-ad390619b15d)

Terakhir, beri nama droplet dan tekan tombol Create Droplet untuk membuat droplet

![WhatsApp Image 2023-12-15 at 14 06 10_55785b63](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/b40358da-0337-4d5b-985b-6405bfc9b709)

Masuk ke droplet yang sudah dibuat melalui SSH
`root@178.128.88.111`

Kemudian masukkan password yang tadi sudah dibuat

![WhatsApp Image 2023-12-15 at 13 56 00_3bdbc203](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/c5c8dfcb-3f00-436f-9640-65e203225898)

Jika sudah masuk, lakukan langkah-langkah berikut untuk melakukan set-up worker pada droplet

`nano setup-worker.sh`

Masukkan code berikut pada file `setup-worker.sh`

```
#!/bin/bash

sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt-cache policy docker-ce
sudo apt install docker-ce -y
sudo systemctl status docker

mkdir worker1
cd worker1

echo 'FROM python:3.9-slim
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:8000", "app:app"]
' > Dockerfile

echo 'version: '3.1'

services:
  worker1:
    build: /root/worker1
    restart: always
    ports:
      - "8080:8000"
' > docker-compose.yml

echo 'fastapi==0.78.0
uvicorn==0.18.2
pymongo
pydantic
uuid
Flask
Flask-PyMongo
gunicorn
' > requirements.txt

echo 'from flask import Flask, jsonify, request
from flask_pymongo import PyMongo
from bson import ObjectId

app = Flask(__name__)

# Configuration for MongoDB
app.config['MONGO_URI'] = 'mongodb+srv://doadmin:<password>@db-mongodb-sgp1-55072-cf745936.mongo.ondigitalocean.com/myDatabases?replicaSet=db-mongodb-sgp1-55072&tls=true&authSource=admin'
mongo = PyMongo(app)

# Routes

# Get all orders
@app.route('/orders', methods=['GET'])
def get_orders():
    orders = mongo.db.orders.find()
    orders_list = []
    for order in orders:
        order['_id'] = str(order['_id'])  # Convert ObjectId to string
        orders_list.append(order)
    return jsonify({"orders": orders_list})

# Get a specific order by ID
@app.route('/orders/<string:order_id>', methods=['GET'])
def get_order(order_id):
    order = mongo.db.orders.find_one({'_id': ObjectId(order_id)})
    if order:
        order['_id'] = str(order['_id'])  # Convert ObjectId to string
        return jsonify({"order": order})
    else:
        return jsonify({"message": "Order not found"}), 404

# Create a new order
@app.route('/orders', methods=['POST'])
def create_order():
    data = request.json
    new_order = {
        'product': data['product'],
        'quantity': data['quantity'],
        'customer_name': data['customer_name'],
        'customer_address': data['customer_address']
    }
    result = mongo.db.orders.insert_one(new_order)
    new_order['_id'] = str(result.inserted_id)  # Convert ObjectId to string
    return jsonify({"message": "Order created successfully", "order": new_order})

# Update an order by ID
@app.route('/orders/<string:order_id>', methods=['PUT'])
def update_order(order_id):
    data = request.json
    updated_order = {
        'product': data.get('product'),
        'quantity': data.get('quantity'),
        'customer_name': data.get('customer_name'),
        'customer_address': data.get('customer_address')
    }
    mongo.db.orders.update_one({'_id': ObjectId(order_id)}, {'$set': updated_order})
    updated_order['_id'] = order_id
    return jsonify({"message": "Order updated successfully", "order": updated_order})

# Delete an order by ID
@app.route('/orders/<string:order_id>', methods=['DELETE'])
def delete_order(order_id):
    result = mongo.db.orders.delete_one({'_id': ObjectId(order_id)})
    if result.deleted_count > 0:
        return jsonify({"message": "Order deleted successfully"})
    else:
        return jsonify({"message": "Order not found"}), 404

if __name__ == '__main__':
    app.run(debug=True)
' > app.py

cd /root
```

Kemudian, pada direktori root jalankan command

`chmod +x worker-setup.sh`

`./worker-setup.sh`

Setelah command dijalankan, worker akan ter set up hanya saja belum dijalankan. Worker akan dijalankan menggunakan docker dengan command berikut

(command dijalankan pada direktori worker1)

`cd worker1`

Membuat docker images :
`docker build -t worker1-app -f Dockerfile .`

Menjalankan container :
`docker run -p 8000:8000 -d worker1-app`

Kita bisa melihat apakah worker sudah berhasil berjalan melalui command
`docker ps` Jika berhasil, maka akan keluar seperti berikut

![WhatsApp Image 2023-12-15 at 13 46 07_e316005a](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/7dce9f46-9513-4634-acf2-974372e17ee0)

Untuk memeriksa apakah worker sudah berjalan di IP, port, dan endpoint yang sesuai, kita bisa mengeceknya melalui Insomnia/Postman

Di sini, kami memeriksa menggunakan endpoint GET /orders

![WhatsApp Image 2023-12-15 at 14 05 29_b517e646](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/025fbc28-c0d5-459b-803d-df8135a87393)

Lakukan hal yang sama pada droplet lain untuk mengsetup worker, jangan lupa untuk menyesuaikan nama sesuai kebutuhan.

### Set Up LoadBalancer

### Spesifikasi

Load balancer kami buat dengan menggunakan image Ubuntu 23.10 dan memiliki spesifikasi 1 CPU, 1 GB Memory, dan 25 GB SSD. Pricing yang dimiliki load balancer kami ada di angka 6 dolar.

### Konfigurasi

1. Pertama-tama klik tombol Create pada navbar Digital Ocean dan pilih menu Load Balancer.

2. Kemudian, pilih region sesuai dengan region kita saat ini.

![Screenshot 2023-12-15 011745](https://github.com/reyhanqb/Jarkom-IT09-2023/assets/107137535/74db4e10-fa6d-4b5c-b38c-080abc726787)

3. Lalu sesuaikan jumlah droplet yang ingin terhubung ke Load Balancer. Pada arsitektur yang kami buat, kami menggunakan 2 worker.

![Screenshot 2023-12-15 011947](https://github.com/reyhanqb/Jarkom-IT09-2023/assets/107137535/19f29c14-42d5-4167-af69-e08b11e87af0)

4. Setelah itu atur forwarding rules untuk melakukan konfigurasi port dari Load Balancer menuju ke 2 worker. Disini kami menggunakan port 8000 untuk keduanya.

![Screenshot 2023-12-15 012235](https://github.com/reyhanqb/Jarkom-IT09-2023/assets/107137535/dd1488be-084f-4a7a-a130-85d9ddc345ef)

5. Terakhir berikan nama yang sesuai untuk Load Balancer yang ingin kita buat, kemudian klik Create untuk membuat Load Balancer.

![Screenshot 2023-12-15 012415](https://github.com/reyhanqb/Jarkom-IT09-2023/assets/107137535/4c1d07b2-0fe4-4817-a2a7-71a58af1ce5a)

---

Setelah Load Balancer berhasil dibuat, kita dapat mengakses dashboard Load Balancer untuk melihat status droplet yang terhubung ke Load Balancer kita. Apabila Load Balancer sudah berjalan dan tidak ada masalah pada kedua node, maka harusnya health check di dashboard bernilai 100%.

![Screenshot 2023-12-15 012711](https://github.com/reyhanqb/Jarkom-IT09-2023/assets/107137535/33996ea1-1765-473e-90bb-bf3e70e7e28a)

## Konfigurasi Load Balancer Nginx

## Spesifikasi

Load balancer kami buat dengan menggunakan image Ubuntu 23.10 dan memiliki spesifikasi 1 CPU, 1 GB Memory, dan 25 GB SSD. Pricing yang dimiliki load balancer kami ada di angka 6 dolar.

## Konfigurasi

Load balancer kami menggunakan nginx. Pertama-tama, lakukan ```sudo apt-get update``` dan lakukan instalasi nginx dengan menjalankan command ```sudo apt-get install nginx -y```. 

Setelah berhasil, buatlah konfigurasi nginx untuk membuat load balancer. Konfigurasi nginx kami adalah sebagai berikut:

```
upstream app {
    server 178.128.88.111:8000;
    server 139.59.243.183:8000;
}

server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://app;
    }
}
```

Konfigurasi kami buat di direktori 
```/etc/nginx/sites-enabled``` dengan cara melakukan symlink dengan command ```sudo ln -s /etc/nginx/sites-available/loadbalancer /etc/nginx/sites-enabled/```. 

![Screenshot 2023-12-15 005928](https://github.com/reyhanqb/Jarkom-IT09-2023/assets/107137535/105dcab0-f22f-45e9-bc66-1beb114c97b0)

Selanjutnya, restart service nginx dan pastikan nginx sudah berjalan dengan menjalankan command ```sudo service nginx status```.

![Screenshot 2023-12-15 010221](https://github.com/reyhanqb/Jarkom-IT09-2023/assets/107137535/338af52f-08bd-4e35-a490-9d2862e0af78)

## Hasil Pengujian Load Balancer Nginx

Peak concurrency maksimum (spawn rate 25, rps 60 detik)

![WhatsApp Image 2023-12-14 at 4 56 44 PM](https://github.com/reyhanqb/Jarkom-IT09-2023/assets/107137535/0cf86902-0d2b-415f-804f-635cd5ccb093)


--
Peak concurrency maksimum (spawn rate 25, rps 60 detik)

![WhatsApp Image 2023-12-13 at 11 13 37 AM](https://github.com/reyhanqb/Jarkom-IT09-2023/assets/107137535/898e7f28-7291-411f-a5c8-641b7998d1fc)

## Analisis

Didapatkan RPS yang lebih tinggi ketika menggunakan load balancer buatan kami sendiri menggunakan Nginx. Namun, setelah beberapa kali testing seringkali RPS yang tinggi juga diikuti dengan tingkat failures sebesar 5-9 persen. Apabila dibandingkan dengan Load Balancer dari Digital Ocean, Load Balancer Nginx memiliki potensi untuk menghandle request yang jauh lebih besar dengan harga yang lebih fleksibel, namun tidak lebih konsisten dibandingkan dengan Load Balancer dari Digital Ocean

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
    <img src="https://i.ibb.co/gjHT8bt/Screenshot-22.png">

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
