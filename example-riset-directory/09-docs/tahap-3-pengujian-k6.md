# Tahap 3 — Konfigurasi Lingkungan, Kalibrasi, dan Skrip Otomatisasi Pengujian (YOLOv2 vs YOLOv3)

**Status:** Selesai — Seluruh alur penyiapan environment, perbaikan kompilasi, hingga skrip looping pengujian otomatis untuk YOLOv2 dan YOLOv3 telah berhasil dieksekusi di Google Colab.  
**Bergantung pada:** Akselerasi Hardware GPU (NVIDIA Tesla T4 di Google Colab)  
**Lokasi Penyimpanan Data:** Google Drive (`/content/drive/MyDrive/RTI/`)

---

## Tujuan

Menyiapkan lingkungan kerja framework Darknet berbasis GPU dan menyusun skrip looping otomatis (Python) untuk menguji serta membandingkan performa model YOLOv2 (Baseline) vs YOLOv3 (Intervensi). Pengujian dilakukan terhadap variasi citra di dalam lift berdasarkan tiga skenario kepadatan objek manusia:

- **Kepadatan Rendah:** Citra dengan jumlah objek sedikit (1-2 orang) tanpa halangan.
- **Kepadatan Sedang:** Citra dengan jumlah objek beberapa orang (3-4 orang) dengan sedikit halangan/oklusi.
- **Kepadatan Tinggi:** Citra dengan kondisi ramai (≥ 5 orang) dan objek saling bertumpukan/terhalang ekstrem.

## Deliverable Praktikum

- [x] Integrasi Cloud: Menghubungkan Google Colab dengan direktori penyimpanan Google Drive.
- [x] Kompilasi Jaringan: Modifikasi berkas Makefile untuk mengaktifkan fitur GPU, OpenCV, dan cuDNN.
- [x] Audit Pustaka: Pemeriksaan versi dependensi Python (`cv2`, `numpy`, `PIL`, `matplotlib`, `pandas`).
- [x] Solusi Eror (Troubleshooting): Pembersihan sisa build yang gagal dengan `!make clean` sebelum kompilasi ulang berhasil.
- [x] Uji Jalur Data (Smoke Test): Kalibrasi awal menggunakan gambar `dog.jpg` dan uji coba satu `manusia.jpg`.
- [x] Otomatisasi YOLOv3: Skrip perulangan Python untuk mendeteksi seluruh isi folder gambar uji menggunakan model YOLOv3.
- [x] Otomatisasi YOLOv2: Skrip perulangan Python untuk mendeteksi seluruh isi folder gambar uji menggunakan model YOLOv2.

## Desain & Struktur Direktori Praktikum

Semua berkas bobot (*weights*), konfigurasi (`.cfg`), dan citra uji diletakkan di dalam Google Drive agar tidak hilang saat session Colab terputus:

```text
/content/drive/MyDrive/RTI/
├── config/
│   ├── YOLOv2.cfg                   # Arsitektur model YOLOv2 (matriks 416 x 416)
│   └── yolov3_training.cfg          # Arsitektur model YOLOv3 (matriks 416 x 416)
├── weights/
│   ├── YOLOv2.weights               # Bobot standar YOLOv2
│   └── yolov3_training_last.weights # Bobot hasil training YOLOv3
└── dataset/
    └── test/                        # Folder berisi kumpulan gambar lift yang diuji
        ├── manusia.jpg              # Citra untuk uji coba awal
        ├── test_gambar.jpg          # Citra hasil salinan dog.jpg untuk kalibrasi
        └── [Gambar Kepadatan Lift Lainnya] (.jpg, .jpeg, .png)
```

## Skenario Pengujian & Alur Kode Praktikum

### 1. Penyiapan Lingkungan Awal & Perbaikan Eror (Langkah 1 - 4)

