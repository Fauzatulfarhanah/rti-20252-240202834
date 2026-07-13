# WS-16: Presentation & Defense (UAS)

> **Bab 16 — Presentasi & Pertahanan Ilmiah**

**Nama:** Fauzatul Farhanah
**NIM:** 240202834
**Kelas:** 4IKRB
**Mata Kuliah:** Riset dan Teknologi Informasi
**Topik Penelitian:** Analisis Perbandingan YOLOv2 dan YOLOv3 untuk Deteksi dan Penghitungan Manusia Menggunakan CCTV Lift

---

## Ringkasan Materi

### Scientific Defense Model


```

Research Work → Presentation → Questioning → Defense → Evaluation → Acceptance

```

### Presentasi ≠ Ringkasan Paper

| Paper | Presentasi |
|-------|-----------|
| Dibaca (self-paced) | Didengar (presenter-paced) |
| Detail lengkap | Ide kunci + highlight |
| Tabel numerik detail | Grafik visual + angka kunci |
| Pembaca bisa re-read | Audiens dengar sekali |

**Prinsip:** Presentasi membutuhkan **reformulasi**, bukan kompresi. Medium berbeda = pendekatan berbeda.

### Claim-Evidence-Reasoning (CER)

Setiap jawaban defense harus memiliki:
1. **Claim** — Pernyataan yang dijawab
2. **Evidence** — Data/fakta pendukung
3. **Reasoning** — Logika yang menghubungkan evidence ke claim

**Contoh:**
| Pertanyaan | Bad Answer | Good Answer (CER) |
|-----------|-----------|-------------------|
| "Kenapa hanya 3 dataset?" | "Tiga sudah cukup" | "3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy [E]. Generalisasi perlu validasi lanjut — listed as limitation [R]" |
| "Hasil DS-3 menurun?" | "Itu outlier" | "Ya, karena distribusi heavy-tail melanggar asumsi Gaussian [E]. Ini menunjukkan boundary condition metode [R]" |
| "Effect size?" | "p=0.003, jadi signifikan" | "Cohen's d=1.2 (large effect) [E] — bukan hanya signifikan tapi substansial [R]" |

### Slide Design — One Slide, One Message

**Optimal 9-Slide Plan (15 menit):**

| # | Slide | Waktu | Pesan |
|---|-------|-------|-------|
| 1 | Title + context | 1 min | Apa ini tentang apa |
| 2 | Problem + motivation | 2 min | Mengapa penting |
| 3 | Gap + RQ | 1.5 min | Apa yang belum terjawab |
| 4 | Method overview | 2 min | Bagaimana dijawab (diagram) |
| 5 | Key result — tabel | 2 min | Temuan utama |
| 6 | Key result — grafik | 2 min | Pola visual |
| 7 | Interpretation + failure | 2 min | Apa artinya |
| 8 | Limitation + future | 1.5 min | Batasan & arah |
| 9 | Conclusion + contribution | 1 min | Closing message |

### Anticipatory Defense

Prediksi pertanyaan berdasarkan kategori:

| Kategori | Contoh Pertanyaan |
|---------|------------------|
| Problem | "Mengapa masalah ini penting?" |
| Gap | "Bagaimana dengan studi X yang sudah menjawab ini?" |
| Method | "Mengapa metode ini, bukan Y?" |
| Results | "Bagaimana menjelaskan anomali di DS-3?" |
| Generalization | "Apakah bisa diterapkan di domain lain?" |

### Tiga Prinsip Jawaban

1. **Direct** — Jawab dulu, elaborasi kemudian
2. **Data-based** — Tunjuk evidence spesifik
3. **Honest** — Akui limitasi jika memang ada

### Jebakan Kognitif

1. "Presentasi = semua yang ada di paper" → terlalu padat
2. "Slide cantik = presentasi bagus" → konten > estetika
3. "Tidak bisa jawab = gagal" → "I don't know, but..." menunjukkan kejujuran
4. "Tidak perlu latihan — saya paham riset saya" → latihan = menemukan celah

---

## Template A.16 — Defense Preparation Sheet


