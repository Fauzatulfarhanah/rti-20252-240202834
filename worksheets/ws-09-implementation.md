# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : Intel Xeon @ 2.20 GHz, 2 Core (dialokasikan otomatis oleh Google Colab)
  RAM     : 12.7 GB (Google Colab Standard Session)
  GPU     : NVIDIA Tesla T4, 15 GB VRAM (diaktifkan melalui Runtime → GPU)
  Storage : Google Drive 15 GB (menyimpan dataset, file konfigurasi, dan bobot model)

Software:
  OS        : Ubuntu 20.04 LTS (environment internal Google Colab)
  Runtime   : Python 3.10.12 
  Framework : Darknet (AlexeyAB Fork), dikompilasi dari source dengan opsi GPU=1, OPENCV=1, dan CUDNN=1
Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
| opencv-python | 4.8.0.76 | pip / PyPI | cek via: `pip hash opencv_python-4.8.0.76.whl` |
| numpy | 1.24.3 | pip / PyPI | cek via: `pip hash numpy-1.24.3.whl` |
| Pillow | 9.5.0 | pip / PyPI | cek via: `pip hash Pillow-9.5.0.whl` |
| matplotlib | 3.7.1 | pip / PyPI | cek via: `pip hash matplotlib-3.7.1.whl` |
| pandas | 2.0.3 | pip / PyPI | cek via: `pip hash pandas-2.0.3.whl` |
| Darknet | AlexeyAB Fork | GitHub | Git commit hash dicatat saat clone |

Konfigurasi:
  Config file     : YOLOv2.cfg dan yolov3_training.cfg yang disimpan pada folder `/MyDrive/YOLO_Research/config/`
  Random seed     : 42 (ditetapkan menggunakan `random.seed(42)` dan `numpy.random.seed(42)`)
  Hyperparameters : batch=64, subdivisions=16, width=416, height=416, learning_rate=0.001, max_batches=6000, threshold=0.30, classes=1 (person) 

Reproducibility Check:
  [✅] Dependency terdokumentasi (requirements.txt / lock file)
  [✅] Seed ditetapkan di semua level (Python, NumPy, framework)
  [✅] Config di version control
  [✅] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Lingkungan eksperimen dalam penelitian ini sepenuhnya berbasis cloud menggunakan Google Colaboratory. Pilihan ini diambil karena aksesibilitas GPU gratis, kemudahan integrasi dengan Google Drive sebagai tempat penyimpanan dataset dan bobot model, serta tidak memerlukan instalasi lokal yang kompleks.

| Komponen | Spesifikasi |
|-----------|------------|
| CPU | Intel Xeon @ 2.20 GHz, 2 Core (dialokasikan otomatis oleh Google Colaboratory) |
| RAM | 12.7 GB (Google Colaboratory Standard Session) |
| GPU | NVIDIA Tesla T4 dengan 15 GB VRAM (Google Colaboratory Free Tier) |
| Storage | Google Drive 15 GB untuk penyimpanan dataset, file konfigurasi, dan bobot model |
| OS | Ubuntu 20.04 LTS (environment internal Google Colaboratory) |
| Runtime | Python 3.10.12 |
| Framework | Darknet (AlexeyAB Fork) yang dikompilasi dari source code menggunakan dukungan GPU, OpenCV, dan cuDNN |
| Random Seed | 42 (ditetapkan pada Python `random` dan NumPy untuk menjaga konsistensi eksperimen) |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|----------|----------|-------------------|
| opencv-python | 4.8.0.76 | Melakukan pre-processing citra, visualisasi hasil deteksi, serta pengolahan frame video sebelum dan sesudah inferensi model. |
| numpy | 1.24.3 | Mendukung operasi numerik dan manipulasi array pada data citra serta perhitungan metrik evaluasi. |
| Pillow | 9.5.0 | Membaca, mengonversi, dan memanipulasi format file gambar yang digunakan dalam dataset. |
| matplotlib | 3.7.1 | Menampilkan grafik perbandingan hasil evaluasi antara YOLOv2 dan YOLOv3. |
| pandas | 2.0.3 | Mengelola, merekap, dan menyimpan hasil pengujian serta metrik evaluasi dalam bentuk tabel. |
| Google Colaboratory | Built-in | Menyediakan lingkungan komputasi berbasis cloud serta integrasi dengan Google Drive untuk penyimpanan dataset dan hasil eksperimen. |

