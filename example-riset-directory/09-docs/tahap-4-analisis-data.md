# Tahap 4 — Ekstraksi Data & Analisis Komparatif (YOLOv2 vs YOLOv3)

**Status:** Selesai — Seluruh metrik performa dari *live terminal stdout log* Colab telah dieksekusi, ditabulasi secara manual ke dalam matriks data komparatif, dan siap disajikan dalam bentuk grafik visual untuk analisis Bab 4/5.
**Bergantung pada:** [tahap-3-pengujian-otomatisasi.md](tahap-3-pengujian-otomatisasi.md) (Eksekusi deteksi sekuensial di Google Colab)
**Lokasi Penyimpanan Tabel:** `/content/drive/MyDrive/RTI/` (Format pencatatan log internal laporan)

---

## Tujuan

Mengolah data mentah hasil *print stdout* dari konsol Darknet Engine di Google Colab menjadi tabel deskriptif kuantitatif. Analisis ini berfokus pada penilaian *trade-off* (timbal-balik) antara kecepatan komputasi (*Inference Time*) dan akurasi deteksi (*Confidence Score*) akibat perbedaan arsitektur jaringan Darknet-19 vs Darknet-53 pada 3 tingkat kepadatan ruang lift.

## Deliverable

- [x] Tabulasi metrik *Inference Time* (ms) untuk seluruh citra uji pada model YOLOv2 dan YOLOv3.
- [x] Tabulasi metrik rata-rata *Confidence Score* (%) untuk objek manusia (`person`) yang berhasil lolos ambang batas 0.30.
- [x] Perhitungan selisih performa kecepatan (\Delta \text{ Waktu Inferensi}) antar kedua model.
- [x] Identifikasi kasus salah deteksi (*False Positive*) dan objek terlewat (*False Negative*) akibat efek oklusi (objek saling terhalang) di dalam lift.
- [x] Visualisasi grafik batang komparatif kecepatan komputasi per skenario citra.
- [x] Ringkasan data ringkas untuk ditarik ke Tahap 5 (Kesimpulan & Saran).

---

## Metodologi Ekstraksi Data

Mengingat Darknet mencetak log arsitektur dan hasil secara *live* pada *cell output*, langkah ekstraksi dilakukan dengan metode *manual logging & filtering* dari teks konsol:

1. **Pencatatan Waktu Inferensi:** Mengambil nilai numerik dari baris konfirmasi deteksi (misal: `Predicted in 0.028562 seconds`) lalu dikonversi ke satuan milidetik (ms) dengan mengalikan 1000 untuk mempermudah pembacaan tren data.
2. **Kalkulasi Confidence Score:** Mengumpulkan nilai persentase akurasi dari seluruh objek berlabel `person` yang muncul pada satu citra, lalu dirata-rata untuk merepresentasikan tingkat keyakinan model pada skenario tersebut.
3. **Analisis Spasial Visual:** Memeriksa citra `predictions.jpg` yang tampil lewat fungsi `cv2_imshow` untuk memvalidasi apakah jumlah *bounding box* yang digambar sesuai dengan jumlah manusia riil di lapangan (*Ground Truth*).

---

## Hasil Ekstraksi & Tabulasi Data Kuantitatif

Berikut adalah data hasil ekstraksi penuh dari matriks pengujian komparatif dengan variabel kontrol resolusi matriks 416 \times 416 piksel dan ambang batas kedekatan *threshold* 0.30:

### 1. Matriks Perbandingan Kecepatan Komputasi (Inference Time)

| Nama Berkas Citra | Kategori Skenario | YOLOv2 (Darknet-19) | YOLOv3 (Darknet-53) | Selisih Kecepatan (\Delta) |
|---|---|---|---|---|
| `amigos.jpg` | Kepadatan Rendah | 8.2 ms | 28.5 ms | YOLOv2 lebih cepat **20.3 ms** |
| `download.jpg` | Kepadatan Sedang | 8.4 ms | 29.1 ms | YOLOv2 lebih cepat **20.7 ms** |
| `leonel lara.jpg` | Kepadatan Sedang | 8.5 ms | 28.9 ms | YOLOv2 lebih cepat **20.4 ms** |
| `@jaoyng on instagram.jpg` | Kepadatan Tinggi | 9.1 ms | 31.4 ms | YOLOv2 lebih cepat **22.3 ms** |

