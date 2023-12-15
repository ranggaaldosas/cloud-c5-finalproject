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
- Berikut adalah rancangan arsitektur yang telah kami buat untuk final project kami.
  
  Terdapat 3 rancangan arsitektur yang kami buat:
  1. Database dan Worker

     ![WhatsApp Image 2023-12-15 at 13 42 25](https://github.com/anisaghinasalsabila/pemrograman-integratif/assets/71119774/fc243b87-3da4-4585-b601-15f706f0eaf2)
  3. Database, Worker 1, Worker 2, dan Load Balancer (Costum Droplet)

     ![Screenshot 2023-12-15 135959](https://github.com/anisaghinasalsabila/pemrograman-integratif/assets/71119774/851413a1-9fc2-4025-b54d-83eca06eae92)
  5. Database, Worker 1, Worker 2, dan Load Balancer (Digital Ocean)

     ![WhatsApp Image 2023-12-15 at 13 46 01](https://github.com/anisaghinasalsabila/pemrograman-integratif/assets/71119774/5ac18c2a-ef2a-42f3-9b57-285f38ab13a3)
     
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
   
### Set Up Worker

Pada digital ocean, klik tombol create dan pilih droplets
![WhatsApp Image 2023-12-15 at 13 11 31_83e71d96](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/5c44c5b2-99e3-4fc7-9ca8-6eb515c40f2f)

Region yang dipilih adalah Singapura karena merupakan negara terdekat 
![WhatsApp Image 2023-12-15 at 13 14 04_ececae17](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/ce15fae6-6079-41b9-a31b-5c1266958e6c)

Kemudian, pilih Image. Image yang kami gunakan adalah Ubuntu versi 22.04 (LTS) x64 
![WhatsApp Image 2023-12-15 at 13 14 16_0ffa9122](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/3daed0a5-c9cd-4e5d-a004-4893b086da83)

Selanjutnya, pilih Size. Di sini, kami menentukan Droplet Type dan CPU untuk droplet yang akan dijadikan worker. Sesuai dengan rancangan,  kami memilih droplet dengan spesifikasi 2GB/2CPUs seharga $18
![WhatsApp Image 2023-12-15 at 13 16 46_4d5067d8](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/66c37080-095f-4fdd-b629-280de5031a4a)

Untuk authentication mode, kami memilih menggunakan password
![WhatsApp Image 2023-12-15 at 13 19 36_c0ee6351](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/1c881d72-16ea-418a-82e5-ad390619b15d)

Terakhir, beri nama droplet dan tekan tombol Create Droplet untuk membuat droplet
![WhatsApp Image 2023-12-15 at 13 55 01_ee6e41b1](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/3d5a0992-cfc0-4a0f-bb19-f7de1a316598)

Masuk ke droplet yang sudah dibuat melalui SSH
```root@178.128.88.111```

Kemudian masukkan password yang tadi sudah dibuat
![WhatsApp Image 2023-12-15 at 13 56 00_3bdbc203](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/c5c8dfcb-3f00-436f-9640-65e203225898)

Jika sudah masuk, lakukan langkah-langkah berikut untuk melakukan set-up worker pada droplet

```nano setup-worker.sh```

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
app.config['MONGO_URI'] = 'mongodb+srv://doadmin:c74HW9J20y1vmz35@db-mongodb-sgp1-55072-cf745936.mongo.ondigitalocean.com/myDatabases?replicaSet=db-mongodb-sgp1-55072&tls=true&authSource=admin'
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

```chmod +x worker-setup.sh```

```./worker-setup.sh```

Setelah command dijalankan, worker akan ter set up hanya saja belum dijalankan. Worker akan dijalankan menggunakan docker dengan command berikut

(command dijalankan pada direktori worker1)

```cd worker1```

Membuat docker images :
```docker build -t worker1-app -f Dockerfile .```

Menjalankan container : 
```docker run -p 8000:8000 -d worker1-app```

Kita bisa melihat apakah worker sudah berhasil berjalan melalui command
```docker ps``` Jika berhasil, maka akan keluar seperti berikut
![WhatsApp Image 2023-12-15 at 13 46 07_e316005a](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/7dce9f46-9513-4634-acf2-974372e17ee0)

Untuk memeriksa apakah worker sudah berjalan di IP, port, dan endpoint yang sesuai, kita bisa mengeceknya melalui Insomnia/Postman

Di sini, kami memeriksa menggunakan endpoint GET /orders
![WhatsApp Image 2023-12-15 at 13 47 05_e326853a](https://github.com/ranggaaldosas/cloud-c5-finalproject/assets/103043684/0f8d5b38-1106-4c44-bd4c-ede06de20ab1)

Lakukan hal yang sama pada droplet lain untuk mengsetup worker, jangan lupa untuk menyesuaikan nama sesuai kebutuhan.

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
