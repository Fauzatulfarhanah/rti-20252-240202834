# 04-data

Data mentah hasil pengujian — output dari **Tahap 3 (Inference/Testing)**, input untuk **Tahap 4 (Analisis & Evaluasi)**.

## Isi yang diharapkan

- Log output mentah (*raw terminal logs*) dari framework Darknet untuk tiap citra uji per model (YOLOv2 vs YOLOv3)
- Rekapitulasi tabel data mentah hasil komparasi (*Inference Time*, Jumlah Objek, *Confidence Score*)
- Metadata eksekusi *runtime* Google Colab (Spesifikasi GPU, parameter threshold)

---

## Metadata Eksekusi Pengujian

Seluruh pengujian dilakukan secara terotomatisasi menggunakan *script* Python pada *environment* Google Colab dengan parameter lingkungan sebagai berikut:

* **Platform Eksekusi:** Google Colaboratory (Koneksi arsitektur *Hosted Runtime*)
* **Perangkat Keras Akselerator:** GPU Nvidia Tesla T4 (16 GB VRAM)
* **Framework Utama:** Darknet (Kompilasi berbasis C/CUDA)
* **Parameter Batas Deteksi (*Confidence Threshold*):** `-thresh 0.30` (Hanya mendeteksi objek dengan kepastian \ge 30\%)
* **Parameter Tampilan:** `-dont_show` (Menonaktifkan GUI bawaan Darknet, visualisasi dialihkan ke `predictions.jpg`)
* **Lokasi Sumber Data:** `/content/drive/MyDrive/RTI/dataset/test/`
* **Total Sampel Citra Uji:** 4 Citra karakteristik utama (Kondisi kepadatan di dalam lift)

---

## Log Output Mentah Terminal (Raw Terminal Logs)

Berikut adalah potongan data log mentah asli yang ditangkap langsung dari *output stream* perintah `!./darknet detector test` saat memproses citra uji:

### 1. Contoh Log Mentah Eksperimen YOLOv2 (`@jaoyng on instagram.jpg`)
```text
/content/drive/MyDrive/RTI/dataset/test/@jaoyng on instagram.jpg: Predicted in 72.959000 milli-seconds.
person: 46%
person: 56%
person: 45%
person: 34%
person: 61%
person: 34%
person: 52%
person: 66%
person: 52%
person: 41%
person: 40%
person: 43%
person: 35%
```

### 2. Contoh YOLOv3 (`@jaoyng on instagram.jpg`)
```text
/content/drive/MyDrive/RTI/dataset/test/@jaoyng on instagram.jpg: Predicted in 86.086000 milli-seconds.
person: 76%
person: 46%
person: 97%
person: 84%
person: 99%
person: 55%
person: 40%
person: 99%
person: 61%
person: 80%
person: 34%