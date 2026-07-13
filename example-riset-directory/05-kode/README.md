# 05-kode

Source code implementasi — Skrip Otomasi Pengujian Lingkungan Eksperimen Komparasi YOLOv2 dan YOLOv3 di Google Colab.

## Struktur yang direncanakan
05-kode/
└── notebooks/
├── yolov2_inference.py   # Skrip loop pengujian karakteristik objek model YOLOv2
└── yolov3_inference.py   # Skrip loop pengujian karakteristik objek model YOLOv3

## Acuan

- Jalur File Konfigurasi Model: `/content/drive/MyDrive/RTI/config/`
- Jalur File Bobot Kecerdasan Buatan: `/content/drive/MyDrive/RTI/weights/`
- Target Dataset Uji: `/content/drive/MyDrive/RTI/dataset/test/`

---

## Kode Implementasi Eksperimen

### 1. Skrip Pengujian YOLOv2 (`notebooks/yolov2_inference.py`)
Skrip ini digunakan untuk memuat arsitektur jala-surya `YOLOv2.cfg` dan berkas bobot `YOLOv2.weights` guna mendeteksi manusia secara sekuensial.

```python
import os
import cv2
from google.colab.patches import cv2_imshow

# 1. Masuk ke folder utama darknet
%cd /content/darknet

# 2. Tentukan folder lokasi gambar di Drive kamu
folder_test = "/content/drive/MyDrive/RTI/dataset/test/"

# 3. Ambil daftar semua file gambar
daftar_gambar = [f for f in os.listdir(folder_test) if f.endswith(('.jpg', '.jpeg', '.png'))]

print(f"Menemukan {len(daftar_gambar)} gambar untuk diuji dengan YOLOv2.\n")

# 4. Lakukan perulangan untuk menguji tiap gambar dengan YOLOv2
for nama_file in daftar_gambar:
    jalur_gambar = os.path.join(folder_test, nama_file)
    print(f"=== MENGUJI GAMBAR DENGAN YOLOv2: {nama_file} ===")

    # Jalankan perintah Darknet detector versi YOLOv2
    !./darknet detector test \
      cfg/coco.data \
      /content/drive/MyDrive/RTI/config/YOLOv2.cfg \
      /content/drive/MyDrive/RTI/weights/YOLOv2.weights \
      "{jalur_gambar}" \
      -thresh 0.30 \
      -dont_show

    # Tampilkan hasil deteksi visualnya
    hasil_prediksi = cv2.imread('predictions.jpg')
    print(f"Hasil Visual YOLOv2 untuk {nama_file}:")
    cv2_imshow(hasil_prediksi)
    print("\n" + "="*50 + "\n")
```

2. Skrip Pengujian YOLOv3 (notebooks/yolov3_inference.py)
Skrip ini digunakan untuk memuat arsitektur jala-surya yolov3_training.cfg dan berkas bobot hasil latihan terakhir yolov3_training_last.weights guna mendeteksi manusia pada tingkat oklusi berbeda.
```
Python
import os
import cv2
from google.colab.patches import cv2_imshow
```
# 1. Pastikan program berada di folder utama darknet
%cd /content/darknet

# 2. Tentukan folder lokasi 5 gambar kamu di Drive
folder_test = "/content/drive/MyDrive/RTI/dataset/test/"

# 3. Ambil daftar semua file gambar di folder tersebut
daftar_gambar = [f for f in os.listdir(folder_test) if f.endswith(('.jpg', '.jpeg', '.png'))]

print(f"Menemukan {len(daftar_gambar)} gambar untuk diuji.\n")

# 4. Lakukan perulangan untuk menguji tiap gambar dengan YOLOv3
for nama_file in daftar_gambar:
    jalur_gambar = os.path.join(folder_test, nama_file)
    print(f"=== MENGUJI GAMBAR: {nama_file} ===")

    # Jalankan perintah Darknet detector
    !./darknet detector test \
      cfg/coco.data \
      /content/drive/MyDrive/RTI/config/yolov3_training.cfg \
      /content/drive/MyDrive/RTI/weights/yolov3_training_last.weights \
      "{jalur_gambar}" \
      -thresh 0.30 \
      -dont_show

    # Tampilkan hasil deteksi visualnya langsung di layar Colab
    hasil_prediksi = cv2.imread('predictions.jpg')
    print(f"Hasil Visual untuk {nama_file}:")
    cv2_imshow(hasil_prediksi)
    print("\n" + "="*50 + "\n")

Logika Operasional Kode
Manajemen File I/O: Skrip memanfaatkan modul bawaan os.listdir() untuk membaca direktori Google Drive secara dinamis, sehingga peneliti cukup menambahkan atau mengurangi gambar di Google Drive tanpa perlu mengubah baris kode program.

Mekanisme Tampilan Rendah Beban (Low-Overhead Display): Parameter -dont_show disematkan langsung pada perintah CLI Darknet untuk mencegah sistem memanggil GUI X11 (yang akan menyebabkan eror fatal pada headless server Google Colab). Pemrosesan visual dialihkan ke fungsi patching cv2_imshow bawaan Colab dengan membaca berkas cache temporal predictions.jpg.