```

DEFENSE PREPARATION

Slide Deck Plan:
Total slides   : 11 Slides (9 konten utama + 1 title + 1 closing)
Time per slide : ~1.3 menit
Total time     : 15 menit

Slide Outline:

| # | Pesan Utama | Visual | Waktu |
| --- | --- | --- | --- |
| 1 | Judul, Identitas Diri, dan Topik Komparasi YOLOv2 vs YOLOv3 | Slide Judul Resmi UPB + Foto Skenario Lift | 1.0 min |
| 2 | Urgensi pembatasan kapasitas lift & bahaya galat hitung manual | Grafik Data Insiden Overkapasitas Lift / Foto Berita | 2.0 min |
| 3 | Rumusan Masalah (4 RQ) & Gap dari Riset Pamungkas (2021) | Tabel Pemetaan Gap Literatur & Teks Eksplisit RQ | 1.5 min |
| 4 | Metodologi eksperimen terkontrol pada GPU Tesla T4 Cloud | Diagram Alir Prosedur Eksperimen 7 Langkah | 2.0 min |
| 5 | Hasil Aktual Akurasi: YOLOv3 mendominasi nilai keyakinan | Tabel Deskriptif Mean Confidence Score (78.6% vs 57.1%) | 2.0 min |
| 6 | Hasil Aktual Waktu Inferensi: YOLOv2 unggul efisiensi 30% | Bar Chart Komparasi Latensi Temporal Pemrosesan (ms) | 1.5 min |
| 7 | Analisis Kegagalan: Deteksi berhimpit memicu overcounting | Cuplikan Visual Bounding Box Redundan pada Skenario Padat | 2.0 min |
| 8 | Batasan Ukuran Sampel Pilot (N=4) & Solusi Skala Penuh | Tabel Validitas Internal/Eksternal + Rencana N=150 | 1.5 min |
| 9 | Kesimpulan Trade-off Spasial-Temporal & Rekomendasi Praktis | Diagram Rekomendasi Model Berdasarkan Kebutuhan Gedung | 1.5 min |

Anticipatory Defense Matrix:

| Kategori | Pertanyaan Potensial | Jawaban (CER) |
| --- | --- | --- |
| Problem | Mengapa harus menggunakan computer vision untuk menghitung kapasitas lift, bukan sensor berat mekanis saja? | Sensor berat mekanis hanya bekerja saat kondisi lift sudah kritis dan pintu akan menutup [C]. Melalui visual CCTV, sistem bisa mendeteksi antrean dan melakukan pencegahan sebelum pengguna masuk [E]. Logikanya, computer vision memberikan perlindungan preventif, bukan reaktif [R]. |
| Gap | Apa beda riset ini dengan riset Pamungkas (2021) yang sama-sama menguji YOLOv2 dan YOLOv3? | Riset terdahulu tidak menstandarisasi environment dan threshold pengujian untuk kedua model [C]. Di riset ini, kami menggunakan threshold identik (0.30) pada arsitektur GPU Tesla T4 yang sama [E]. Maka, bias eksternal berhasil dieliminasi untuk menghasilkan komparasi yang objektif [R]. |
| Method | Mengapa memilih uji Wilcoxon Signed-Rank, bukan Paired t-test yang biasa digunakan? | Uji Wilcoxon dipilih karena sebaran data sampel pilot test ini tidak berdistribusi normal [C]. Berdasarkan uji normalitas, ukuran sampel awal yang kecil (N=4) menghasilkan sebaran bimodal [E]. Menggunakan uji parametrik pada data non-normal akan melanggar asumsi statistika dasar [R]. |
| Results | Mengapa kuantitas deteksi YOLOv2 pada citra padat (@jaoyng) lebih banyak (13 orang) daripada YOLOv3 (11 orang), apakah itu artinya YOLOv2 lebih teliti? | Tidak, jumlah yang lebih banyak itu justru merupakan anomali overcounting (false positive) [C]. Hasil visual menunjukkan YOLOv2 memunculkan bounding box ganda pada objek manusia yang sama [E]. Hal ini terjadi karena arsitektur spasial tunggal Darknet-19 gagal menyaring box redundan lewat NMS [R]. |
| Generalization | Apakah model yang diuji pada citra statis ini bisa langsung diimplementasikan pada video CCTV lift real-time? | Bisa, namun dengan catatan batasan spesifikasi hardware penunjang [C]. Hasil uji mencatat latensi YOLOv2 adalah 69.86 ms dan YOLOv3 adalah 90.82 ms [E]. Kedua angka ini masih berada di bawah ambang batas pemrosesan video real-time standar (100 ms), sehingga sangat siap dideploy [R]. |

Latihan:
Latihan 1: 06 Juli 2026 — Catatan: Presentasi melebihi waktu (18 menit) karena terlalu lama membaca data angka tabel di slide hasil.
Latihan 2: 09 Juli 2026 — Catatan: Timing pas (14.5 menit), penyampaian slide hasil diubah fokusnya ke angka kunci rata-rata dan grafik visual.
Latihan 3: 12 Juli 2026 — Catatan: Timing stabil (14 menit), kelancaran menjawab pertanyaan simulasi CER meningkat tajam.

```

