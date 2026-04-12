# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (artefak dibuat sebagai instrumen pengujian hipotesis, bukan tujuan akhir).

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Fauzatul Farhanah
Tanggal          : 10 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya:  Apakah data yang digunakan itu data asli atau hanya data buatan?
   - Data yang dibutuhkan untuk verifikasi: Dataset yang digunakan, jumlah data, dan cara pengujian akurasi


2. Posisi paradigma:
   - Pendekatan: [✅] Positivis  [ ] Interpretivis  [✅] Design Science  [ ] Mixed
   - Alasan: Karena penelitian ini menggunakan data dan perhitungan (akurasi, MAE, RMSE), serta membuat sistem rekomendasi sebagai alat untuk diuji.


3. Identifikasi distorsi:
   - Asumsi tersembunyi: Data dummy dianggap cukup mewakili kondisi nyata
   - Sumber bias potensial: Data dibuat sendiri sehingga belum tentu mencerminkan kondisi pengguna sebenarnya
   - Langkah mitigasi: Menggunakan data asli dan melakukan pengujian pada kondisi sebenarnya.


4. Komitmen etika:
   - Data yang tidak akan dimanipulasi:  Nilai hasil eksperimen seperti MAE dan RMSE tidak akan dimanipulasi
   - Batasan yang diakui sejak awal: Data yang digunakan adalah data dummy sehingga hasil mungkin tidak sepenuhnya akurat
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

**Paper yang dipilih:**
> Judul: Peningkatan Akurasi Rekomendasi Dokter pada Kondisi Data Sparsity Menggunakan Algoritma Content-Based Filtering 
> Penulis (Tahun): Alwan Prasetya, Ahsanun Naseh Khudori, Risqy Siwi Pradini (2025)

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Membuat dataset dummy(data buatan) 1.000 dokter dan 500 pasien untuk simulasi| Data tidak berasal dari kondisi nyata, sehingga berpotensi tidak merepresentasikan perilaku pengguna sebenarnya|
| Data → Processing | Melakukan imputasi data kosong menggunakan mean (numerik) dan modus (kategorikal)|Data menjadi tidak asli karena diisi secara perkiraan |
| Processing → Analysis | Menggunakan algoritma Content-Based Filtering dengan cosine similarity berdasarkan 5 atribut | Model hanya melihat beberapa atribut, faktor lain diabaikan |
| Analysis → Inference | Menyimpulkan akurasi meningkat berdasarkan penurunan nilai MAE dan RMSE| Metrik evaluasi hanya berbasis simulasi sehingga belum tentu mencerminkan kepuasan pengguna nyata|
| Inference → Knowledge | Menyimpulkan metode efektif untuk sistem rekomendasi dokter | Hasil belum tentu dapat digeneralisasi ke dunia nyata karena belum diuji pada data real |

**Distorsi paling besar di tahap:** Reality → Data
Karena sejak awal data yang digunakan bukan data asli (menggunakan data  dummy), jadi hasilnya bisa berbeda dengan kondisi yang sebenarnya.

**Dua distorsi spesifik yang teridentifikasi:**
1. Sampling bias (Dataset yang digunakan merupakan data buatan sehingga tidak sepenuhnya mewakili kondisi nyata pengguna dan dokter.)
2. External Validity (Hasil penelitian belum tentu dapat diterapkan di dunia nyata karena tidak diuji menggunakan data asli pengguna.)
---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Peneliti sebaiknya menampilkan hasil dengan dan tanpa outlier supaya tidak menyesatkan|
| Transparansi | Harus dijelaskan alasan kenapa outlier dihapus, misalnya karena ada kesalahan data atau tidak wajar|
| Peer review | Reviewer bisa menolak jika data dihapus tanpa alasan jelas|

**Keputusan akhir dan justifikasi:**
> Data tidak boleh langsung dihapus begitu saja. Outlier boleh dihapus kalau memang ada alasan yang masuk akal (misalnya error). Tapi tetap lebih baik menampilkan dua hasil (dengan dan tanpa outlier) supaya penelitian tetap jujur dan transparan.
---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Sistem rekomendasi dokter menggunakan Content-Based Filtering

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | 5 | 1 | 5 |
| Jenis data yang dikumpulkan | Data numerik (rating, biaya, dll) | Pendapat/pengalaman pengguna | Data sistem & hasil pengujian |
| Limitasi paradigma | Kurang melihat sisi subjektif pengguna | Kurang cocok untuk perhitungan angka | Lebih fokus ke sistem, jadi sisi teorinya tidak terlalu dalam |

**Paradigma yang dipilih:** Positivis dan Design Science
**Alasan:** Karena penelitian ini menggunakan data angka dan perhitungan seperti MAE dan RMSE (positivis), serta membuat sistem rekomendasi yang diuji performanya (design science).

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelumnya saya langsung percaya dengan klaim seperti “95% akurat”. Tetapi, setelah memahami tentang distorsi, saya akan bertanya apakah data yang digunakan itu benar-benar dari kondisi nyata, bagaimana cara menghitung akurasinya, dan apakah hasilnya bisa benar-benar dipakai di dunia nyata.
