# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [x] Semua skenario tercakup
  [x] Jumlah run sesuai rencana
  [ ] Tidak ada file output hilang
  Missing: 1 dari 6 data points

Format Consistency:
  [x] Semua file format sama (TXT/Log Terminal Darknet)
  [x] Header konsisten
  [x] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [x] Nilai dalam range masuk akal
  [x] Tidak ada waktu negatif
  [x] Metrik 0–100%, tidak di luar range
  Anomali ditemukan: Glitch IO pada video stream OpenCV Colab yang menyebabkan infinite loop ("Video-stream stopped!") sehingga file output video .mp4 gagal digenerate.

Cross-Validation:
  [x] Run identik → hasil mendekati
  [x] Trend konsisten dengan ekspektasi teori

Keputusan:
  [ ] Data siap analisis
  [ ] Perlu cleaning
  [x] Perlu re-run (skenario: Alokasi ulang runtime OpenCV untuk eksekusi video dinamis hasil_deteksi_video.mp4)

```

---

## # Laporan Validasi Data Eksperimen (WS-11)

## Latihan 1 — Completeness Check
Verifikasi apakah semua data yang direncanakan sudah terkumpul.

### Tabel Kelengkapan Run Eksperimen
| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
| :--- | :---: | :---: | :---: | :--- |
| **YOLOv3 — Kepadatan Rendah**<br>*(download.jpg / download.webp)* | 3 | 3 | 0 | — |
| **YOLOv3 — Kepadatan Tinggi**<br>*(@jaoyng on instagram.jpg)* | 3 | 3 | 0 | — |
| **YOLOv3 — Kepadatan Sedang**<br>*(leonel lara.jpg)* | 3 | 3 | 0 | — |
| **YOLOv3 — Kepadatan Sedang**<br>*(amigos.jpg)* | 3 | 2 | 1 | Log terminal Google Colab terpotong sebelum output *confidence score* dan *people count* muncul di layar. |
| **YOLOv3 — Objek Dinamis**<br>*(hasil_deteksi_video.mp4)* | 1 | 0 | 1 | Interupsi *infinite loop* pada pustaka OpenCV runtime Google Colab (*"Video-stream stopped!"*). |
| **Total** | **13** | **11** | **2** | |

* **Total expected:** 13
* **Total actual:** 11
* **Missing:** 2

### Keputusan untuk Data Missing:
* **Run `amigos.jpg` yang log-nya terpotong:** Tidak dihapus dari catatan eksperimen. Data ke-2 run yang berhasil tetap disimpan dan didokumentasikan sebagai run yang valid. Untuk melengkapi data yang missing, akan dilakukan *re-run* pada sesi Colab berikutnya dengan menggunakan konfigurasi penulisan output langsung ke file `.txt` agar tidak bergantung pada batas tampilan log terminal.
* **Skenario video dinamis (`hasil_deteksi_video.mp4`) & 9 run YOLOv2 yang tertunda:** Akan dijalankan ulang setelah restrukturisasi *environment* OpenCV selesai, menggunakan dataset, *threshold*, dan skenario yang identik dengan rencana awal.

---

## Latihan 2 — Anomaly Investigation
Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

### Dataset Sampel (Data Eksperimen):
| Run | Confidence Rata-rata (%) | Sumber Gambar & Seed |
| :---: | :---: | :--- |
| 1 | 96.5% | `download.jpg` (Run 1) — seed 42 |
| 2 | 96.2% | `download.jpg` (Run 2) — seed 42 |
| 3 | 96.8% | `download.jpg` (Run 3) — seed 42 |
| 4 | 60.9% | `@jaoyng on instagram.jpg` (Run 1) — seed 42 |
| 5 | 61.2% | `@jaoyng on instagram.jpg` (Run 2) — seed 42 |

### Deteksi Outlier (Metode IQR):
* **Data Diurutkan (Kecil ke Besar):** 60.9 — 61.2 — 96.2 — 96.5 — 96.8
* **Kuartil:** 
  * $Q_1 = 61.05$
  * $Q_3 = 96.65$
  * $IQR = 35.60$
* **Batas Batas:**
  * Batas bawah ($Q_1 - 1.5 \times IQR$) = $61.05 - 53.40 = 7.65$
  * Batas atas ($Q_3 + 1.5 \times IQR$) = $96.65 + 53.40 = 150.05$

**Hasil Deteksi Outlier:**  
Tidak ada outlier statistik — semua nilai berada di antara rentang 7.65 dan 150.05. Namun, **Run 4 (60.9%)** dan **Run 5 (61.2%)** tergolong ke dalam ***contextual anomaly*** karena nilainya jauh di bawah rata-rata keseluruhan dataset (82.3%). Hal ini terjadi bukan karena error sistem, melainkan karena kondisi kepadatan gambar yang berbeda secara signifikan.

### Tabel Investigasi Anomali
| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
| :--- | :---: | :--- | :--- |
| **Run 4 & 5**<br>*(@jaoyng on instagram.jpg)* | 60.9% & 61.2% | Gambar berisi 11 orang yang saling berdekatan dan sebagian tubuhnya saling menutupi (*occlusion*), sehingga model sulit memisahkan batas antar-objek dan menghasilkan *confidence* lebih rendah pada banyak deteksi. Ini bukan *bug*, melainkan perilaku nyata model saat menghadapi kepadatan tinggi. | Dokumentasikan sebagai temuan valid yang relevan dengan tujuan penelitian. Perbedaan *confidence* antara skenario padat dan normal justru menjadi poin pembahasan utama dalam perbandingan YOLOv2 vs YOLOv3. |
| **Run `amigos.jpg`** | Output tidak terbaca | Ukuran atau kompleksitas gambar menyebabkan *inference* melampaui batas alokasi tampilan log terminal Colab. | *Re-run* dengan sistem pencatatan terisolasi. Run yang sempat gagal atau terpotong tetap dicatat dalam log integritas data, tidak dihapus begitu saja. |

---

## Latihan 3 — Validation Report
Buat laporan validasi ringkas untuk dataset eksperimen Anda.

1. **Completeness:** **84.6%** data run utama terkumpul (11 dari 13 run YOLOv3 berhasil tercatat; 1 run `amigos.jpg` dan 1 run video dinamis memerlukan proses *re-run* akibat kendala teknis IO; 9 run YOLOv2 dijadwalkan pada sesi berikutnya).
2. **Format:**  
   - [x] **Konsisten** — seluruh output citra statis menggunakan format log teks terminal Darknet yang seragam; tidak ada perbedaan struktur output antar-run gambar yang berhasil.
3. **Range Check (Anomali):** Semua nilai *confidence* berada pada rentang 34%–100%, di dalam batas valid $[0, 1]$. Tidak ada nilai negatif atau melebihi 100%. Nilai terendah (34%) masih di atas *threshold* 0.30 yang ditetapkan di desain eksperimen, sehingga tetap dihitung sebagai deteksi valid. Dua anomali ditemukan dan sudah didokumentasikan:
   - (1) Log `amigos.jpg` terpotong (*format anomaly*)
   - (2) Rata-rata *confidence* `@jaoyng.jpg` 60.9% vs 93–96% skenario lain (*contextual anomaly* yang merupakan karakteristik performa model, bukan error).
4. **Logic Check:**  
   - [x] **Parameter sesuai plan** — *threshold* 0.30 digunakan konsisten di semua run, file konfigurasi dan bobot *pre-trained* tidak berubah antar-run gambar, dan seluruh objek uji identik dengan perancangan di WS-10.

**Kesimpulan:**  
- [ ] Data siap analisis  
- [x] **Perlu tindakan:** *Re-run* pada run `amigos.jpg` yang terpotong serta penjadwalan ulang alokasi library video OpenCV untuk eksekusi berkas `hasil_deteksi_video.mp4` agar analisis komparatif performa objek statis dan dinamis bisa disajikan secara utuh.

---

## Refleksi

### Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

* **"Data yang benar"** artinya nilainya mencerminkan kondisi nyata hasil komputasi — misalnya nilai *confidence* 96.5% memang benar-benar menunjukkan tingkat keyakinan arsitektur YOLOv3 saat mendeteksi objek manusia di dalam lift. 
* **"Data yang dipercaya"** adalah data yang sudah melewati proses verifikasi formal sehingga peneliti yakin tidak ada bagian yang hilang, tidak ada format yang inkonsisten, dan tidak ada nilai yang berada di luar logika desain eksperimen. Data bisa saja benar secara angka mentah, namun belum bisa dipercaya untuk ditarik menjadi kesimpulan ilmiah sebelum divalidasi integritasnya.

Dalam praktikum ini, *framework* Darknet mencatat output secara otomatis lewat log runtime terminal. Namun ternyata proses "otomatis" tidak menjamin data aman dari masalah teknis — kasus terpotongnya log pada `amigos.jpg` serta kegagalan *stream* internal OpenCV pada file video membuktikannya. Tanpa adanya *completeness check* seperti yang dilakukan di WS-11 ini, data yang cacat atau hilang bisa saja masuk ke tahap analisis Bab 4 tanpa disadari dan merusak akurasi riset. 

Selain itu, validasi formal membantu mengklasifikasikan mana data yang benar-benar error sistem dan mana data yang merupakan anomali kontekstual hasil penelitian; penurunan rata-rata *confidence* pada `@jaoyng on instagram.jpg` awalnya tampak mencurigakan, namun setelah diinvestigasi terbukti bahwa itu merupakan respon riil arsitektur terhadap efek tumpang tindih (*occlusion*) pada kerumunan padat lift, yang justru menjadi poin diskusi esensial dalam penelitian ini.