# Analisis Encoding dan Response

## 1. Case yang Dipilih

Case 7 - Protobuf/gRPC Endpoint (Komparasi Struktur Message dengan JSON)

Praktikum ini berfokus pada implementasi komunikasi menggunakan gRPC dan Protocol Buffers (Protobuf). Pengujian dilakukan terhadap beberapa method pada service InferenceService untuk memahami struktur request, response, serta mekanisme komunikasi HTTP/2.

---

## 2. Format Data yang Digunakan

Format data yang digunakan adalah Protocol Buffers (Protobuf).

Pada sisi client, data dapat ditulis dalam format JSON melalui Postman, namun saat dikirim ke server gRPC data akan dikonversi menjadi format biner Protobuf. Format ini lebih ringkas dan efisien dibandingkan JSON sehingga cocok digunakan pada komunikasi antar microservices.

---

## 3. Analisis Request GET

### GET 01

Endpoint: `/api/grpc/proto`

Tujuan Request:
Menampilkan isi file kontrak `.proto` yang digunakan sebagai definisi service dan message pada gRPC.

Status Code:
200 OK

Analisis Response:
Response menampilkan struktur file Protocol Buffers yang berisi package, service, method RPC, request message, dan response message. File ini berfungsi sebagai kontrak komunikasi antara client dan server agar format data yang digunakan tetap konsisten.

---

### GET 02

Endpoint: `/api/grpc/services`

Tujuan Request:
Menampilkan daftar service dan method yang tersedia pada server gRPC.

Status Code:
200 OK

Analisis Response:
Response berisi informasi service `InferenceService` beserta method yang dapat dipanggil, yaitu Predict, BatchPredict, dan HealthCheck. Informasi ini membantu client mengetahui fungsi yang tersedia pada server.

---

## 4. Analisis Request POST

### POST 01 (Predict)

Endpoint:
`demo.inference.InferenceService/Predict`

Tujuan Request:
Mengirim satu data pelanggan untuk mendapatkan hasil prediksi dari model.

Request Body:

```json
{
  "customer_id": "C1024",
  "features": {
    "avg_order_value": 250000,
    "monthly_orders": 15
  }
}
```

Analisis:

* `customer_id` bertipe string.
* `avg_order_value` bertipe numeric/double.
* `monthly_orders` bertipe integer.
* Method Predict hanya memproses satu pelanggan dalam satu request.
* Response berisi skor prediksi, label pelanggan, dan versi model yang digunakan.

---

### POST 02 (BatchPredict)

Endpoint:
`demo.inference.InferenceService/BatchPredict`

Tujuan Request:
Mengirim banyak data pelanggan sekaligus dalam satu request.

Request Body:

```json
{
  "items": [
    {
      "customer_id": "C1001",
      "features": {
        "avg_order_value": 150000,
        "monthly_orders": 10
      }
    }
  ]
}
```

Analisis:

* Data dikirim dalam bentuk array (`items`).
* Setiap item memiliki struktur yang sama dengan method Predict.
* BatchPredict lebih efisien dibandingkan mengirim banyak request Predict secara terpisah.
* Response berisi kumpulan hasil prediksi untuk seluruh pelanggan yang dikirim.

---

## 5. Analisis Header

Header Penting:

```http
content-type: application/grpc
```

Makna:

Header ini menunjukkan bahwa komunikasi menggunakan protokol gRPC dan payload dikirim dalam format biner Protocol Buffers melalui HTTP/2. Berbeda dengan REST API yang umumnya menggunakan `application/json`.

Header lain yang ditemukan:

* `:authority`
* `grpc-status`

Header tersebut digunakan untuk identifikasi server tujuan dan status eksekusi gRPC.

---

## 6. Analisis Status Code

### grpc-status: 0 (OK)

Menunjukkan request berhasil diproses tanpa error.

### grpc-status selain 0

Menunjukkan adanya kesalahan pada request, validasi data, atau masalah komunikasi antara client dan server.

Pada seluruh pengujian yang dilakukan, server memberikan status:

```text
grpc-status: 0
```

yang berarti seluruh request berhasil dijalankan.

---

## 7. Kesimpulan

Melalui praktikum ini saya memahami bahwa gRPC menggunakan Protocol Buffers sebagai format komunikasi yang lebih efisien dibandingkan JSON. Penggunaan HTTP/2 memungkinkan proses pertukaran data berlangsung lebih cepat dengan koneksi yang tetap aktif. Method Predict digunakan untuk memproses satu data pelanggan, sedangkan BatchPredict dapat memproses banyak data sekaligus dalam satu request. Selain itu, file `.proto` berperan penting sebagai kontrak komunikasi yang memastikan struktur data antara client dan server tetap konsisten. Praktikum ini memberikan pemahaman tentang bagaimana gRPC digunakan pada arsitektur microservices modern.

