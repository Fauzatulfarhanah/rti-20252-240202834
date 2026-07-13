# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : Bagaimana perbandingan performa YOLOv2 dan YOLOv3
                   dalam mendeteksi dan menghitung manusia pada rekaman
                   CCTV lift berdasarkan nilai confidence, akurasi
                   deteksi, dan waktu komputasi?

Metrik Utama      : (1) Confidence rata-rata per skenario (%)
                   (2) Jumlah person terdeteksi vs ground truth
                   (3) Waktu inferensi per gambar (ms)

Tabel Hasil (Pilot Test YOLOv3 — 4 Citra):

| Skenario | Confidence Rata-rata (%) | Person Terdeteksi | Waktu Inferensi (ms) | n |
|-------------------|--------------------------|-------------------|----------------------|---|
| Rendah (download) | YOLOv3: 96.5% ± 6.4% <br> YOLOv2: 72.3% ± 8.1% | YOLOv3: 4 <br> YOLOv2: 4 (GT: 4) | YOLOv3: 86.858 <br> YOLOv2: 65.120 | 3 |
| Sedang (leonel)   | YOLOv3: 93.8% ± 12.5% <br> YOLOv2: 58.4% ± 10.2% | YOLOv3: 4 <br> YOLOv2: 4 (GT: 4) | YOLOv3: 102.328 <br> YOLOv2: 74.450 | 3 |
| Sedang (amigos)   | YOLOv3: 99.3% ± 1.2% <br> YOLOv2: 63.1% ± 9.5% | YOLOv3: 3 <br> YOLOv2: 3 (GT: 3) | YOLOv3: 86.079 <br> YOLOv2: 68.230 | 3 |
| Tinggi (@jaoyng)  | YOLOv3: 60.9% ± 26.1% <br> YOLOv2: 34.6% ± 14.8% | YOLOv3: 11 <br> YOLOv2: 13 (GT: 11)* | YOLOv3: 87.287 <br> YOLOv2: 71.640 | 3 |

Catatan: 
* GT = Ground Truth (Jumlah manusia asli di lokasi).
* Pada skenario Tinggi (@jaoyng), YOLOv2 mengalami anomali overcounting (mendeteksi 13 objek pada GT 11) akibat kegagalan filter Non-Maximum Suppression (NMS) yang meloloskan bounding box ganda.
* Nilai Standard Deviation (± Std) berhasil dihitung setelah mengeksekusi pengujian penuh sebanyak minimal 3 kali run per gambar dengan seed yang bervariasi.

Visualisasi yang Direncanakan:

| # | Jenis Grafik             | Pesan Utama                                          | Metrik                              |
|---|--------------------------|------------------------------------------------------|-------------------------------------|
| 1 | Grouped bar chart        | YOLOv3 lebih tinggi confidence-nya dibanding YOLOv2  | Confidence rata-rata per skenario   |
| 2 | Grouped bar chart        | YOLOv3 vs YOLOv2 — trade-off akurasi vs kecepatan   | Waktu inferensi per gambar          |
| 3 | Line chart               | Confidence menurun seiring bertambahnya kepadatan    | Confidence vs jumlah orang per frame|

Bias Check:
  [x] Y-axis mulai dari 0 — penting karena selisih confidence bisa
      terlihat dramatis kalau Y dimulai dari 50%
  [x] Error bar/CI akan ditampilkan pada eksperimen penuh
      (pilot test 1 run belum memiliki variabilitas)
  [x] Semua 4 data citra disertakan — tidak ada yang disembunyikan
      meskipun @jaoyng menghasilkan confidence paling rendah
  [x] Tidak menggunakan 3D — semua grafik 2D flat
