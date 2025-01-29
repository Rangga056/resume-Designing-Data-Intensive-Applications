# Reliable, Scalable, and Maintainable Applications

## Bab 1: Aplikasi yang Andal, Skalabel, dan Mudah Dipelihara

### 1. Keandalan (Reliability)

**Definisi**: Sistem tetap berfungsi dengan benar meskipun terjadi gangguan (_fault_).

#### Berbagai Jenis Gangguan:

- **Hardware Faults**  
  Contoh: Kerusakan hardware seperti disk, RAM, atau jaringan.  
  **Solusi**: Redundansi seperti (RAID, _backup power_), toleransi kegagalan perangkat lunak.

- **Software Errors**  
  Contoh: Bug sistematis, _cascading failures_.  
  **Solusi**: Pengujian menyeluruh, isolasi proses, pemantauan, dan _automated recovery_.

- **Human Errors**  
  Contoh: Kesalahan konfigurasi.  
  **Solusi**: Desain antarmuka intuitif, _sandbox environment_ dimana bisa melakukan experiment tanpa mempengaruhi production, dan mekanisme _rollback_ otomatis jika terjadi _failure_.

**Contoh Teknik**:

- _Netflix Chaos Monkey_: Mematikan komponen acak untuk menguji toleransi kesalahan.

---

### 2. Skalabilitas (Scalability)

**Definisi**: Kemampuan sistem untuk dapat menghadapi peningkatan beban secara efisien.

#### Parameter Beban:

- **Contoh Kasus**:
  - _Twitter_ dengan _fan-out load_ (distribusi pengikut per pengguna).
  - Pendekatan _write-heavy_ (cache timeline) vs. _read-heavy_ (query langsung).
  - Pengunaan gabungan dari keduanya yang tergantung dari jumlah follower tiap user unttuk penentuan pendekatan yang dipilih

#### Metrik Kinerja:

- **Response Time**  
  Waktu respon atau delay yang dirasakan langsung oleh end user yang diukur menggunakan **percentil** (p50, p95, p99) untuk mengidentifikasi _tail latency_.  
  Contoh: 99th percentile = 1 detik → 99% permintaan selesai dalam ≤1 detik.
- **Latency**
  Durasi waktu yang diperlukan untuk memproses suatu request.
- **Throughput**  
  Jumlah proses per satuan waktu (_batch processing_). Contoh: Hadoop.

#### Strategi:

- **Scaling Up** (_Vertical_): Menambah kapasitas dari server (CPU, RAM).
- **Scaling Out** (_Horizontal_): Menambah node/ jumlah dari server untuk distribusi beban.

---

### 3. Kemudahan Pemeliharaan (Maintainability)

**Tiga Prinsip Utama**:

1. **Operability**

   - Memudahkan tim operasional dalam pemantauan (_monitoring_), _troubleshooting_, dan pembaruan sistem.
   - Contoh: Otomatisasi deploy, dokumentasi yang jelas dan mudah dimengerti, dan _self-healing_.

2. **Simplicity**

   - Mengurangi kompleksitas dengan **abstraksi** yaitu dengan menghilangkan atau menghapus karakteristik dari suatu objek agar mengurangi kompleksitasnya.
   - Contoh: SQL menyembunyikan kompleksitas struktur penyimpanan data.

3. **Evolvability**
   - Kemampuan adaptasi terhadap perubahan kebutuhan di masa yang akan datang baik dari penambahan atau perubahan use case, regulasi, pertumbuhan sistem dll.
   - Contoh: Migrasi arsitektur Twitter dari query langsung ke cache timeline.

---

### Contoh Integrasi Sistem

- **Arsitektur Gabungan** (Gambar 1-1):  
  Kombinasi database, cache, dan _search index_.
  ![Image](https://github.com/user-attachments/assets/b89f2e53-af74-4eb8-a7e6-5e1fda2ec1ae)
- **Tantangan**: Konsistensi data antar komponen dan _API design_.

---
