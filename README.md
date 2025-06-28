
# ♻ Node.js data consumption project (microservice pattern)

ini adalah proyek demo yang mengilustrasikan arsitektur microservice sederhana menggunakan Node.js. Terdapat satu layanan utama (API Gateway) yang bertugas mengonsumsi data dari dua layanan independen (`Order Service` dan `User Service`) dan menggabungkannya menjadi satu respons tunggal.


## 🔴Arsitektur Proyek
Proyek ini terdiri dari 3 layanan yang berjalan secara terpisah:

**1.`server.js` (API Gateway / Aggregator Service)**

- Teknologi: `Hapi.js` dan `got`.

- Port: `3000`.

- Tugas: Bertindak sebagai pintu masuk utama (**entrypoint**). Ketika menerima permintaan dengan `id`, layanan ini akan memanggil `Order Service` dan `User Service` secara bersamaan, lalu menggabungkan hasilnya.

**2.`order-service.js` (Order Service)**

- Teknologi: *Node.js (modul http bawaan)*.

- Port: `4000` (diasumsikan).

- Tugas: Menyediakan data pesanan (menu) berdasarkan `id`. Ini adalah layanan mandiri yang tidak bergantung pada layanan lain.

**`user-service.js` (User Service)**

- Teknologi: *Node.js (modul http bawaan)*.

- Port: `5000` (diasumsikan).

- Tugas: Menyediakan data pengguna berdasarkan `id`. Sama seperti `Order Service`, ini adalah layanan mandiri.


## 🟢Tech Stack

- [Node.js](https://nodejs.org/en/download): Lingkungan eksekusi JavaScript.

- [@hapi/hapi](https://hapi.dev/resources/changelog/): Framework untuk membangun API Gateway yang andal dan terstruktur.

- [got](https://www.npmjs.com/package/got/v/9.6.0): Library modern untuk membuat permintaan HTTP, digunakan untuk komunikasi antar-service.


## 🟣Installation

- Pastikan Anda telah menginstal Node.js versi terbaru.

- Clone repository ini atau buka folder proyek Anda.

- Install semua dependencies yang dibutuhkan:

```bash
  npm install
```


## 🟡Running Tests

Karena ini adalah arsitektur microservice, Anda harus menjalankan ketiga server secara bersamaan di terminal yang terpisah.

**Langkah 1: Jalankan Order Service**

- Buka terminal pertama dan jalankan perintah berikut untuk memulai `Order-Service.js` pada port 4000:
```bash
  npm run start:Order
```
- Anda akan melihat log: `Order service listening on localhost on port: 4000`

**Langkah 2: Jalankan User Service**

- Buka terminal kedua dan jalankan `User-Service.js` pada port 5000.

```bash
npm run start:User
```
- Anda akan melihat log: `User service listening on localhost on port: 5000`

**Langkah 3: Jalankan API Gateway Utama**

Buka terminal ketiga dan jalankan server utama:
```bash
npm run start
```
- Anda akan melihat log: `Server berjalan pada http://localhost:3000`

**Sekarang semua layanan sudah berjalan dan siap digunakan.**



## 🔰Documentation API

#### Semua permintaan harus ditujukan ke API Gateway (http://localhost:3000).

**Mengambil Data Gabungan Pengguna dan Pesanan**

Endpoint ini mengambil `id`, memanggil `Order Service` dan `User Service` dengan `id` tersebut, lalu menggabungkan hasilnya.

- URL: `/:id`

- Method: `GET`

- Deskripsi: Mengembalikan data menu pesanan dan nama pengguna berdasarkan `ID` yang diberikan.

```Bash
  curl -X GET http://localhost:3000/1
```
#### Contoh Respons Sukses (200 OK):
```JSON
{
  "id": 1,
  "menu": "Mie Goreng",
  "user": "John Doe"
}
```
#### Contoh Respons Error (404 Not Found):
Jika Anda meminta dengan `id=3`, `Order Service` akan mengembalikan 404, yang kemudian ditangani oleh API Gateway.
```Bash
curl -X GET http://localhost:3000/3
```
#### Respons:
```JSON
{
    "message": "not found"
}
```


## License

[MIT](https://choosealicense.com/licenses/mit/)
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)



## 👷‍♂Authors

- [@wijayakusuma](https://)