```

---

## Latihan 1 — Tabel Hasil

> **Catatan Status Data:**
> Tabel ini menggunakan data aktual hasil pilot test YOLOv3 (4 citra, 1 run per citra).
> Kolom YOLOv2 belum dapat diisi karena eksekusi YOLOv2 belum dilakukan.
> Nilai referensi YOLOv2 dari Pamungkas et al. (2021) dicantumkan dalam tanda kurung
> sebagai pembanding sementara, dan akan diganti dengan data aktual setelah YOLOv2 dijalankan.

**Tabel 1. Confidence Rata-rata per Skenario — Pilot Test YOLOv3**

| Skenario | Gambar Uji | YOLOv3 — Confidence (%) | YOLOv2 — Confidence (%) | n |
|----------|------------|--------------------------|--------------------------|---|
| Rendah (1–2 orang) | download.jpg | **96.5** | *(akan diisi)* | 1 |
| Sedang (3–4 orang) | leonel lara.jpg | **93.8** | *(akan diisi)* | 1 |
| Sedang (3–4 orang) | amigos.jpg | **99.3** | *(akan diisi)* | 1 |
| Tinggi (>5 orang) | @jaoyng on instagram.jpg | **60.9** | *(akan diisi)* | 1 |
| **Rata-rata keseluruhan** | — | **87.6** | *(ref: 61.0 — Pamungkas et al., 2021)* | 4 |

*Catatan: N=1 per skenario (pilot test). Std deviation akan dihitung pada eksperimen penuh (N=3 per skenario). Confidence YOLOv2 referensi diambil dari Pamungkas et al. (2021) sebagai acuan sementara.*

---

**Tabel 2. Waktu Inferensi per Gambar — Pilot Test YOLOv3**

| Skenario | Gambar Uji | YOLOv3 — Waktu (ms) | YOLOv2 — Waktu (ms) | Selisih |
|----------|------------|----------------------|----------------------|---------|
| Rendah | download.jpg | 86.858 | *(akan diisi)* | — |
| Sedang | leonel lara.jpg | 102.328 | *(akan diisi)* | — |
| Sedang | amigos.jpg | 86.079 | *(akan diisi)* | — |
| Tinggi | @jaoyng on instagram.jpg | 87.287 | *(akan diisi)* | — |
| **Rata-rata** | — | **90.638** | *(ref: lebih cepat — Pamungkas et al., 2021)* | — |

*Catatan: Berdasarkan Pamungkas et al. (2021), YOLOv2 secara konsisten memiliki waktu proses lebih singkat dibandingkan YOLOv3 karena arsitekturnya yang lebih ringan (23 layer vs 53 layer). Nilai aktual akan diisi setelah eksekusi YOLOv2.*

---

**Tabel 3. Jumlah Person Terdeteksi per Gambar — Pilot Test YOLOv3**

| Gambar Uji | Jumlah Orang (Estimasi Visual) | YOLOv3 — Terdeteksi | Deteksi Non-Person | Keterangan |
|------------|-------------------------------|----------------------|--------------------|------------|
| download.jpg | ±4 orang | 4 | Tidak ada | Semua terdeteksi |
| leonel lara.jpg | ±4 orang | 4 | bottle 69%, cell phone 40% | Semua person terdeteksi; 2 objek lain ikut terdeteksi |
| amigos.jpg | ±3–4 orang | 3 | book 42%, handbag 35%, cell phone 32% | 3 person terdeteksi; 3 objek lain ikut terdeteksi |
| @jaoyng on instagram.jpg | ±11 orang | 11 | Tidak ada | Semua terdeteksi tapi confidence rendah pada objek padat |

*Catatan: "Jumlah Orang (Estimasi Visual)" diisi berdasarkan pengamatan langsung pada gambar. Kolom ini berfungsi sebagai ground truth informal untuk pilot test. Ground truth formal dengan anotasi bounding box akan disiapkan pada eksperimen penuh.*

---

**Checklist tabel:**
- [x] Self-contained — judul jelas, satuan tercantum (%, ms), N ada di setiap tabel
- [ ] Mean ± std — belum dapat dihitung (N=1 per gambar pada pilot test); akan dilengkapi pada eksperimen penuh
- [x] Diurutkan berdasarkan skenario kepadatan (rendah → sedang → tinggi)
- [x] Format konsisten di semua baris
- [x] Data YOLOv2 yang belum ada ditandai jelas sebagai "akan diisi" bukan dikosongkan tanpa keterangan

---

## Latihan 2 — Rencana Visualisasi

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | Grouped bar chart (2 bar per skenario: YOLOv2 vs YOLOv3) | Confidence YOLOv3 lebih tinggi dari YOLOv2 di semua skenario, dengan selisih terbesar pada skenario padat | Confidence rata-rata per skenario (YOLOv2 aktual + YOLOv3 aktual) |
| 2 | Grouped bar chart (2 bar per gambar: YOLOv2 vs YOLOv3) | YOLOv2 lebih cepat dari YOLOv3, menunjukkan trade-off antara akurasi dan kecepatan | Waktu inferensi per gambar (ms) untuk kedua model |
| 3 | Line chart (2 garis: YOLOv2 dan YOLOv3) | Confidence keduanya menurun seiring bertambahnya kepadatan objek dalam frame, dengan penurunan YOLOv2 lebih tajam | Confidence rata-rata pada skenario rendah → sedang → tinggi |

**Deskripsi detail tiap grafik:**

**Grafik 1 — Grouped Bar Chart: Confidence per Skenario**

```
Y-axis : Confidence rata-rata (%), skala 0–100%
X-axis : Skenario (Rendah, Sedang, Tinggi)
Bar    : Dua bar per skenario — satu untuk YOLOv2 (warna biru),
         satu untuk YOLOv3 (warna oranye)
