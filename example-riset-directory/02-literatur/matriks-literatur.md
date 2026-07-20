# MATRIKS LITERATUR

---

## I. Matriks Literatur

| No | Topik Kajian Literatur | Kode Referensi Terverifikasi |
| :--- | :--- | :--- |
| **1** | Deteksi Manusia dan Pelacakan Objek Bergerak (*Human Tracking*) | R-01, R-03, R-05, R-06 |
| **2** | Optimasi Klasifikasi Spesies dan Segmentasi Instans (*Species Segmentation*) | R-02, R-14, R-15, R-16 |
| **3** | Aplikasi Visi Komputer untuk Protokol Kesehatan dan Manajemen Absensi | R-04, R-09, R-10, R-11 |
| **4** | Teknik Augmentasi Data dan Rekayasa Prapemrosesan Citra | R-02, R-04, R-08, R-14 |
| **5** | Evolusi Efisiensi Komputasi Detektor *One-Stage* (YOLOv4 & YOLOv5) | R-01, R-03, R-06, R-13 |
| **6** | Analisis Komparatif Arsitektur Tingkat Lanjut (YOLOv6, YOLOv7, & YOLOv8) | R-02, R-04, R-07, R-17, R-18 |
| **7** | Integrasi Jaringan Saraf Konvolusional pada Perangkat Keras Terapan | R-01, R-03, R-12, R-13 |

---

## II. Catatan Temuan Literatur

* **Koreksi Kode Validasi:** Validasi referensi (R-01 s d R-18) murni menggunakan kecocokan data sitasi internal jurnal. Kode *CVE-2026-48524* sengaja tidak dilibatkan karena CVE merupakan sistem pelacakan celah keamanan siber (kerentanan *software*), bukan standar validasi karya ilmiah akademis.
* **Metrik Akurasi Tertinggi:** Optimasi pada klasifikasi spesies (siput beracun) menghasilkan mAP@0.5 sangat tinggi yaitu 0.987 pada *bbox* dan 0.986 pada *mask* [R-02]. Sementara itu, akurasi deteksi pemakaian masker wajah yang tepat mencapai 97% [R-04].
* **Lompatan Arsitektur YOLO:** YOLOv8 membawa perubahan masif dengan mengganti modul *C3* menjadi *C2f* serta menerapkan sistem *Anchor-Free Detection* (tanpa jangkar) yang berhasil memangkas waktu proses hingga 17 ms per citra pada perangkat *edge* [R-04].
* **Rekayasa Citra & Input:** Proses pelatihan mewajibkan standarisasi dimensi gambar ke kelipatan 32 (misal 480 \times 480 atau 640 \times 640 piksel) disertai augmentasi visual (*flip*, *brightness*, *exposure*) untuk mencegah model mengalami *underfitting* [R-02, R-03, R-04].
* **Implementasi Hardware:** Output koordinat dari *bounding box* hasil deteksi dikonversikan menjadi nilai sudut (*angle*) menggunakan fungsi *arctangent* untuk langsung menggerakkan aktuator/roda robot secara *real-time* [R-01].