Pertama, Google Drive disambungkan ke mesin Colab. Selanjutnya, repositori Darknet dikloning. Agar proses deteksi berjalan cepat menggunakan kartu grafis (GPU Tesla T4), setelan awal Makefile diubah dari 0 menjadi 1 menggunakan perintah `sed`.

**Catatan Penanganan Eror:** Setelah verifikasi pustaka Python dilakukan, sempat terjadi kendala kegagalan build/error compile. Solusi yang diterapkan adalah menjalankan perintah pembersihan memori sisa kompilasi terlebih dahulu baru kemudian memicu kompilasi ulang secara bersih:

```bash
%cd /content/darknet
!make clean
!make
```

### 2. Kalibrasi Jalur Data (Langkah 5)

Folder tujuan di Drive dibuat secara otomatis jika belum ada. Gambar `dog.jpg` disalin sebagai tes awal, lalu dilakukan pengujian satu citra (`manusia.jpg`) untuk memastikan biner `./darknet` bisa mengenali konfigurasi model YOLOv3 dengan ambang batas (threshold) 0.30:

```bash
!./darknet detector test \
  cfg/coco.data \
  /content/drive/MyDrive/RTI/config/yolov3_training.cfg \
  /content/drive/MyDrive/RTI/weights/yolov3_training_last.weights \
  /content/drive/MyDrive/RTI/dataset/test/manusia.jpg \
  -thresh 0.30 \
  -dont_show
```

### 3. Eksekusi Otomatisasi Masal (YOLOv3 vs YOLOv2)

Bukan memproses satu per satu gambar secara manual, praktikum menggunakan skrip perulangan Python (`for nama_file in daftar_gambar`) yang otomatis memindai seluruh file berekstensi gambar di folder Drive.

Pada **Skenario YOLOv3:** Gambar disuapkan ke arsitektur backbone Darknet-53. Setelah teks perhitungan layer keluar di terminal, hasil gambar visual diambil dari berkas sementara `predictions.jpg` lalu ditampilkan langsung ke layar menggunakan fungsi `cv2_imshow()`.

Pada **Skenario YOLOv2:** Dengan logika perulangan yang sama, gambar dialihkan ke berkas konfigurasi `YOLOv2.cfg` dan bobot `YOLOv2.weights` (Darknet-19) untuk melihat perbandingan hasil deteksi objek manusianya.

## Karakteristik Hasil Output Pengujian

Hasil dari pengujian praktikum ini bukan berupa berkas file baru (seperti `.json`/`.csv`) yang tersimpan di dalam folder, melainkan berupa Live Terminal Stdout Log yang langsung tercetak pada output cell Google Colab dengan rincian:

- **Informasi Perangkat Keras:** Menampilkan status CUDA, cuDNN, dan tipe GPU aktif (`GPU: Tesla T4`).
- **Detail Lapisan Jaringan:** Menampilkan daftar layer konvolusi (`conv`), ukuran filter, perubahan dimensi resolusi gambar input ke output (misalnya `416 × 416 × 3 → 416 × 416 × 32`), serta nilai beban komputasi miliaran operasi (BFLOPS).
- **Metrik Utama & Visual Gambar:** Di baris paling bawah setiap iterasi gambar, terminal mencetak durasi pemrosesan kecepatan inferensi dalam hitungan detik (contoh: `Predicted in 0.0XXXXX seconds`), daftar objek manusia beserta akurasinya (`person: XX%`), dan langsung menampilkan gambar hasil deteksi yang sudah dilengkapi kotak pembatas (*bounding box*).

Output YOLOv3 :
https://colab.research.google.com/drive/1BFBBx0qb5tVRJhlo_bJqjW_djQaALQGG#scrollTo=v43GfoTzhDlC&fullscreenOutput=true

Output YOLOv2 :
https://colab.research.google.com/drive/1BFBBx0qb5tVRJhlo_bJqjW_djQaALQGG#scrollTo=Hw38H8RUigQS&fullscreenOutput=true