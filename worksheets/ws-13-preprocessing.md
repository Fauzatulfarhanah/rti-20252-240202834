# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset           : Rekaman CCTV lift — Pilot Test 4 citra
                   (download.jpg, @jaoyng on instagram.jpg,
                    leonel lara.jpg, amigos.jpg)
Jumlah data awal  : 4 citra (input gambar)
                   25 bounding box hasil deteksi (output Darknet)
                   — rincian: 22 deteksi kelas "person" +
                              3 deteksi kelas non-person dari leonel lara
                              + 3 deteksi kelas non-person dari amigos
                   Total raw deteksi: 28 bounding box

---

LAPISAN 1 — IMAGE PREPROCESSING (Input ke Model YOLO)

Cleaning:
| Masalah         | Jumlah Kasus  | Penanganan              | Justifikasi                                      |
|-----------------|---------------|-------------------------|--------------------------------------------------|
| Format gambar   | 0 kasus       | Tidak ada — semua .jpg  | Darknet mendukung .jpg langsung                  |
| Resolusi berbeda| 4 dari 4 citra| Resize otomatis Darknet | Semua gambar diubah ke 416×416 px saat inference |
| Missing file    | 0 kasus       | —                       | Semua 4 file berhasil terbaca dan dieksekusi      |

Transformation:
| Transformasi            | Variabel    | Detail                        | Alasan                                          |
|-------------------------|-------------|-------------------------------|-------------------------------------------------|
| Resize                  | Citra input | Semua gambar → 416×416 px     | Ukuran input wajib sesuai konfigurasi YOLOv3    |
| Konversi warna          | Citra input | RGB → dilakukan internal YOLO | Darknet memproses channel secara otomatis       |
| Pixel value scaling     | Nilai piksel| [0, 255] → [0.0, 1.0] (auto) | Dilakukan internal Darknet saat inference       |

Normalization (Lapisan 1):
  Metode    : Pixel normalization otomatis oleh Darknet ([0,255] → [0.0,1.0])
  Alasan    : Diperlukan oleh arsitektur YOLOv3 agar nilai input konsisten
              dengan bobot yang telah dilatih
  Parameter : Dihitung dari training set (sudah baked-in di dalam file
              yolov3_training_last.weights) — tidak dihitung ulang dari test set

---

LAPISAN 2 — RESULT PREPROCESSING (Output Darknet → Data Analisis)

Cleaning:
| Masalah                        | Jumlah Kasus | Penanganan                              | Justifikasi                                                                   |
|--------------------------------|--------------|-----------------------------------------|-------------------------------------------------------------------------------|
| Deteksi kelas non-person       | 6 dari 28 BB | Filter — hanya simpan kelas "person"    | Fokus penelitian adalah people counting; bottle, cell phone, book, handbag    |
|                                |              |                                         | tidak relevan untuk variabel dependen DV2 (akurasi penghitungan manusia)      |
| Deteksi confidence < threshold | 0 kasus      | Tidak ada — threshold 0.30 sudah aktif  | Darknet sudah memfilter otomatis saat inference dengan -thresh 0.30;           |
|                                |              |                                         | semua output yang muncul di log sudah di atas threshold                       |
| Duplikat bounding box          | 0 kasus      | Tidak ada                               | Non-Max Suppression (NMS) sudah dijalankan otomatis oleh Darknet              |
|                                |              |                                         | sebelum output muncul — tidak ada double-detection pada objek yang sama       |
| Format confidence (% vs desimal)| 22 deteksi  | Konversi: % → desimal (misal 96% → 0.96)| Agar konsisten dengan standar metrik penelitian yang menggunakan rentang 0–1 |

Transformation:
| Transformasi          | Variabel              | Detail                               | Alasan                                              |
|-----------------------|-----------------------|--------------------------------------|-----------------------------------------------------|
| Filter kelas          | Semua bounding box    | Hapus non-person, pertahankan person | Menjaga fokus pada variabel dependen DV2            |
| Konversi satuan waktu | Waktu inferensi       | Milidetik → detik (÷ 1000)          | Standarisasi satuan untuk tabel perbandingan        |
| Kelompokkan per skenario | Semua deteksi      | Rendah / Sedang / Tinggi             | Menyiapkan data untuk analisis per-skenario (RQ4)   |

