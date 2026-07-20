# Tahap 1 — Perancangan Lingkungan Eksperimen & Struktur Data

**Status:** Selesai

---

## 1. Komponen Lingkungan Eksperimen

1. **Google Colab (Python Script Runtime)** — Berfungsi sebagai *environment* utama untuk mengeksekusi skrip otomasi pengujian, membaca *dataset* uji via `os.listdir()`, memicu perintah eksternal Darknet, serta menampilkan visualisasi hasil deteksi via `cv2_imshow()`.
2. **Framework Darknet Engine (`!./darknet`)** — Komponen *core* visi komputer berbasis C yang bertindak sebagai mesin inferensi *one-stage detector*. Berfungsi melakukan prapemrosesan gambar (pemotongan/skala otomatis) dan komputasi matriks *layer* syaraf tiruan.
3. **GPU Tesla T4 (Hardware Accelerator)** — Akselerator perangkat keras berbasis CUDA yang disediakan oleh *runtime* Colab untuk mempercepat proses kalkulasi tensor grafis dan menangani beban operasi BFLOPS yang besar dari model.
4. **Google Drive Storage (Persistent Repository)** — Bertindak sebagai pengganti database tradisional (Source of Truth) untuk menyimpan seluruh artefak permanen eksperimen: berkas konfigurasi arsitektur (`.cfg`), bobot jaringan (*weights*), serta direktori citra latih dan citra uji kunci.

---

## 2. Alur Proses Inferensi & Resolusi Objek

Citra Uji CCTV Lift Masuk (Raw Image)

│
├─ Script Python membaca file dari `/dataset/test/` via `os.listdir()`
│
├─ Prapemrosesan Otomatis oleh Darknet Engine
│     └─ Dimensi citra di-*resize* otomatis secara konsisten ke 416x416 piksel
│
├─ Percabangan Komparasi Arsitektur Model (Kondisi Eksperimen)
│     ├─ KONDISI A (YOLOv2) → Alokasi beban ke GPU untuk komputasi dangkal (Darknet-19 | 29.475 BFLOPS)
│     └─ KONDISI B (YOLOv3) → Alokasi beban ke GPU untuk komputasi dalam (Darknet-53 | 65.879 BFLOPS)
│
├─ Resolusi Deteksi oleh GPU Tesla T4
│     └─ Pencarian objek manusia → Ekstraksi koordinat Bounding Box & Confidence Score
│
├─ Ekspor Cache Lokal Virtual Machine
│     └─ Darknet menulis hasil visualisasi ke berkas runtime tunggal `predictions.jpg`
│
└─ Output Visualisasi Colab
      └─ Script memuat `predictions.jpg` via `cv2.imread()` → Tampil di layar via `cv2_imshow()`

### Mekanisme Ketahanan Eksperimen (Fail-Safe Rules)

* **Fail-Open (Runtime Reconnection):** Jika koneksi *runtime* Google Colab terputus akibat batas waktu (*timeout*), skrip Python dirancang untuk mampu melakukan pemulihan (*checkpointing*). Sistem akan otomatis membaca ulang file bobot pelatihan terakhir dari direktori `backup/` di Google Drive sehingga pengujian tidak perlu diulang dari *epoch* awal.
* **Fail-Closed (Inference Rejection):** Jika file citra uji mengalami kerusakan piksel (*corrupted file*) atau berkas `.weights` tidak terbaca sempurna oleh Darknet Engine, sistem pengujian akan langsung memicu eror *fatal stop* (menghentikan proses secara paksa). Hal ini dilakukan untuk menghindari keluarnya nilai prediksi acak yang dapat merusak validitas metrik *Precision*, *Recall*, dan *IoU*.

---

## 3. Skema Struktur Data Eksperimen (Google Drive Storage)

Sebagai pengganti skema database relasional tradisional, seluruh konfigurasi jaringan dan data visual diatur menggunakan struktur direktori objek terisolasi pada Google Drive demi menjamin validitas dan replikasi pengujian:

```text
📁 MyDrive/
└── 📁 RTI/
    ├── 📁 darknet/                 # Source-code kompilasi utama Darknet Framework
    ├── 📁 backup/                  # Tempat penyimpanan file bobot (.weights) hasil pelatihan
    │   ├── 📄 yolov2.weights       # Bobot siap uji untuk model Baseline
    │   └── 📄 yolov3_training_last.weights # Bobot siap uji untuk model Intervensi
    ├── 📁 cfg/                     # Berkas konfigurasi struktur arsitektur jaringan
    │   ├── 📄 yolov2.cfg           # Jaringan syaraf tiruan berbasis Darknet-19
    │   └── 📄 yolov3_training.cfg  # Jaringan syaraf tiruan berbasis Darknet-53
    └── 📁 dataset/
        ├── 📁 train/               # 1.500 citra latih + berkas anotasi koordinat (.txt)
        └── 📁 test/                # 4 Citra karakteristik uji kunci (Ground Truth Terkunci)
            ├── 📄 amigos.jpg
            ├── 📄 download.jpg
            ├── 📄 leonel lara.jpg
            └── 📄 @jaoyng on instagram.jpg
```

## 4. Skema Penyimpanan Sementara (Runtime Cache VM)

| Nama Berkas Cache | Format / Tipe | Lokasi Penyimpanan | Tujuan Eksperimen |
|-------------------|---------------|--------------------|-------------------|
| predictions.jpg | Citra Kompresi (JPEG) | `/content/` (Local VM Cache) | Menyimpan visualisasi bounding box dan nilai confidence score objek manusia dari satu iterasi frame sebelum ditimpa oleh frame berikutnya. |

## 5. Keputusan Teknis (Final)

**Mode Eksperimen:** Desain komparatif *apple-to-apple* langsung antara model Baseline (Kondisi A: YOLOv2) melawan Intervensi (Kondisi B: YOLOv3) untuk mengukur diferensiasi nilai performa metrik akurasi dan waktu komputasi (D_{perf}).

**Framework Utama:** Darknet Framework berbasis C (dikompilasi langsung di dalam arsitektur Linux Google Colab).

**Dimensi Resolusi Input:** Semua gambar uji diseragamkan dan dikunci pada resolusi 416x416 piksel melalui modifikasi parameter baris *width* dan *height* pada masing-masing file `.cfg`.

**Parameter Ambang Batas Deteksi:** Nilai batas bawah penerimaan objek (*confidence threshold*) dikunci secara ketat pada parameter `-thresh 0.30` untuk semua sesi pengujian citra lift.

**Akselerasi Perangkat Keras:** Menggunakan arsitektur komputasi awan tunggal dengan spesifikasi GPU Tesla T4 untuk meminimalkan bias eksternal pada perhitungan durasi waktu inferensi.

**Data Uji Karakteristik Kunci:** Validasi akhir performa model difokuskan pada 4 citra uji spesifik (`amigos.jpg`, `download.jpg`, `leonel lara.jpg`, `@jaoyng on instagram.jpg`) yang mencerminkan tantangan nyata oklusi dan kepadatan ruang lift.

**Pustaka Visualisasi:** Menggunakan kombinasi pustaka OpenCV (Python) untuk penanganan pembacaan matriks gambar (`cv2.imread`) dan fungsi internal Colab patches (`cv2_imshow`) untuk merender matriks citra ke layar.