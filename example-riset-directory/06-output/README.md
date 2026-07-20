# 06-output

Hasil olahan data & visualisasi — **Tahap 4 (Analisis & Evaluasi)**.

Dihasilkan dari ekstraksi log mentah `04-data/` untuk membandingkan hasil visualisasi citra serta metrik performa antara Kondisi A (YOLOv2) dan Kondisi B (YOLOv3).

---

## tables/

| File | Isi |
|---|---|
| `tabel_komparasi_analisis.csv` | Tabel utama yang merangkum perbandingan *Inference Time* (ms), jumlah manusia terdeteksi, dan rata-rata *confidence score* antara YOLOv2 dan YOLOv3 untuk seluruh citra uji. |
| `akurasi_ground_truth.csv` | Tabel evaluasi selisih hitung objek murni kelas `person` dibandingkan dengan data asli di lapangan (*ground truth*). |

---

## figures/

Berikut adalah berkas citra hasil plot *bounding box* target kelas `person` yang diekspor dari berkas temp `predictions.jpg` setelah dieksekusi oleh masing-masing model:

### 1. Hasil Visualisasi YOLOv2
| File | Isi |
|---|---|
| `amigos_yolov2.png` | Hasil deteksi visual objek manusia menggunakan model YOLOv2 pada citra `amigos.jpg` (Terdeteksi 3 manusia beserta deteksi *false positive* objek tas). |
| `download_yolov2.png` | Hasil deteksi visual objek manusia menggunakan model YOLOv2 pada citra `download.jpg` (Terdeteksi 4 manusia). |
| `leonel lara_yolov2.png` | Hasil deteksi visual objek manusia menggunakan model YOLOv2 pada citra `leonel lara.jpg` (Terdeteksi 4 manusia beserta objek *cell phone* & *bottle*). |
| `@jaoyng on instagram_yolov2.png` | Hasil deteksi visual objek manusia menggunakan model YOLOv2 pada citra `@jaoyng on instagram.jpg` dengan kepadatan tinggi (Terdeteksi 13 manusia). |

### 2. Hasil Visualisasi YOLOv3
| File | Isi |
|---|---|
| `amigos_yolov3.png` | Hasil deteksi visual objek manusia menggunakan model YOLOv3 pada citra `amigos.jpg` (Terdeteksi 3 manusia dengan akurasi *confidence score* mencapai 100%). |
| `download_yolov3.png` | Hasil deteksi visual objek manusia menggunakan model YOLOv3 pada citra `download.jpg` (Terdeteksi 4 manusia dengan akurasi stabil). |
| `leonel lara_yolov3.png` | Hasil deteksi visual objek manusia menggunakan model YOLOv3 pada citra `leonel lara.jpg` (Terdeteksi 4 manusia dengan *confidence score* 100%). |
| `@jaoyng on instagram_yolov3.png` | Hasil deteksi visual objek manusia menggunakan model YOLOv3 pada citra `@jaoyng on instagram.jpg` dalam kondisi lift sangat padat (Terdeteksi 11 manusia). |

---

## Acuan

- Target Evaluasi: Akurasi penghitungan jumlah manusia dan efisiensi waktu deteksi pada ruang CCTV Lift.
- Sumber Data: Ekstraksi *log console* pengujian dari folder `04-data/`.

[../09-docs/tahap-4-analisis-data.md](../09-docs/tahap-4-analisis-data.md)