---

## Latihan 1 — Slide Outline

Rencanakan presentasi 15 menit untuk riset Anda.

| # | Pesan Utama | Visual yang Digunakan | Waktu |
|---|-------------|----------------------|-------|
| 1 | Analisis Perbandingan YOLOv2 vs YOLOv3 pada CCTV Lift | Slide Judul Resmi Universitas Putra Bangsa, Identitas Mahasiswi | 1.0 min |
| 2 | Urgensi pembatasan kapasitas lift gedung bertingkat demi keselamatan | Foto ruang dalam lift yang padat + kutipan regulasi batas muatan | 1.5 min |
| 3 | Gap Penelitian: Ketiadaan pengujian komparatif dengan parameter terkontrol | Tabel komparasi pemetaan fitur riset terdahulu vs riset saat ini | 1.5 min |
| 4 | Metode: Eksperimen terkontrol 2 arsitektur model pada Google Colab GPU | Diagram alir 7 langkah prosedur (Input -> Preprocess -> Run -> Evaluasi)| 2.0 min |
| 5 | Temuan Akurasi: YOLOv3 mendominasi kestabilan nilai keyakinan | Tabel deskriptif nilai Mean & Std Deviasi Confidence Score (78.6% vs 57.1%) | 2.0 min |
| 6 | Temuan Kecepatan: YOLOv2 memotong waktu inferensi rata-rata sebesar 30% | Bar chart komparasi performa latensi temporal (69.86 ms vs 90.82 ms) | 1.5 min |
| 7 | Failure Analysis: Oklusi tinggi teridentifikasi sebagai boundary condition | Visualisasi perbandingan bounding box redundan pada gambar `@jaoyng.jpg` | 2.0 min |
| 8 | Batasan Penelitian: Skala dataset pilot (N=4) & ancaman validitas | Tabel matriks limitasi (Internal, External, Construct) + mitigasi | 1.5 min |
| 9 | Kesimpulan & Rekomendasi: Trade-off komputasi spasial-temporal | Teks ringkas kesimpulan (jawaban 4 RQ) + poin agenda Future Work | 2.0 min |

**Total waktu estimasi:** 15.0 menit

---

## Latihan 2 — Anticipatory Defense

Prediksi 5 pertanyaan yang mungkin diajukan penguji, lalu siapkan jawaban CER.

| # | Kategori | Pertanyaan | Claim | Evidence | Reasoning |
|---|----------|-----------|-------|----------|-----------|
| 1 | *Problem* | Mengapa variabel "kepadatan objek" dimasukkan sebagai salah satu skenario pengujian? | Kepadatan memicu oklusi visual yang menurunkan akurasi model | Nilai mean confidence YOLOv3 merosot tajam dari 96.5% ke 60.9% saat objek padat | Perubahan density mengubah beban ekstraksi fitur arsitektur secara drastis |
| 2 | *Method* | Mengapa Anda menguji model menggunakan bobot bawaan COCO (80 kelas), bukan melakukan custom training khusus manusia? | Pengujian dengan bobot COCO bertujuan menguji keandalan dasar arsitektur asli | Muncul deteksi objek mati (bottle, cell phone) secara salah pada hasil YOLOv2 | Ini membuktikan detektor spasial tunggal rentan mengalami distorsi kelas di area sempit |
| 3 | *Results* | Berapa besarnya efek keunggulan akurasi YOLOv3 dibanding YOLOv2 berdasarkan uji statistik? | Efek keunggulan akurasi YOLOv3 bernilai sangat besar (*Large Effect*) | Nilai perhitungan effect size r pada pengujian Wilcoxon didapatkan sebesar 0.88 | Angka r > 0.5 membuktikan perbedaan performa kedua arsitektur nyata secara substansial |
| 4 | *Failure* | Mengapa YOLOv3 bisa lebih stabil menahan efek penurunan akurasi pada kondisi padat dibanding YOLOv2? | Arsitektur YOLOv3 memanfaatkan fitur deteksi multi-skala | YOLOv3 memiliki struktur Darknet-53 dengan tiga lapisan ekstraksi ukuran box | Fitur berlapis memungkinkannya mengenali bagian tubuh manusia yang terpotong/terhalang |
| 5 | *Generalization* | Bagaimana Anda akan menguji validitas eksternal hasil penelitian ini di masa mendatang? | Melakukan ekspansi skala pengujian dengan dataset yang bervariasi | Menambah total sampel menjadi N=150 citra dari 3 gedung bertingkat berbeda | Pengujian multisitus diperlukan untuk menjamin keandalan sistem kontrol lift universal |

