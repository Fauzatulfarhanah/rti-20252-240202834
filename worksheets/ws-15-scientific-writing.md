# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title   : Analisis Perbandingan YOLOv2 dan YOLOv3 untuk Deteksi dan
          Penghitungan Manusia Menggunakan Rekaman CCTV Lift
Target  : [x] Laporan (Proposal UTS) → rencana ke [ ] Jurnal / [ ] Konferensi

Section Check:
  [x] Abstract — masalah (kapasitas lift + COVID), metode (komparatif
      eksperimen terkontrol YOLOv2 vs YOLOv3), hasil yang diharapkan
      (YOLOv3 lebih akurat, YOLOv2 lebih cepat), kontribusi (laporan
      komparatif terukur + rekomendasi model). Max 250 kata ✓

  [x] Introduction (D.1 + D.2 + D.3) — konteks (lift + COVID-19 +
      CCTV) → gap (tidak ada evaluasi komparatif terkontrol YOLOv2 vs
      YOLOv3 di CCTV lift) → RQ (4 RQ tentang confidence, akurasi,
      waktu, kepadatan) → kontribusi (data komparatif valid secara
      metodologis)

  [x] Related Work (D.3 State of the Art) — literature mapping dari
      Redmon et al. (2016) → YOLOv2 (2017) → YOLOv3 (2018) →
      Pamungkas et al. (2021) → Khairunnas (2021) → Sugandi (2022) →
      Yanto (2023). Gap diposisikan eksplisit sebagai selisih antara
      kondisi ideal dan kondisi aktual

  [x] Method (E.1 s.d. E.5) — desain komparatif terkontrol, IV/DV,
      metrik lengkap (confidence, precision, recall, F1, IoU, waktu),
      skenario kepadatan 3 level, prosedur 7 langkah, setup Darknet
      + Colab, batasan dan asumsi

  [x] Results — Data pengujian dari kedua model arsitektur (YOLOv2 dan YOLOv3) 
      telah dieksekusi secara lengkap. Menyajikan tabel statistik deskriptif 
      mean confidence score per skenario kepadatan (YOLOv3 unggul rata-rata 
      78.6% vs YOLOv2 57.1%) dan tabel perbandingan performa latensi temporal 
      (YOLOv3 90.82 ms vs YOLOv2 69.86 ms). Menyertakan visualisasi bounding box 
      dan pemetaan anomali overcounting.

  [x] Discussion — Interpretasi mendalam menunjukkan keunggulan akurasi YOLOv3 
      signifikan secara statistik lewat uji Wilcoxon Signed-Rank (p < 0.05, r = 0.88). 
      Ditemukan boundary condition pada skenario padat di mana oklusi ekstrem memicu 
      kegagalan filter NMS pada YOLOv2 (mendeteksi 13 objek dari ground truth 11). 
      Hasil disinkronkan dengan literatur Pamungkas et al. (2021) dan limitasi 
      skala dataset diakui secara eksplisit.

  [x] Conclusion (F. Hasil yang Diharapkan) — menjawab 4 RQ secara
      prediktif, kontribusi (laporan komparatif + rekomendasi), future
      work (integrasi ke sistem kontrol lift real-time)

Consistency Matrix:
  [x] RQ di Introduction = RQ di Method = RQ di Conclusion
      (4 RQ konsisten muncul di D.2, E.1, dan F)
  [x] Variabel di Method = variabel di Results
      (IV: jenis model; DV: confidence, jumlah terdeteksi, waktu —
       semuanya diukur dalam pilot test)
  [x] Klaim di Discussion didukung data di Results
      (pilot test mendukung klaim YOLOv3 confidence ~87.6% vs
       referensi YOLOv2 61.0% dari Pamungkas et al. 2021)
  [x] Limitasi di Discussion di-address di Conclusion/Future Work
      (N kecil → eksperimen penuh 150 citra; YOLOv2 belum → rencana
       eksekusi; boundary condition kepadatan → rekomendasi threshold)

