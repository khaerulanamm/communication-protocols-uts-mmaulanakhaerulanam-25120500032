# Request Documentation

## Catatan

Case yang dipilih adalah **Case 7 - Protobuf/gRPC Endpoint**.

Praktikum dilakukan menggunakan **Postman gRPC Client** untuk mengirim request dan **Wireshark** untuk menganalisis traffic jaringan.

Karena komunikasi menggunakan protokol **gRPC** dengan format **Protocol Buffers (Protobuf)** melalui **HTTP/2**, request tidak dijalankan menggunakan command `curl` seperti pada REST API biasa.

### Request yang Diuji

#### GET Proto

Endpoint:
`/api/grpc/proto`

Tujuan:
Menampilkan isi file `.proto` yang digunakan sebagai kontrak komunikasi.

---

#### GET Services

Endpoint:
`/api/grpc/services`

Tujuan:
Menampilkan daftar service dan method yang tersedia.

---

#### Predict

Service:
`demo.inference.InferenceService/Predict`

Tujuan:
Mengirim satu data pelanggan untuk memperoleh hasil prediksi.

---

#### BatchPredict

Service:
`demo.inference.InferenceService/BatchPredict`

Tujuan:
Mengirim banyak data pelanggan dalam satu request.

---

#### HealthCheck

Service:
`demo.inference.InferenceService/HealthCheck`

Tujuan:
Memastikan server gRPC aktif dan siap menerima request.

