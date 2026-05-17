# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : Bagaimana perbandingan kinerja YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia berdasarkan nilai confidence pada citra dari video CCTV?
Hypothesis        : YOLOv3 memiliki performa lebih baik dibandingkan YOLOv2 dalam mendeteksi dan menghitung manusia berdasarkan nilai confidence pada citra CCTV.
Tipe Eksperimen   : [✅] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Pengujian deteksi manusia menggunakan YOLOv2 | YOLOv2 | Dataset video CCTV yang sama, threshold 0.30, preprocessing dan environment yang sama |
| Treatment | Pengujian deteksi manusia menggunakan YOLOv3 | YOLOv3 | Dataset video CCTV yang sama, threshold 0.30, preprocessing dan environment yang sama |

Fairness Checklist:
  [✅] Dataset identik untuk semua kondisi
  [✅] Preprocessing setara
  [✅] Tuning effort setara
  [✅] Environment identik
  [✅] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Perbedaan parameter atau threshold dapat memengaruhi hasil deteksi | Menggunakan threshold dan parameter yang sama pada kedua model |
| External | Dataset hanya berasal dari CCTV lift sehingga kurang mewakili kondisi lain | Menggunakan variasi video CCTV dari kondisi berbeda jika memungkinkan |
| Construct | Nilai confidence belum sepenuhnya menggambarkan keseluruhan performa deteksi | Menambahkan metrik pendukung seperti jumlah objek terdeteksi dan processing time | Menggunakan jumlah objek terdeteksi sebagai metrik tambahan |
| Conclusion | Jumlah data uji terbatas dapat memengaruhi kesimpulan penelitian | Menambah jumlah data uji dan melakukan pengujian berulang |

Statistical Plan:
  Uji statistik    : Analisis perbandingan nilai confidence rata-rata
  Justifikasi      : Digunakan untuk melihat perbedaan performa kedua model pada kondisi yang sama
  Alpha            : 0.05
  Effect size min  : Perbedaan nilai confidence rata-rata yang menunjukkan peningkatan performa deteksi
```

---

## Latihan 1 — Desain Eksperimen

**RQ:** Bagaimana perbandingan kinerja YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia berdasarkan nilai confidence pada citra dari video CCTV?

**Tipe eksperimen:** [✅] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Pengujian menggunakan model YOLOv2 | YOLOv2 | Dataset video CCTV yang sama, threshold 0.30, preprocessing yang sama |
| Treatment | Pengujian menggunakan model YOLOv3 | YOLOv3 | Dataset video CCTV yang sama, threshold 0.30, preprocessing yang sama |

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | ✅ | Menggunakan dataset video CCTV yang sama untuk YOLOv2 dan YOLOv3 |
| Preprocessing setara | ✅ | Kedua metode menggunakan proses preprocessing yang sama pada dataset CCTV  |
| Tuning effort setara | ✅ | Kedua model menggunakan threshold yang sama yaitu 0.30 |
| Environment identik | ✅ | Pengujian dilakukan pada sistem dan environment yang sama |
| Metrik evaluasi sama | ✅ | Kedua metode dibandingkan menggunakan nilai confidence dan jumlah manusia yang terdeteksi |

**Ada yang tidak fair?** [ ] Ya / [✅] Tidak
> Karena kedua metode diuji menggunakan dataset, preprocessing, parameter, dan metrik evaluasi yang sama, maka perbandingan sudah dilakukan secara adil.

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Perbedaan hasil deteksi bisa dipengaruhi kondisi pengujian yang tidak sama | Menggunakan dataset, parameter, dan environment yang sama untuk YOLOv2 dan YOLOv3 |
| External | Dataset CCTV yang digunakan terbatas sehingga hasil belum tentu berlaku untuk semua kondisi nyata | Menggunakan variasi video CCTV dengan kondisi pencahayaan dan jumlah objek yang berbeda |
| Construct | Nilai confidence belum sepenuhnya menggambarkan keseluruhan performa deteksi | Menambahkan metrik pendukung seperti jumlah objek terdeteksi dan processing time |
| Conclusion | Jumlah data atau frame yang diuji terlalu sedikit sehingga hasil kurang kuat secara statistik | Menggunakan jumlah frame dan data uji yang lebih banyak agar hasil lebih valid |

**Ancaman mana yang paling sulit dimitigasi?** External validity
**Mengapa?**
> Karena dataset penelitian hanya berasal dari rekaman CCTV lift sehingga hasil penelitian belum tentu mewakili kondisi di tempat lain, seperti area ramai, pencahayaan berbeda, atau sudut kamera yang berbeda.
---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah semua metode diuji menggunakan dataset dan kondisi yang sama?
2. Apakah parameter dan preprocessing setiap metode dibuat setara dan adil?
3. Metrik evaluasi apa yang digunakan untuk membandingkan performa metode?

## Referensi
Pamungkas, B. P., Nugroho, B., & Anggraeny, F. (2021). Deteksi dan Menghitung Manusia Menggunakan YOLO-CNN. Jurnal Informatika dan Sistem Informasi (JIFoSI), 2(1), 67–76. https://www.semanticscholar.org/paper/Penggunaan-lift-pada-gedung-gedu-DETEKSI-DAN-Putra-Nugroho/0ff4c70d327624389d5197e2773db37e3816325d