Writing Quality:
  [x] Clarity — kalimat kunci menggunakan angka spesifik, bukan
      deskripsi samar ("confidence YOLOv3 rata-rata 87.6%", bukan
      "performa lebih baik")
  [x] Precision — istilah teknis konsisten (YOLOv2/YOLOv3, bukan
      "model lama/baru"; "confidence" bukan "akurasi" untuk DV1)
  [x] Conciseness — setiap bagian proposal langsung ke isi; tidak ada
      kalimat pembuka umum yang tidak informatif
```

---

## Latihan 1 — Paper Outline

| Section | Konten Utama | Target Kata |
|---------|-------------|------------|
| Abstract | Masalah: lift tanpa deteksi otomatis pengguna → risiko pelanggaran kapasitas di masa pandemi. Metode: eksperimen komparatif terkontrol YOLOv2 vs YOLOv3 pada rekaman CCTV lift (threshold 0.30, 3 skenario kepadatan). Hasil utama: YOLOv3 confidence rata-rata 87.6% vs YOLOv2 referensi 61.0%; YOLOv2 lebih cepat secara komputasi. Kontribusi: data komparatif terukur sebagai dasar pemilihan model berbasis bukti. | 200–250 |
| Introduction | Konteks: lift sebagai fasilitas kritis + regulasi kapasitas COVID-19 2020. Gap: Pamungkas et al. (2021) membandingkan YOLOv2 dan YOLOv3 tapi tidak dalam kondisi eksperimen terkontrol dan identik; metrik tidak lengkap; tidak ada analisis per kepadatan. RQ utama: bagaimana perbandingan YOLOv2 vs YOLOv3 pada confidence, akurasi, dan waktu komputasi? Kontribusi: evaluasi komparatif metodologis pertama dengan metrik lengkap dan skenario kepadatan. | 500–700 |
| Related Work | Kronologi: YOLO (Redmon et al., 2016) → YOLOv2/YOLO9000 (2017) → YOLOv3 (2018). Aplikasi deteksi manusia: Lan et al. (2018) pedestrian detection, Pamungkas et al. (2021) CCTV lift, Khairunnas et al. (2021) mobile robot YOLOv4, Sugandi & Hartono (2022) quadcopter YOLOv5, Yanto et al. (2023) YOLOv8 masker. Pola: setiap generasi lebih akurat tapi lebih lambat; tidak ada yang membandingkan dua versi secara terkontrol di CCTV lift. Gap eksplisit: selisih antara evaluasi mandiri (kondisi aktual) dan evaluasi komparatif terkontrol (kondisi ideal). | 700–1000 |
| Method | Desain: controlled comparative experiment. Unit analisis: frame citra dari rekaman CCTV lift. Populasi: rekaman CCTV lift bertingkat; sampel purposive 150 citra + 10 video (pilot: 4 citra). IV: jenis model (YOLOv2 vs YOLOv3). DV: confidence, jumlah terdeteksi, waktu komputasi. Metrik: confidence rata-rata, precision, recall, F1-score, IoU, waktu inferensi. Setup: Darknet + Google Colab GPU + OpenCV; threshold 0.30 identik. Skenario: rendah (1–2), sedang (3–4), tinggi (5–6 orang). Prosedur 7 langkah. Batasan dan asumsi. | 800–1200 |
| Results | Menyajikan tabel komparatif performa YOLOv3 vs YOLOv2. Hasil akurasi pilot: YOLOv3 menghasilkan mean confidence score lebih kokoh (78.6% vs 57.1%), di mana pada skenario rendah mencapai 96.5% dan sedang 93.8–99.3%. Hasil temporal: YOLOv2 unggul konstan dengan rata-rata inferensi 69.86 ms vs YOLOv3 yang memakan waktu 90.82 ms (selisih kecepatan ~30.00%). Observasi: Penurunan confidence score signifikan terjadi di skenario padat (YOLOv3 turun ke 60.9%); muncul deteksi non-person (bottle, cell phone) karena bobot COCO 80 kelas; serta terpetakan anomali overcounting (13 box) pada YOLOv2 akibat kegagalan filter NMS saat oklusi tinggi. | 500–800 |
| Discussion | Interpretasi per RQ: RQ1 (YOLOv3 confidence lebih tinggi terkonfirmasi), RQ3 (YOLOv2 lebih cepat. Boundary condition ditemukan: confidence YOLOv3 turun dari 96.5% ke 60.9% saat kepadatan naik dari 4 ke 11 orang. Implikasi praktis: sistem perlu penyesuaian threshold di skenario padat. Perbandingan literatur: konsisten dengan Pamungkas et al. (2021). Limitation: N kecil pada pilot, YOLOv2 belum dieksekusi, ground truth informal. | 600–900 |
| Conclusion | Jawaban 4 RQ: YOLOv3 unggul dalam akurasi, YOLOv2 dalam kecepatan; perbedaan makin besar di skenario padat. Kontribusi: data komparatif terkontrol pertama untuk konteks CCTV lift. Rekomendasi: pilih YOLOv3 untuk akurasi, YOLOv2 untuk real-time terbatas. Future work: integrasi ke sistem kontrol lift nyata + uji pada dataset CCTV lift yang lebih besar dan beragam gedung. | 200–400 |

---

## Latihan 2 — Consistency Matrix

| | Intro (D.1–D.3) | Method (E.1–E.5) | Result (F — prediksi / pilot) | Discussion (rencana) | Conclusion (F) |
|--|----------------|-----------------|-------------------------------|---------------------|---------------|
| **RQ1** — confidence YOLOv3 > YOLOv2? | ✓ | ✓ | ✓ | ✓ | ✓ |
| **RQ2** — akurasi penghitungan berbeda? | ✓ | ✓ | ✓ | ✓ | ✓ |
| **RQ3** — waktu komputasi? | ✓ | ✓ | ✓ | ✓ | ✓ |
| **RQ4** — kepadatan berpengaruh? | ✓ | ✓ | ✓ (boundary condition teridentifikasi)| ✓ | ✓ |
| **IV — jenis model YOLO** | ✓ | ✓ | ✓ | ✓ | ✓ |
| **DV1 — confidence** | ✓ | ✓ | ✓ | ✓ | ✓ |
| **DV2 — jumlah terdeteksi** | ✓ | ✓ | ✓ (anomali overcounting terpetakan) | ✓ | ✓ |
| **DV3 — waktu komputasi** | ✓ | ✓ | ✓ (data temporal aktual tersedia) | ✓ | ✓ |
| **Metrik precision/recall/F1** | ✓ | ✓ | ✓ (analisis komparatif kuantitas) | ✓ | ✓ |
| **Metrik IoU** | ✓ | ✓ | ~ (limitasi: evaluasi posisi box manual) | ✓ | ✓ |
| **Kontribusi utama** | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Batasan penelitian** | ✓ | ✓ | ✓ | ✓ | ✓ |

**Keterangan:** ✓ = ada dan konsisten | ✗ = missing | ~ = 

**Inkonsistensi yang ditemukan:**
> Berkat penyelesaian run data aktual untuk model baseline YOLOv2 pada Bab 14, seluruh indikator inkonsistensi data temporal (DV3, RQ3) dan kuantitas deteksi (DV2, RQ2) telah berhasil diselesaikan secara empiris. Satu-satunya nilai berstatus `~` yang tersisa adalah pada metrik IoU (*Intersection over Union*). Metrik ini diperkenalkan di bab Metode sebagai instrumen ukur, namun pada pengerjaan Hasil dan Pembahasan aktual, posisi koordinat kotak prediksi masih dievaluasi secara visual-komparatif (manual) tanpa kalkulasi matriks otomatis karena batasan waktu pemrograman.

**Tindakan perbaikan:**

> 1. Jalankan YOLOv2 pada 4 gambar pilot yang sama → mengisi DV3, RQ3, dan tabel perbandingan komparatif.
> 2. Anotasi ground truth secara formal menggunakan LabelImg pada 4 gambar uji → memungkinkan perhitungan precision, recall, F1-score, dan IoU.
> 3. Setelah kedua langkah di atas selesai, semua sel `~` dapat diubah menjadi ✓ dan paper/laporan final bisa ditulis secara konsisten penuh.

---

## Latihan 3 — Writing Quality Check

**Paragraf asli (dari D.1 Latar Belakang proposal):**

> Studi yang dilakukan oleh Pamungkas et al. (2021) telah menggunakan YOLOv3 dan YOLOv2 dalam konteks deteksi manusia di dalam lift, namun penelitian tersebut belum melakukan perbandingan eksperimen secara komprehensif. Hal ini terlihat dari beberapa keterbatasan, yaitu (1) tidak menggunakan dataset dan kondisi pengujian yang identik untuk kedua model secara simultan, (2) tidak melaporkan metrik evaluasi standar seperti precision, recall, dan F1-score secara komprehensif, dan (3) tidak menganalisis secara kuantitatif pengaruh kepadatan objek terhadap performa masing-masing model.

| Kriteria | Evaluasi | Perbaikan |
|----------|---------|-----------|
| Clarity | Sudah jelas — tiga keterbatasan dijabarkan eksplisit dengan nomor. Pembaca langsung tahu apa yang kurang dari studi rujukan | Tidak perlu perubahan besar |
| Precision | Frasa "belum melakukan perbandingan eksperimen secara komprehensif" masih agak umum — belum menyebut secara eksplisit apa yang dimaksud "komprehensif" di kalimat pertama | Pindahkan kata kunci "kondisi identik dan metrik lengkap" ke kalimat pertama agar lebih presisi sejak awal |
| Conciseness | Frasa "Hal ini terlihat dari beberapa keterbatasan, yaitu" bisa dipersingkat | Hapus frasa pengantar, langsung masuk ke poin keterbatasan |

**Paragraf setelah perbaikan:**

> Pamungkas et al. (2021) menerapkan YOLOv2 dan YOLOv3 untuk deteksi manusia di dalam lift, tetapi tidak membandingkan kedua model dalam kondisi eksperimen yang identik. Tiga keterbatasan metodologis teridentifikasi: (1) dataset dan threshold pengujian tidak distandarisasi untuk kedua model secara simultan, (2) metrik evaluasi yang dilaporkan terbatas pada confidence rata-rata tanpa mencakup precision, recall, dan F1-score, dan (3) pengaruh kepadatan objek terhadap performa masing-masing model tidak dianalisis secara kuantitatif. Ketiga keterbatasan ini menjadi dasar kebaruan penelitian yang diusulkan.

> **Catatan perubahan:** (1) "Studi yang dilakukan oleh" → langsung nama penulis — lebih ringkas. (2) Tambahan kalimat penutup "Ketiga keterbatasan ini menjadi dasar kebaruan..." — menghubungkan gap ke kontribusi penelitian (red thread). (3) Kalimat pertama kini sudah menyebut "kondisi identik" secara eksplisit.

---

## Refleksi

> **Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?**

> Perbedaannya terasa cukup nyata waktu mengerjakan proposal ini. Menulis "tentang" riset artinya mendeskripsikan — misalnya menjelaskan apa itu YOLOv2, apa itu YOLOv3, bagaimana cara kerjanya. Tapi menulis sebagai "argumen" artinya setiap kalimat harus menjawab pertanyaan: mengapa ini penting, mengapa ini belum dilakukan, dan mengapa cara ini yang paling tepat untuk menjawabnya. Argumen punya arah dan tujuan, sedangkan deskripsi hanya memberikan informasi.
>
> Soal urutan penulisan, saya sebelumnya selalu mulai dari Introduction karena terasa logis. "kan harus ada konteks dulu baru isi." Tapi setelah tahu cara yang disarankan (Method → Result → Discussion → Introduction), mulai masuk akal kenapa urutan itu lebih baik. Kalau Introduction ditulis pertama, kita cenderung berjanji hal-hal yang belum tentu bisa dibuktikan di hasil. Sementara kalau Method dan Result ditulis dulu, Introduction bisa ditulis lebih akurat karena sudah tahu betul apa yang benar-benar akan dilakukan dan ditemukan. Dalam penelitian ini misalnya, kalau Introduction ditulis sebelum pilot test dijalankan, mungkin tidak akan menyebut boundary condition kepadatan — padahal temuan dari @jaoyng.jpg itu justru salah satu poin paling kuat dalam argumentasi penelitian.
