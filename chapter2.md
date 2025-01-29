# Data Models and Query Languages

## Bab 2: Model Data dan Bahasa Kueri

### 1. Model Relasional vs Dokumen

**Model Relasional (SQL)**

- **Konsep**: Data diorganisasi dalam tabel dengan baris dan kolom.
- **Kelebihan**:
  - Dukungan kuat untuk _join_ dan hubungan _many-to-many_.
  - Skema terstruktur (_schema-on-write_).
- **Contoh Kasus**: LinkedIn profile dengan tabel terpisah untuk pengguna, pekerjaan, dan pendidikan (Gambar 2-1).

**Model Dokumen (NoSQL)**

- **Konsep**: Data disimpan dalam dokumen terstruktur (JSON/XML) dengan hierarki.
- **Kelebihan**:
  - _Schema-on-read_: Fleksibel untuk data heterogen.
  - Lokalisasi data: Akses cepat untuk dokumen lengkap.
- **Contoh**: Representasi profil LinkedIn dalam JSON (Contoh 2-1).

**Perbandingan**

- **Impedansi Objek-Relasional**: Translasi rumit antara objek aplikasi dan tabel database.
- **Skema**: Relasional (kaku) vs Dokumen (fleksibel).
- **Hubungan**: Dokumen cocok untuk _one-to-many_, relasional lebih baik untuk _many-to-many_.

---

### 2. Model Data Graf

**Kapan Digunakan?**

- Untuk data dengan hubungan kompleks (_many-to-many_), seperti jejaring sosial, rekomendasi, atau sistem navigasi.

**Contoh Query**

- **Cypher (Neo4j)**:
  ```cypher
  MATCH (person)-[:BORN_IN]->()-[:WITHIN*0..]->(us:Location {name:'United States'})
  RETURN person.name
  ```
- **SPARQL (Triple-Store)**:
  ```sparql
  SELECT ?personName WHERE {
    ?person :bornIn / :within* / :name "United States".
  }
  ```

**Kelebihan**:

- Menyimpan entitas beragam (orang, lokasi, event) dalam satu struktur.
- Traversal hubungan kompleks lebih efisien.

---

### 3. Bahasa Kueri: Deklaratif vs Imperatif

**Deklaratif (SQL, Cypher)**

- **Ciri**: Menentukan _apa_ yang dibutuhkan, bukan _cara_ mencapainya.
- **Contoh**:
  ```sql
  SELECT * FROM animals WHERE family = 'Sharks';
  ```
- **Manfaat**: Optimasi otomatis oleh database, paralelisasi mudah.

**Imperatif (Kode JavaScript)**

- **Ciri**: Langkah eksplisit untuk pengambilan data.
- **Contoh**: Loop untuk filter data secara manual.

**MapReduce**

- Hybrid: Logika diproses dengan _map_ (filter) dan _reduce_ (agregasi).
- **Contoh MongoDB**:
  ```javascript
  db.observations.mapReduce(mapFunction, reduceFunction, {
    query: { family: "Sharks" },
  });
  ```

---

### 4. Evolusi Model Data

- **Relasional → NoSQL**: Adopsi JSON (PostgreSQL, MySQL) untuk fleksibilitas.
- **NoSQL → Relasional**: Beberapa database dokumen (MongoDB) menambahkan dukungan operasi _join_.
- **Konvergensi**: Database modern menggabungkan kelebihan kedua model (contoh: Spanner, Cassandra).

---

**Kesimpulan**

- Pilih model berdasarkan kebutuhan:
  - **Dokumen**: Untuk data hierarkis dan _schema-on-read_.
  - **Relasional**: Untuk hubungan kompleks dan konsistensi.
  - **Graf**: Untuk jejaring data yang saling terhubung.
- Bahasa kueri deklaratif (SQL, Cypher) lebih efisien untuk optimasi dan skalabilitas.