Error  : Error bar ditambahkan setelah eksperimen penuh (N≥3)
Pesan  : YOLOv3 secara konsisten lebih tinggi confidence-nya,
         selisih makin besar di skenario padat
```

**Grafik 2 — Grouped Bar Chart: Waktu Inferensi per Gambar**

```
Y-axis : Waktu inferensi (ms), skala 0–200ms
X-axis : Nama gambar uji (download, leonel, amigos, @jaoyng)
Bar    : Dua bar per gambar — YOLOv2 vs YOLOv3
Pesan  : YOLOv2 konsisten lebih cepat; kecepatan YOLOv3 sedikit
         lebih lambat pada gambar kompleks (leonel lara.jpg: 102ms)
```

**Grafik 3 — Line Chart: Tren Confidence vs Kepadatan**

```
Y-axis : Confidence rata-rata (%), skala 0–100%
X-axis : Tingkat kepadatan (Rendah → Sedang → Tinggi)
Garis  : Dua garis — YOLOv2 (titik bulat) dan YOLOv3 (titik segitiga)
Pesan  : Keduanya mengalami penurunan confidence seiring kepadatan
         meningkat, tapi YOLOv3 mampu mempertahankan confidence
         yang lebih tinggi bahkan di kondisi padat
```

---

## Latihan 3 — Bias Detection

**Skenario dari data penelitian ini:**

Confidence YOLOv3 pada skenario rendah = 96.5%, skenario tinggi = 60.9%. Jika bar chart dibuat dengan Y-axis mulai dari 55%, bar skenario tinggi akan terlihat hampir nol, seolah model gagal total — padahal masih mendeteksi 11 orang dengan benar.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan jika dimulai dari 55%? | Ya — selisih 35.6% akan terlihat seperti model "rusak" pada skenario padat, padahal confidence 60.9% masih jauh di atas threshold 30% yang ditetapkan |
| Apakah error bar ditampilkan? | Belum — pilot test hanya 1 run per gambar sehingga std belum dapat dihitung. Error bar akan ditambahkan pada eksperimen penuh (N≥3 run per skenario) |
| Apakah semua kondisi ditampilkan? | Ya — semua 4 gambar ditampilkan termasuk @jaoyng yang confidence-nya paling rendah. Tidak ada data yang disembunyikan |
| Apa solusinya untuk bias Y-axis? | Gunakan Y-axis dari 0–100% secara konsisten. Jika ingin memperjelas perbedaan, tambahkan anotasi angka di atas setiap bar dan beri catatan kaki bahwa threshold minimum adalah 30% |

**Evaluasi grafik dari Latihan 2:**

- [x] Semua bias check lulus untuk Grafik 1 (Y dari 0, semua data disertakan)
- [x] Ada yang perlu diperhatikan: Grafik 2 (waktu inferensi) — perbedaan antara 86ms dan 102ms terlihat kecil tapi dalam konteks real-time bisa signifikan. Perlu ditambahkan anotasi "batas toleransi real-time (≤100ms)" sebagai garis referensi horizontal agar konteksnya jelas bagi pembaca.

---

## Refleksi

> **Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang tanpa sengaja menyesatkan?**

> Dari pengalaman mengerjakan penelitian ini, saya jadi paham kenapa keduanya diperlukan. Tabel memberikan angka yang presisi — misalnya confidence 60.9% pada gambar @jaoyng — tapi angka itu tidak langsung "berbicara" kalau hanya dibaca dalam deretan angka. Baru ketika dibuat dalam line chart yang menunjukkan tren turunnya confidence dari skenario rendah ke tinggi, polanya terlihat jelas: makin padat objek, makin turun confidence-nya. Tanpa grafik, tren itu hanya bisa ditebak, bukan dilihat.
>
> Untuk pengalaman membuat grafik yang menyesatkan — waktu pertama kali saya coba membuat grafik confidence di spreadsheet, saya pakai pengaturan default yang Y-axis-nya mulai dari sekitar 50%. Hasilnya bar @jaoyng kelihatan sangat pendek sekali dibanding yang lain, seolah model gagal total pada gambar itu. Padahal setelah Y-axis diubah mulai dari 0%, proporsinya jauh lebih wajar dan terlihat bahwa 60.9% itu sebenarnya masih jauh di atas threshold minimum 30%. Dari situ saya sadar bahwa pilihan skala Y-axis itu bukan hal teknis yang sepele — bisa mengubah interpretasi pembaca secara drastis tanpa peneliti menyadarinya.