---

## Latihan 2 — Repeatability Test Plan

Uji repeatability dilakukan dengan menjalankan inference YOLOv2 dan YOLOv3 masing-masing sebanyak 3 kali pada subset data uji yang sama (30 citra dari 150 total) tanpa mengubah konfigurasi apapun di antara setiap run.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|--------------|-------------|
| 1 | 42 | Confidence rata-rata (YOLOv2 & YOLOv3) | — (run pertama sebagai acuan) |
| 2 | 42 | Confidence rata-rata (YOLOv2 & YOLOv3) | [✅] Ya / [ ] Tidak |
| 3 | 42 | Confidence rata-rata (YOLOv2 & YOLOv3) | [✅] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**
> Perbedaan hasil antar-run pada Darknet paling sering disebabkan oleh dua hal: (1) alokasi GPU yang tidak sepenuhnya deterministik di Google Colab karena resource sharing dengan pengguna lain, dan (2) urutan pembacaan file gambar yang tidak dikunci secara eksplisit. Selain itu, sesi Colab yang terputus lalu dimulai ulang bisa mengubah versi driver GPU secara otomatis, yang dalam beberapa kasus mempengaruhi hasil komputasi floating point pada level desimal terakhir.

**Checklist kontrol yang sudah diterapkan:**
- [✅] Random seed di-set di semua level
- [✅] Tidak ada background process yang mengganggu
- [✅] Cache dibersihkan antar-run
- [✅] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Perbandingan YOLOv2 vs YOLOv3 untuk Deteksi dan Penghitungan Manusia pada Rekaman CCTV Lift


## 1. Environment
> | Komponen | Spesifikasi |
|-----------|------------|
| Platform | Google Colaboratory dengan dukungan GPU berbasis cloud |
| CPU | Intel Xeon @ 2.20 GHz, 2 Core |
| RAM | 12.7 GB |
| GPU | NVIDIA Tesla T4 dengan 15 GB VRAM |
| OS | Ubuntu 20.04 LTS (environment internal Google Colaboratory) |
| Runtime | Python 3.10.12 |
| Framework | Darknet (AlexeyAB Fork) yang dikompilasi dari source code dengan dukungan GPU, OpenCV, dan cuDNN |
| Random Seed | 42 untuk menjaga konsistensi hasil eksperimen |

## 2. Installation
> # Step 1 — Mount Google Drive
from google.colab import drive
drive.mount('/content/drive')

# Step 2 — Clone dan kompilasi Darknet (GPU + OpenCV aktif)
!git clone https://github.com/AlexeyAB/darknet
%cd darknet
!sed -i 's/OPENCV=0/OPENCV=1/' Makefile
!sed -i 's/GPU=0/GPU=1/' Makefile
!sed -i 's/CUDNN=0/CUDNN=1/' Makefile
!make

# Step 3 — Install dependencies Python
!pip install opencv-python==4.8.0.76
!pip install numpy==1.24.3
!pip install Pillow==9.5.0
!pip install matplotlib==3.7.1
!pip install pandas==2.0.3

---


## 3. Data
> ## 3. Data

### Sumber Data
Data penelitian berasal dari rekaman CCTV lift gedung bertingkat yang mengacu pada metodologi penelitian Pamungkas et al. (2021). Untuk mendukung proses pelatihan dan validasi model, digunakan pula subset kelas **person** dari COCO Dataset.

### Format Data

| Jenis Data | Format |
|------------|---------|
| Citra | `.jpg` |
| Label Anotasi | `.txt` (format YOLO) |
| Video | `.mp4`, 30 fps, durasi 10–30 detik per file |

### Ukuran Dataset

| Kategori | Jumlah |
|-----------|---------|
| Data Training | 1.500 citra hasil ekstraksi frame CCTV lift |
| Data Testing | 150 citra dan 10 video CCTV lift |
| Anotasi | Dibuat menggunakan LabelImg dalam format YOLO (`.txt`) |

### Struktur Penyimpanan Data