Normalization (Lapisan 2):
  Metode    : Tidak diperlukan
  Alasan    : Confidence score sudah dalam rentang [0,1] — tidak perlu
              min-max atau z-score. Waktu inferensi dibandingkan langsung
              dalam satuan yang sama (ms atau detik). Normalisasi justru
              akan menghilangkan makna absolut dari nilai confidence
              (misal: 96% vs 61% adalah informasi penting yang tidak boleh
              dinormalisasi menjadi 1.0 vs 0.0).

Leakage Check:
  [x] Parameter normalisasi dari training set saja
      (pixel normalization sudah baked-in di weights, bukan dihitung
       ulang dari test images)
  [x] Tidak ada informasi test set dalam preprocessing
      (ground truth tidak digunakan untuk menentukan threshold atau
       parameter preprocessing — threshold 0.30 ditetapkan sebelum
       inference dimulai)
  [x] Cross-validation dilakukan setelah split
      (tidak relevan untuk inference YOLO — tidak ada cross-validation
       dalam desain eksperimen komparatif ini)

Jumlah data awal  : 28 bounding box (22 person + 6 non-person)
Jumlah data akhir : 22 bounding box kelas "person" — siap untuk analisis
Persentase dibuang: 6/28 = 21.4% (semua non-person, bukan data error)
Script tersedia   : [x] Ya → Darknet flag: -thresh 0.30 (filtering otomatis)
                   Filter manual non-person dilakukan saat rekap spreadsheet
```

---

## Latihan 1 — Cleaning Plan

> **Konteks:** Cleaning dilakukan pada output hasil deteksi Darknet (28 bounding box),
> bukan pada gambar input. Gambar input sudah bersih dan valid — tidak ada missing,
> duplikat, atau error format pada level input.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Deteksi kelas non-person (bottle, cell phone, book, handbag) | 6 dari 28 bounding box (21.4%) | Filter — keluarkan dari analisis people counting, dokumentasikan sebagai catatan terpisah | Kelas non-person tidak relevan untuk DV2 (akurasi penghitungan manusia). Kemunculannya disebabkan bobot COCO 80 kelas, bukan error model |
| Deteksi confidence di bawah threshold 0.30 | 0 kasus | Tidak diperlukan | Sudah difilter otomatis oleh Darknet dengan flag -thresh 0.30 sebelum output ditulis |
| Duplikat bounding box (double detection objek sama) | 0 kasus | Tidak diperlukan | Non-Max Suppression (NMS) berjalan otomatis di dalam pipeline Darknet |
| Format confidence tidak konsisten (% vs desimal) | 22 deteksi person | Standarisasi ke desimal: bagi 100 (misal 96% → 0.96) | Konsistensi dengan standar pelaporan metrik confidence [0,1] dalam literatur |

**Jumlah data sebelum cleaning:** 28 bounding box
**Jumlah data setelah cleaning:** 22 bounding box (hanya kelas person)
**Persentase data yang dibuang:** 21.4% (6 bounding box non-person)

> **Catatan penting:** Data yang "dibuang" bukan data error — melainkan deteksi yang
> valid tapi tidak relevan untuk variabel dependen penelitian ini. Keputusan ini
> terdokumentasi agar orang lain bisa memahami mengapa angkanya berbeda dari total
> raw output Darknet.

---

## Latihan 2 — Normalisasi Decision

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|-----------|-----------|----------|-------------------|--------|
| Confidence score (person) | 34% – 100% (0.34 – 1.00) | Tidak normal — tergantung skenario; bimodal (skenario padat vs normal) | Ya — @jaoyng 60.9% vs download 96.5% | Tidak perlu normalisasi | Sudah dalam [0,1]. Nilai absolutnya bermakna: 60.9% vs 96.5% adalah temuan penelitian yang tidak boleh diratakan |
| Waktu inferensi | 86.079 ms – 102.328 ms | Relatif sempit dan normal | Tidak | Tidak perlu normalisasi | Dibandingkan langsung dalam satuan ms atau detik; skala sama antar model |
| Jumlah person terdeteksi | 3 – 11 orang | Tergantung gambar | Tidak (dalam konteks skenario masing-masing) | Tidak perlu normalisasi | Dibandingkan dengan ground truth per gambar secara langsung |
| Piksel gambar input (internal Darknet) | [0, 255] per channel | — | — | Otomatis oleh Darknet → [0.0, 1.0] | Diperlukan agar nilai piksel konsisten dengan bobot YOLOv3 yang sudah dilatih |

**Apakah normalisasi diperlukan?** [ ] Ya untuk data hasil / [x] Tidak — kecuali pixel normalisasi internal Darknet yang sudah otomatis

**Justifikasi:**
> Ketiga variabel dependen (confidence, waktu inferensi, jumlah person) sudah berada
> dalam skala yang dapat dibandingkan secara langsung tanpa normalisasi tambahan.
> Confidence sudah dalam [0,1], waktu dalam ms dengan satuan yang sama untuk kedua
> model, dan jumlah person adalah bilangan bulat yang dibandingkan dengan ground truth.
> Melakukan normalisasi pada variabel-variabel ini justru akan menghilangkan makna
> absolutnya — misalnya, jika confidence dinormalisasi menjadi [0,1] dari range 34–100%,
> nilai 60.9% akan menjadi ~0.38 yang terlihat "rendah", padahal dalam konteks penelitian
> ini 60.9% masih jauh di atas threshold minimum 30%.

**Leakage check:**
- [x] Parameter dihitung dari training set saja — pixel normalisasi sudah baked-in di weights
- [x] Normalisasi diterapkan setelah train-test split — inference dilakukan pada test images yang terpisah dari training

---

## Latihan 3 — Preprocessing Report

```
PREPROCESSING SUMMARY

