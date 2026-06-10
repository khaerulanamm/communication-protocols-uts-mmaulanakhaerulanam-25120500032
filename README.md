# UTS Communication Protocols 

## 📋 Identitas Mahasiswa

| Keterangan    | Detail                                                                  |
| ------------- | ----------------------------------------------------------------------- |
| Nama          | M. Maulana Khaerul Anam                                                 |
| NIM           | 25120500032                                                             |
| Kelas         | Profesional                                                             |
| Program Studi | Sains Data                                                              |
| Mata Kuliah   | Communication Protocols                                                 |
| Judul Case    | Case 7 - Protobuf/gRPC Endpoint: Komparasi Struktur Message dengan JSON |

---

## 📖 Deskripsi Singkat

Praktikum berfokus pada implementasi dan analisis komunikasi berbasis **gRPC (Google Remote Procedure Call)** yang menggunakan **Protocol Buffers (Protobuf)** sebagai format serialisasi data. Pengujian dilakukan menggunakan Postman dan Wireshark untuk menganalisis request, response, metadata HTTP/2, serta struktur payload yang dikirimkan antara client dan server.

Tujuan utama praktikum adalah memahami bagaimana gRPC bekerja sebagai alternatif REST API yang lebih efisien untuk komunikasi antar layanan (microservices).

---

## 🎯 Case yang Dipilih

**Case 7 – Protobuf/gRPC Endpoint**

### Service yang Digunakan

```proto
service InferenceService {
  rpc Predict (PredictionRequest) returns (PredictionReply);
  rpc BatchPredict (BatchPredictionRequest) returns (BatchPredictionReply);
  rpc HealthCheck (HealthCheckRequest) returns (HealthCheckReply);
}
```

---

## 🔄 Daftar Request yang Diuji

### 1. GET Proto Definition

Menampilkan isi file `.proto` yang digunakan sebagai kontrak komunikasi antara client dan server.

**Endpoint:**

```http
GET /api/grpc/proto
```

**Output:**

* Struktur service
* Message request
* Message response
* Definisi kontrak Protobuf

---

### 2. GET Services

Menampilkan daftar service dan method gRPC yang tersedia.

**Endpoint:**

```http
GET /api/grpc/services
```

**Output:**

* Daftar service
* Daftar RPC method
* Informasi endpoint yang tersedia

---

### 3. Predict (Unary RPC) > Method

Mengirimkan satu data pelanggan dan menerima satu hasil prediksi.

### 4. BatchPredict (Bulk Request) > Method

Mengirimkan banyak data pelanggan dalam satu request.

### 5. HealthCheck > Method

Memastikan server gRPC dalam kondisi aktif dan siap menerima request.

## 📂 Struktur Repository

README
UTS Communication Protocols
📋 Identitas Mahasiswa
Keterangan	Detail
Nama	M. Maulana Khaerul Anam
NIM	25120500032
Kelas	Profesional
Program Studi	Sains Data
Mata Kuliah	Communication Protocols
Judul Case	Case 7 - Protobuf/gRPC Endpoint: Komparasi Struktur Message dengan JSON
📖 Deskripsi Singkat
Praktikum berfokus pada implementasi dan analisis komunikasi berbasis gRPC (Google Remote Procedure Call) yang menggunakan Protocol Buffers (Protobuf) sebagai format serialisasi data. Pengujian dilakukan menggunakan Postman dan Wireshark untuk menganalisis request, response, metadata HTTP/2, serta struktur payload yang dikirimkan antara client dan server.

Tujuan utama praktikum adalah memahami bagaimana gRPC bekerja sebagai alternatif REST API yang lebih efisien untuk komunikasi antar layanan (microservices).

🎯 Case yang Dipilih
Case 7 – Protobuf/gRPC Endpoint

Service yang Digunakan
service InferenceService {
  rpc Predict (PredictionRequest) returns (PredictionReply);
  rpc BatchPredict (BatchPredictionRequest) returns (BatchPredictionReply);
  rpc HealthCheck (HealthCheckRequest) returns (HealthCheckReply);
}
🔄 Daftar Request yang Diuji
1. GET Proto Definition
Menampilkan isi file .proto yang digunakan sebagai kontrak komunikasi antara client dan server.

Endpoint:

GET /api/grpc/proto
Output:

Struktur service
Message request
Message response
Definisi kontrak Protobuf
2. GET Services
Menampilkan daftar service dan method gRPC yang tersedia.

Endpoint:

GET /api/grpc/services
Output:

Daftar service
Daftar RPC method
Informasi endpoint yang tersedia
3. Predict (Unary RPC) > Method
Mengirimkan satu data pelanggan dan menerima satu hasil prediksi.

4. BatchPredict (Bulk Request) > Method
Mengirimkan banyak data pelanggan dalam satu request.

5. HealthCheck > Method
Memastikan server gRPC dalam kondisi aktif dan siap menerima request.

📂 Struktur Repository
UTS-Communication-Protocols/
│
├── requests/
│   ├── grpc-postman-collection.json
│   └── curl-command.md
│
├── evidence/
│   ├── get_proto.png
│   ├── get_services.png
│   ├── predict.png
│   ├── batch_predict.png
│   ├── health_check.png
│   ├── wireshark_request.png
│   └── wireshark_response.png
│
├── analysis/
│   ├── encoding-analysis.md
│   ├── postman_analysis.md
│   └── wireshark_analysis.md
│
├── report/
│   ├── UTS_CommProtocol_Laporan_Anam.pdf
│   └── UTS_CommProtocol_PPT_Anam.pdf
│
└── README.md

---

## 📌 Kesimpulan

1. gRPC menggunakan Protocol Buffers (.proto) sebagai kontrak komunikasi antara client dan server.
2. Payload dikirim dalam format binary sehingga lebih efisien dibanding JSON.
3. HTTP/2 memungkinkan multiplexing dan persistent connection yang meningkatkan performa komunikasi.
4. Method Predict digunakan untuk satu data pelanggan, sedangkan BatchPredict digunakan untuk banyak data sekaligus.
5. HealthCheck digunakan untuk memverifikasi status layanan gRPC.
6. Berdasarkan hasil pengujian, seluruh method berhasil dieksekusi dengan status `grpc-status: 0 (OK)`.

---

**Author:** M. Maulana Khaerul Anam
**Course:** Communication Protocols
**Semester:** 2
**Program Studi:** Sains Data
---

## 📌 Kesimpulan

1. gRPC menggunakan Protocol Buffers (.proto) sebagai kontrak komunikasi antara client dan server.
2. Payload dikirim dalam format binary sehingga lebih efisien dibanding JSON.
3. HTTP/2 memungkinkan multiplexing dan persistent connection yang meningkatkan performa komunikasi.
4. Method Predict digunakan untuk satu data pelanggan, sedangkan BatchPredict digunakan untuk banyak data sekaligus.
5. HealthCheck digunakan untuk memverifikasi status layanan gRPC.
6. Berdasarkan hasil pengujian, seluruh method berhasil dieksekusi dengan status `grpc-status: 0 (OK)`.

---
## Tools yang Digunakan

- Postman (gRPC Client)
- Wireshark
- Protocol Buffers (Protobuf)
- gRPC
- HTTP/2
- Git & GitHub

---
**Author:** M. Maulana Khaerul Anam
**Course:** Communication Protocols
**Semester:** 2
**Program Studi:** Sains Data
