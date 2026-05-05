# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question: Bagaimana perbandingan kinerja YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia berdasarkan nilai confidence pada citra dari video CCTV?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
| Jenis metode (YOLOv2, YOLOv3) | IV   | Algoritma deteksi objek | Kategori metode yang digunakan | Nominal |   -   | Menentukan model yang dipakai saat proses deteksi  |  Karena penelitian memang membandingkan dua metode berbeda |
| Hasil deteksi manusia | DV | Kemampuan model dalam mendeteksi dan menghitung jumlah manusia | Nilai confidence (tingkat keyakinan deteksi) dan jumlah manusia yang terdeteksi | Ratio | Confidence (0–1), jumlah (orang) | Mengambil output dari sistem deteksi YOLO pada setiap frame | Confidence menunjukkan tingkat keyakinan model terhadap objek yang terdeteksi, sedangkan jumlah objek menunjukkan hasil perhitungan manusia yang terdeteksi secara langsung |
| Kondisi input (citra CCTV yang sama) | CV | Konsistensi data uji | Menggunakan data uji yang sama untuk kedua metode agar hasil perbandingan tidak dipengaruhi perbedaan input | Nominal | - | Menggunakan dataset yang sama untuk YOLOv2 dan YOLOv3 | Supaya perbandingan adil dan tidak bias |

Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [✅] Setiap langkah terdokumentasi
  [✅] Tidak ada "lompatan logis"
  [✅] Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Bagaimana perbandingan kinerja YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia berdasarkan nilai confidence pada citra dari video CCTV?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
| Jenis metode | IV | Algoritma deteksi | YOLOv2 dan YOLOv3 | Nominal | — |
| Hasil deteksi manusia | DV | Performa deteksi dan perhitungan jumlah manusia | Confidence (tingkat keyakinan deteksi) dan jumlah manusia terdeteksi | Ratio | Nilai dan jumlah |
| Kondisi input | CV | Konsistensi data uji | Citra CCTV yang sama | Nominal | - |

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [✅] Tidak
> Jika ya, di mana? Tidak ada, semua masih nyambung dari metode sampai hasil.

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 4 | Confidence dan jumlah objek sudah mewakili kemampuan sistem dalam mendeteksi dan menghitung manusia |
| Sensitive      | 4 | Perubahan kecil pada performa model dapat terlihat dari perbedaan nilai confidence dan jumlah objek yang terdeteksi |
| Feasible       | 5 | Data mudah didapat langsung dari output sistem YOLO |

**Apakah perlu secondary metric?** [✅] Ya / [ ] Tidak
> Jika ya, apa dan mengapa?  Bisa ditambahkan waktu proses (processing time), karena selain akurasi, kecepatan juga penting dalam sistem deteksi real-time.
**Contoh kasus ceiling effect untuk metrik ini:**
> Jika nilai confidence dari kedua metode sudah sama-sama tinggi (misalnya mendekati 0,9 atau 1), maka akan sulit melihat perbedaan performa secara jelas karena keduanya terlihat sama-sama baik.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | Apakah semua data terkumpul? | Tidak semua frame dari video mungkin berhasil diproses atau terdeteksi dengan baik | Pastikan semua frame diproses dan lakukan pengecekan ulang pada data yang hilang |
| Consistency | Apakah ada kontradiksi? | Bisa terjadi perbedaan hasil deteksi pada frame yang berbeda walaupun objek sama | Gunakan kondisi pengujian yang sama dan parameter model yang konsisten |
| Validity | Apakah mengukur yang dimaksud? | Ya, karena data diambil langsung dari output sistem deteksi YOLO sesuai dengan tujuan penelitian | Gunakan parameter dan threshold yang sesuai agar hasil deteksi lebih akurat |
| Representativeness | Apakah mewakili kondisi nyata? | Terbatas pada video tertentu sehingga belum mewakili semua kondisi lingkungan | Gunakan variasi data dari berbagai kondisi jika memungkinkan |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data dianggap p-hacking karena bisa membuat hasil terlihat lebih baik dari yang sebenarnya. Misalnya kita memilih metrik yang paling menguntungkan setelah melihat hasil, bukan dari awal. 

> Berbeda dengan eksplorasi data, eksplorasi dilakukan untuk memahami data tanpa mengubah tujuan awal penelitian. Jadi eksplorasi masih boleh, tapi tidak boleh mengganti metrik utama setelah hasil terlihat.