1. Dataset: Output deteksi YOLOv3 dari pilot test 4 citra CCTV
            (download.jpg, @jaoyng on instagram.jpg,
             leonel lara.jpg, amigos.jpg)

2. Data awal: 28 bounding box total (22 kelas person + 6 kelas lain)
              dari 4 gambar uji

3. Cleaning:
   - Non-person detections: 6 kasus
     → Filter, keluarkan dari analisis people counting
     → Dokumentasikan terpisah sebagai catatan observasi
   - Confidence < threshold: 0 kasus (sudah difilter Darknet otomatis)
   - Duplikat bounding box : 0 kasus (NMS sudah berjalan di Darknet)
   - Format tidak konsisten : 22 kasus confidence dalam format %
     → Standarisasi ke desimal (bagi 100)

4. Transformation:
   - Filter kelas non-person → 22 bounding box person dipertahankan
   - Konversi waktu: ms → detik (÷ 1000) untuk tabel perbandingan
   - Pengelompokan per skenario: Rendah (download), Sedang (leonel +
     amigos), Tinggi (@jaoyng) → menyiapkan data untuk analisis RQ4

5. Normalisasi:
   - Hasil deteksi (confidence, waktu, count): TIDAK dinormalisasi
     → Nilai absolut bermakna untuk perbandingan langsung
   - Piksel gambar input: normalisasi [0,255]→[0.0,1.0] dilakukan
     otomatis oleh Darknet (parameter baked-in di weights file)

6. Data akhir: 22 bounding box kelas "person", siap untuk perhitungan
               confidence rata-rata, precision, recall, F1-score, IoU,
               dan waktu inferensi per skenario

7. Leakage check: [x] Lulus
   — Parameter normalisasi sudah di dalam weights (training set)
   — Tidak ada informasi test set yang masuk ke preprocessing
   — Threshold 0.30 ditetapkan sebelum inference, bukan setelah
```

---

## Refleksi

> **Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?**

> Sebenarnya iya. waktu pertama kali belajar machine learning, saya selalu menormalisasi semua data ke [0,1] karena "begitu yang diajarkan." Tidak pernah benar-benar bertanya apakah memang perlu untuk kasus spesifik yang sedang dikerjakan.
>
> Di penelitian ini jadi lebih sadar. Kalau confidence score dinormalisasi, nilai 60.9% pada gambar @jaoyng dan 96.5% pada download akan menjadi angka lain yang kehilangan konteksnya. Padahal selisih 35.6% itulah yang menjadi temuan penting — bahwa YOLOv3 mengalami penurunan confidence yang signifikan pada skenario padat, dan ini relevan langsung dengan hipotesis H4 tentang pengaruh kepadatan terhadap performa model.
>
> Risiko over-preprocessing dalam penelitian komparatif seperti ini lebih berbahaya dari yang terlihat. Kalau waktu inferensi (86–102ms) dinormalisasi, kedua model akan terlihat "sama cepat" karena range-nya sudah dipersempit. Padahal dalam konteks real-time, perbedaan beberapa puluh milidetik antara YOLOv2 dan YOLOv3 bisa jadi faktor penentu apakah sistem bisa dipakai di perangkat dengan GPU terbatas. Normalisasi yang tidak perlu bisa menyembunyikan perbedaan yang sebenarnya bermakna secara praktis.