---

## Latihan 3 — Simulasi Q&A

Minta teman/kolega mengajukan 3 pertanyaan tentang riset Anda. Catat pertanyaan dan evaluasi jawaban Anda.

| # | Pertanyaan | Jawaban Saya | Evaluasi |
|---|-----------|-------------|---------|
| 1 | Mengapa pada gambar `amigos.jpg` standar deviasi confidence score YOLOv2 sangat tinggi (13.1%) dibanding YOLOv3 (1.2%)? | Karena performa deteksi YOLOv2 tidak konsisten antar individu di gambar tersebut, di mana ada box yang bernilai 84% tapi ada yang anjlok ke 58%. Sementara YOLOv3 stabil mematok nilai keyakinan di atas 98% untuk seluruh objek. | [✓] Direct [✓] Data-based [✓] Honest |
| 2 | Mengapa metrik IoU (*Intersection over Union*) belum dipaparkan datanya di bab Hasil, padahal dijanjikan di bab Metode? | Saya mengakui bahwa kalkulasi matriks IoU otomatis belum sempat diintegrasikan ke dalam kode pengujian Colab saat pilot test ini dijalankan. Saat ini, pergeseran posisi box baru dievaluasi secara visual-manual dan hal ini resmi dicatat sebagai batasan penelitian. | [✓] Direct [✓] Data-based [✓] Honest |
| 3 | Dari data waktu proses, arsitektur mana yang paling direkomendasikan untuk perangkat komputasi berspesifikasi rendah (*edge device*)? | YOLOv2 adalah arsitektur yang paling direkomendasikan untuk edge device. Berdasarkan data aktual, rata-rata waktu inferensinya konsisten paling rendah, yaitu sebesar 69.86 ms, menghemat durasi pemrosesan komputasi sebesar 30% dibanding YOLOv3. | [✓] Direct [✓] Data-based [✓] Honest |

**Pertanyaan yang paling sulit dijawab:**
> Pertanyaan mengenai alasan ketiadaan kalkulasi metrik IoU otomatis di slide hasil, karena hal itu langsung menyoroti kelemahan implementasi pemrograman skrip pengujian saya yang belum tuntas.

**Apa yang perlu disiapkan lebih baik:**
> Memperkuat landasan argumen pada bagian batasan penelitian (*limitation*) dan menyusun rencana kerja masa depan (*future work*) secara taktis, sehingga ketika penguji menanyakan kekurangan program, saya bisa menjawabnya dengan solusi ilmiah yang terstruktur.

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-16 — dari paradigma riset hingga presentasi — bagian mana yang paling mengubah cara Anda berpikir tentang riset? Apa satu hal yang akan selalu Anda terapkan di riset berikutnya?

**Insight terbesar:**
> Bagian yang paling mengubah cara berpikir saya adalah *Failure Analysis as a Contribution* (Bab 14) dan metode argumen CER (Bab 16). Dulu saya mengira riset yang bagus adalah riset yang hasilnya selalu sukses, mulus, dan tanpa cacat. Namun, saya menyadari bahwa ketika arsitektur YOLOv2 mengalami kegagalan (anomali *overcounting*) di skenario padat, data eror tersebut justru menjadi temuan ilmiah yang sangat kaya jika mampu dibedah alasannya secara struktural. Kegagalan riset bukanlah aib, melainkan batas pengetahuan baru yang berhasil dipetakan.

**Yang akan selalu diterapkan:**
> Saya akan selalu menerapkan *Consistency Matrix* dan kerangka berpikir *Red Thread* (Benang Merah) di setiap riset ke depan. Menjaga keselarasan mutlak antara apa yang dipertanyakan di awal (RQ), apa yang diukur di laboratorium (Method), apa yang disajikan di tabel (Result), hingga apa yang dipertahankan di depan dewan penguji (Defense) adalah kunci utama integritas sebuah karya ilmiah.

```







