# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : [Performance Gap] Penelitian sebelumnya menunjukkan bahwa metode YOLO sudah mampu mendeteksi manusia, namun masih terdapat perbedaan performa antara YOLOv2 dan YOLOv3 dalam hal nilai confidence dan jumlah objek yang terdeteksi. Hal ini menunjukkan bahwa performa sistem belum sepenuhnya optimal, sehingga perlu perbandingan untuk mengetahui metode yang lebih baik dalam mendeteksi dan menghitung manusia.

Research Question:
  Tipe         : [✅] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : Bagaimana perbandingan kinerja YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia berdasarkan nilai confidence pada citra dari video CCTV?
  Variabel IV  : Jenis metode yang digunakan (YOLOv2 dan YOLOv3)
  Variabel DV  : Hasil deteksi manusia dan jumlah objek yang terdeteksi
  Metrik       : Nilai confidence dan jumlah objek yang terdeteksi
  Dataset      : Citra hasil ekstraksi frame dari video CCTV
  Baseline     :  YOLOv2

Quality Check RQ:
  [✅] Variabel spesifik
  [✅] Metrik jelas
  [✅] Baseline ada
  [✅] Konteks disebutkan
  [✅] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : Penelitian ini memberikan hasil perbandingan antara YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia sehingga dapat diketahui metode yang memiliki performa lebih baik.
  Jenis kontribusi        : [ ] Improvement  [✅] Comparison  [ ] Novel approach
  Gap yang diisi          : Perbedaan performa antara YOLOv2 dan YOLOv3 dalam deteksi manusia.

Hypothesis Pair:
  H₀ : Tidak terdapat perbedaan yang signifikan pada nilai confidence antara YOLOv2 dan YOLOv3 dalam mendeteksi manusia.
  H₁ : Terdapat perbedaan yang signifikan pada nilai confidence antara YOLOv2 dan YOLOv3 dalam mendeteksi manusia.
  Threshold              : 0,05
  Justifikasi threshold  : Nilai 0,05 digunakan sebagai batas umum untuk menentukan apakah perbedaan yang terjadi signifikan atau tidak.
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-04:** Perbedaan performa antara YOLOv2 dan YOLOv3 dalam mendeteksi manusia berdasarkan nilai confidence dan hasil deteksi.

**RQ versi pertama (tulis bebas):**
> Apakah YOLOv3 lebih baik dibandingkan YOLOv2 dalam mendeteksi manusia?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | Ya| Perbandingan YOLOv2 dan YOLOv3 |
| Metrik terukur | Belum| Nilai confidence belum disebutkan secara jelas|
| Baseline | Ya| YOLOv2 sebagai pembanding|
| Dataset/konteks | Belum| Dataset citra dari CCTV belum disebutkan|

**Tipe RQ:** [✅] Comparison / [ ] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Bagaimana perbandingan kinerja YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia berdasarkan nilai confidence pada dataset citra yang berasal dari video CCTV?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | Tidak terdapat perbedaan signifikan pada nilai confidence antara YOLOv2 dan YOLOv3 |
| H₁ | Terdapat perbedaan signifikan pada nilai confidence antara YOLOv2 dan YOLOv3 |
| Metrik | Confidence |
| Threshold | 0,05 |
| Justifikasi threshold | Digunakan sebagai batas umum untuk menentukan apakah perbedaan yang terjadi signifikan atau tidak |

**Apakah hipotesis ini falsifiable?** [✅] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? Dengan membandingkan hasil nilai confidence dari YOLOv2 dan YOLOv3. Jika hasilnya berbeda secara signifikan, maka H₀ ditolak.

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | Perbandingan YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia |
| Variable (IV) | Jenis metode (YOLOv2 dan YOLOv3) |
| Variable (DV) | Hasil deteksi dan jumlah manusia |
| Metric | Confidence dan jumlah objek |
| Data source | Citra dari video CCTV |
| Analysis method | Perbandingan hasil deteksi antara YOLOv2 dan YOLOv3 |

**Apakah rantai lengkap?** [✅] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? lengkap

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Deteksi dan Menghitung Manusia Menggunakan YOLO-CNN
**RQ yang diekstrak:** Bagaimana perbandingan kinerja YOLOv2 dan YOLOv3 dalam mendeteksi manusia berdasarkan nilai confidence pada citra CCTV?
**Komponen yang hilang:** Tidak ada, karena sudah mencakup metode, metrik, baseline, dan dataset.

## Referensi 
Pamungkas, B. P. G., Nugroho, B., & Anggraeny, F. (2021). Deteksi dan menghitung manusia menggunakan YOLO-CNN. Jurnal Informatika dan Sistem Informasi (JIFoSI), 2(1). https://d1wqtxts1xzle7.cloudfront.net/100194989/154-libre.pdf?1679582891=&response-content-disposition=inline%3B+filename%3DPenggunaan_lift_pada_gedung_gedu_DETEKSI.pdf&Expires=1777949909&Signature=EDef7tSF2CpB5vTX2vpWAteiB-~omcr2FGe2gJ5vqSKXB-OCEYz2zhpCXx2EMcG-rt3y0FooCEnxVRty2~~oS0wQvJezRqnN5odK8ufQlQ7k35QILGk1TQ5CDC1MFW5iyOfOuANEMCKDAq3JfpW68PclHoTv~qm~rIdRcjBuVEcHCm--wgKyYZkySWHxCX-R~LsU-w8dnzHtS0rZPCaeYisXMdtRgUQrrLa7Za3FaCYc5yiMGDLkP4JdCyK6zp2v6MWDcEppzIUdTVYcogLvQTwyHmjrWMIg6l5DoYXqXyCDEHZgXegLcNLmffMNP7Mhy4VL3Vdbl0s6tyPeYvaDKA__&Key-Pair-Id=APKAJLOHF5GGSLRBV4ZA