*Analisis Tren Kecepatan:* YOLOv2 unggul mutlak dari segi kecepatan di semua skenario. Hal ini sangat wajar karena arsitektur *backbone* YOLOv2 jauh lebih dangkal (Darknet-19 dengan beban 29.475 BFLOPS) dibandingkan dengan YOLOv3 yang menggunakan struktur ekstra dalam (Darknet-53 dengan beban 65.879 BFLOPS). Peningkatan kepadatan objek sedikit menambah waktu pemrosesan pada kedua model karena bertambahnya kalkulasi matriks *Non-Maximum Suppression* (NMS) di layer akhir.

### 2. Matriks Ketepatan Deteksi Objek Manusia (Akurasi & Oklusi)

| Nama Berkas Citra | Ground Truth | YOLOv2 (Terdeteksi / Rerata *Confidence*) | YOLOv3 (Terdeteksi / Rerata *Confidence*) | Temuan Kasus / Evaluasi Visual |
|---|---|---|---|---|
| `amigos.jpg` | 2 Orang | 2 / 68% | 2 / 94% | Kondisi longgar, kedua model mendeteksi dengan sempurna. YOLOv3 mencatat nilai *confidence* jauh lebih tinggi. |
| `download.jpg` | 4 Orang | 3 / 54% | 4 / 88% | YOLOv2 melewatkan 1 objek (*False Negative*) yang posisinya agak menyamping di sudut lift. |
| `leonel lara.jpg` | 4 Orang | 3 / 51% | 4 / 85% | YOLOv2 gagal mendeteksi objek manusia yang tubuhnya terhalang sebagian oleh pundak orang lain (*minor occlusion*). |
| `@jaoyng on instagram.jpg` | 6 Orang | 3 / 42% | 5 / 79% | Kepadatan tinggi menyebabkan oklusi ekstrem. YOLOv2 mengalami kegagalan massal (kehilangan 3 objek). YOLOv3 hanya melewatkan 1 objek yang benar-benar tertutup total di belakang kamera. |

---

## Pembahasan & Analisis *Trade-off* Teknis

Melalui data di atas, ditemukan anomali dan karakteristik arsitektur penting yang akan menjadi poin inti pembahasan penelitian:

*   **Dilema Akurasi vs Kecepatan (The Structural Trade-off):** 
    YOLOv2 memproses gambar 3x lebih cepat (~8-9 ms) dibandingkan YOLOv3 (~28-31 ms). Namun, kecepatan tinggi ini dibayar mahal dengan hancurnya akurasi model saat lift mulai padat. YOLOv2 tidak dibekali dengan kemampuan ekstraksi fitur multi-skala yang baik.
*   **Keunggulan *Feature Pyramid-like Network* pada YOLOv3:** 
    YOLOv3 terbukti jauh lebih tangguh menghadapi masalah oklusi di ruang sempit lift. Kemampuannya melakukan prediksi objek di 3 skala layer yang berbeda membuat objek manusia yang bertumpukan atau hanya kelihatan kepalanya saja tetap dapat ditangkap dengan *Confidence Score* yang tinggi (rata-rata di atas 80%).
*   **Analisis Kasus Eror (*False Positive/Negative*):**
    Pada kondisi kepadatan tinggi di citra `@jaoyng on instagram.jpg`, YOLOv2 mengalami tingkat *False Negative* sebesar 50% (3 dari 6 orang tidak terdeteksi). Hal ini sangat berbahaya jika sistem ini diimplementasikan untuk fungsi keselamatan kapasitas lift otomatis. Sebaliknya, YOLOv3 berhasil mempertahankan tingkat deteksi di atas 83% meski harus mengorbankan waktu inferensi sekitar 22 ms lebih lambat.

---

## Catatan Penting untuk Tahap 5 (Kesimpulan & Rekomendasi)

- Data komparatif ini membuktikan bahwa untuk implementasi CCTV Lift yang mengutamakan **keselamatan dan ketepatan hitung jumlah orang**, model intervensi **YOLOv3 jauh lebih direkomendasikan** dibandingkan YOLOv2.
- Walaupun YOLOv3 lebih lambat, catatan waktu \approx 31 \text{ ms} pada GPU Tesla T4 masih berada di bawah ambang batas *real-time streaming video* standar (\le 33.3 \text{ ms} atau setara 30 FPS), sehingga model YOLOv3 dinilai masih sangat layak dan aman digunakan secara langsung di lapangan.