```text
/MyDrive/YOLO_Research/
├── dataset/
│   ├── train/
│   │   ├── images/
│   │   └── labels/
│   └── test/
│       ├── images/
│       ├── videos/
│       └── labels/
├── config/
│   ├── YOLOv2.cfg
│   └── yolov3_training.cfg
└── weights/
    ├── YOLOv2.weights
    └── yolov3_training_last.weights
```

## 4. Execution
> Inference YOLOv2 pada dataset testing
!./darknet detector test \
  /content/drive/MyDrive/YOLO_Research/config/YOLOv2.cfg \
  /content/drive/MyDrive/YOLO_Research/weights/YOLOv2.weights \
  /content/drive/MyDrive/YOLO_Research/dataset/test/ \
  -thresh 0.30 \
  -dont_show \
  -save_labels

# Inference YOLOv3 pada dataset testing yang sama
!./darknet detector test \
  /content/drive/MyDrive/YOLO_Research/config/yolov3_training.cfg \
  /content/drive/MyDrive/YOLO_Research/weights/yolov3_training_last.weights \
  /content/drive/MyDrive/YOLO_Research/dataset/test/ \
  -thresh 0.30 \
  -dont_show \
  -save_labels

Kedua command dijalankan secara terpisah dalam sesi yang sama
tanpa restart runtime di antara keduanya.

## 5. Configuration
> File konfigurasi yang digunakan:

YOLOv2.cfg — parameter kunci:
  - batch          = 64
  - subdivisions   = 16
  - width          = 416
  - height         = 416
  - threshold      = 0.30 (saat inference)
  - classes        = 1 (hanya kelas "person")

yolov3_training.cfg — parameter kunci:
  - batch          = 64
  - subdivisions   = 16
  - width          = 416
  - height         = 416
  - threshold      = 0.30 (saat inference)
  - classes        = 1 (hanya kelas "person")

Random seed   : numpy.random.seed(42), random.seed(42)
Version ctrl  : Semua file config disimpan di Google Drive
                dengan revision history aktif.

---

## 6. Expected Output
> Format output per model:
  - File .txt per gambar berisi prediksi bounding box
    (kelas, confidence, koordinat x, y, w, h)
  - Log confidence per objek terdeteksi di terminal Colab
  - Jumlah objek terdeteksi per frame (People Count)

Contoh output YOLOv3 (berdasarkan Pamungkas et al., 2021):
  person: 99%  →  {"x": 190, "y": -3}   →  {"x": 121, "y": 269}
  person: 98%  →  {"x": 303, "y": 8}    →  {"x": 125, "y": 248}
  People Count: 4

Contoh output YOLOv2 (berdasarkan Pamungkas et al., 2021):
  person: 77%  →  bounding box
  person: 72%  →  bounding box
  People Count: 3

Seluruh hasil disalin ke spreadsheet rekap metrik dengan kolom:
[Model | Skenario | Confidence | Precision | Recall | F1 | IoU | Waktu (detik)]
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?
> Untuk saat ini, eksperimen ini sudah bisa di-*repeat* oleh saya sendiri di environment yang sama, tapi belum bisa direproduksi sepenuhnya oleh orang lain secara mandiri. Ada dua hal yang jadi kendalanya. Pertama, dataset rekaman CCTV lift belum tersedia secara publik karena bersumber dari konteks penelitian sebelumnya (Pamungkas et al., 2021), jadi orang lain tidak bisa langsung mengakses data yang persis sama. Kedua, proses kompilasi Darknet di Google Colab bisa sedikit berbeda tergantung versi CUDA dan driver GPU yang dialokasikan saat itu, dan ini di luar kendali peneliti.

> Yang sudah cukup siap untuk direproduksi adalah seluruh pipeline inference-nya — konfigurasi model, bobot, threshold, langkah pre-processing, dan cara menghitung metrik sudah terdokumentasi di README di atas. Siapapun yang punya dataset serupa bisa mengikuti langkah yang sama dan mendapatkan hasil yang setara.

**Level saat ini:** [✅] Repeatability / [ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Dataset primer berupa rekaman CCTV lift belum bisa dibagikan secara publik karena bersumber dari penelitian rujukan. Untuk mencapai level reproducibility penuh, langkah berikutnya adalah menyiapkan subset data sampel yang bisa dibagikan, atau menjadikan subset COCO Dataset kelas "person" sebagai data pengganti yang memang sudah tersedia secara publik dan bebas diakses siapapun.
