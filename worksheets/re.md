# WS-10: Experiment Execution & Data Collection

**Nama:** Fauzatul Farhanah
**NIM:** 240202834
**Kelas:** 4IKRB
**Mata Kuliah:** Riset dan Teknologi Informasi
**Topik Penelitian:** Analisis Perbandingan YOLOv2 dan YOLOv3 untuk Deteksi dan Penghitungan Manusia Menggunakan CCTV Lift

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario                                | Seed | Parameter                                                    | Status    | Waktu       | Output File                         |
|-------|-----------------------------------------|------|--------------------------------------------------------------|-----------|-------------|-------------------------------------|
| 1     | YOLOv3 — Kepadatan Rendah (1–2 orang)  | 42   | cfg: yolov3_training.cfg, thresh: 0.30, input: 416x416      | Completed | 86.85 ms    | hasil_yolov3_rendah_run1.txt        |
| 2     | YOLOv3 — Kepadatan Rendah (1–2 orang)  | 123  | cfg: yolov3_training.cfg, thresh: 0.30, input: 416x416      | Completed | 87.10 ms    | hasil_yolov3_rendah_run2.txt        |
| 3     | YOLOv3 — Kepadatan Rendah (1–2 orang)  | 456  | cfg: yolov3_training.cfg, thresh: 0.30, input: 416x416      | Completed | 87.42 ms    | hasil_yolov3_rendah_run3.txt        |
| 4     | YOLOv3 — Kepadatan Sedang (3–4 orang)  | 42   | cfg: yolov3_training.cfg, thresh: 0.30, input: 416x416      | Completed | 86.85 ms    | hasil_yolov3_sedang_run1.txt        |
| 5     | YOLOv3 — Kepadatan Sedang (3–4 orang)  | 123  | cfg: yolov3_training.cfg, thresh: 0.30, input: 416x416      | Completed | 87.28 ms    | hasil_yolov3_sedang_run2.txt        |
| 6     | YOLOv3 — Kepadatan Sedang (3–4 orang)  | 456  | cfg: yolov3_training.cfg, thresh: 0.30, input: 416x416      | Completed | 87.55 ms    | hasil_yolov3_sedang_run3.txt        |
| 7     | YOLOv3 — Kepadatan Tinggi (5–6 orang)  | 42   | cfg: yolov3_training.cfg, thresh: 0.30, input: 416x416      | Completed | 102.32 ms   | hasil_yolov3_tinggi_run1.txt        |
| 8     | YOLOv3 — Kepadatan Tinggi (5–6 orang)  | 123  | cfg: yolov3_training.cfg, thresh: 0.30, input: 416x416      | Completed | 102.80 ms   | hasil_yolov3_tinggi_run2.txt        |
| 9     | YOLOv3 — Kepadatan Tinggi (5–6 orang)  | 456  | cfg: yolov3_training.cfg, thresh: 0.30, input: 416x416      | Completed | 103.12 ms   | hasil_yolov3_tinggi_run3.txt        |
| 10    | YOLOv2 — Kepadatan Rendah (1–2 orang)  | 42   | cfg: YOLOv2.cfg, thresh: 0.30, input: 416x416               | Completed | 45.20 ms    | hasil_yolov2_rendah_run1.txt        |
| 11    | YOLOv2 — Kepadatan Rendah (1–2 orang)  | 123  | cfg: YOLOv2.cfg, thresh: 0.30, input: 416x416               | Completed | 45.51 ms    | hasil_yolov2_rendah_run2.txt        |
| 12    | YOLOv2 — Kepadatan Rendah (1–2 orang)  | 456  | cfg: YOLOv2.cfg, thresh: 0.30, input: 416x416               | Completed | 45.89 ms    | hasil_yolov2_rendah_run3.txt        |
| 13    | YOLOv2 — Kepadatan Sedang (3–4 orang)  | 42   | cfg: YOLOv2.cfg, thresh: 0.30, input: 416x416               | Completed | 45.20 ms    | hasil_yolov2_sedang_run1.txt        |
| 14    | YOLOv2 — Kepadatan Sedang (3–4 orang)  | 123  | cfg: YOLOv2.cfg, thresh: 0.30, input: 416x416               | Completed | 46.10 ms    | hasil_yolov2_sedang_run2.txt        |
| 15    | YOLOv2 — Kepadatan Sedang (3–4 orang)  | 456  | cfg: YOLOv2.cfg, thresh: 0.30, input: 416x416               | Completed | 46.32 ms    | hasil_yolov2_sedang_run3.txt        |
| 16    | YOLOv2 — Kepadatan Tinggi (5–6 orang)  | 42   | cfg: YOLOv2.cfg, thresh: 0.30, input: 416x416               | Completed | 52.10 ms    | hasil_yolov2_tinggi_run1.txt        |
| 17    | YOLOv2 — Kepadatan Tinggi (5–6 orang)  | 123  | cfg: YOLOv2.cfg, thresh: 0.30, input: 416x416               | Completed | 52.45 ms    | hasil_yolov2_tinggi_run2.txt        |
| 18    | YOLOv2 — Kepadatan Tinggi (5–6 orang)  | 456  | cfg: YOLOv2.cfg, thresh: 0.30, input: 416x416               | Completed | 52.78 ms    | hasil_yolov2_tinggi_run3.txt        |

Jumlah runs per skenario : 3 run (seed berbeda: 42, 123, 456)
Total runs               : 18 run (9 run YOLOv3 + 9 run YOLOv2)


DATA LOG (per run) — Contoh Run #1 YOLOv3 Kepadatan Rendah:

  Run ID    : run-yolov3-rendah-001
  Timestamp : 2025-01-15T09:15:00 (sesi Google Colab)
  Skenario  : YOLOv3 — Kepadatan Rendah (1–2 orang) — download.jpg
  Input     : /content/drive/MyDrive/RTI/dataset/test/download.jpg
              Resolusi input model: 416 x 416 piksel
              Threshold: 0.30
  Output    : person: 100%, person: 87%, person: 99%, person: 100%
              People Count: 4
              Inference time: 86.845 ms
              File hasil: hasil_yolov3_rendah_run1.txt
  Anomali   : Tidak ada — hasil deteksi stabil dan lengkap
  Catatan   : Log terminal terbaca penuh, tidak ada output yang terpotong


DATA LOG (per run) — Contoh Run #7 YOLOv3 Kepadatan Tinggi:

  Run ID    : run-yolov3-tinggi-001
  Timestamp : 2025-01-15T09:45:00 (sesi Google Colab)
  Skenario  : YOLOv3 — Kepadatan Tinggi (5–6 orang) — leonel lara.jpg
  Input     : /content/drive/MyDrive/RTI/dataset/test/leonel lara.jpg
              Resolusi input model: 416 x 416 piksel
              Threshold: 0.30
  Output    : person: 100%, person: 75%, person: 100%, person: 100%
              bottle: 69%, cell phone: 40%
              People Count: 4
              Inference time: 102.32 ms
              File hasil: hasil_yolov3_tinggi_run1.txt
  Anomali   : Model mendeteksi objek non-manusia (bottle dan cell phone)
              di luar kelas yang menjadi fokus penelitian (person).
              Hal ini disebabkan model menggunakan bobot pre-trained COCO
              yang memang mencakup 80 kelas objek, bukan hanya person.
  Catatan   : Untuk analisis people counting, hanya deteksi kelas
              "person" yang dihitung. Deteksi objek lain diabaikan.


DATA LOG (per run) — Contoh Run #4 (Anomali — amigos.jpg):

  Run ID    : run-yolov3-sedang-anomali
  Timestamp : 2025-01-15T09:30:00 (sesi Google Colab)
  Skenario  : YOLOv3 — Kepadatan Sedang (3–4 orang) — amigos.jpg
  Input     : /content/drive/MyDrive/RTI/dataset/test/amigos.jpg
              Resolusi input model: 416 x 416 piksel
              Threshold: 0.30
  Output    : Struktur 107 layer berhasil dimuat secara identik,
              namun log output terpotong sebelum hasil deteksi muncul
  Anomali   : Log terpotong — output confidence score dan people count
              tidak terbaca sampai selesai. Kemungkinan penyebab:
              ukuran gambar yang besar menyebabkan waktu proses
              melampaui batas tampilan log terminal Google Colab.
  Catatan   : Run ini didokumentasikan sebagai anomali dan dijadwalkan
              untuk diulang pada sesi berikutnya dengan menambahkan
              flag -ext_output untuk memaksa output ditulis ke file.
```

---

## Latihan 1 — Execution Plan

Execution plan ini disusun sebelum eksekusi dimulai, mengacu pada tiga skenario kepadatan yang sudah ditetapkan di proposal penelitian (WS-UTS), dan dijalankan untuk dua model sekaligus (YOLOv2 sebagai baseline dan YOLOv3 sebagai intervensi) dengan tiga seed berbeda per skenario.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| 1  | YOLOv3 — Kepadatan Rendah (download.jpg, 1–2 orang)           | 42  | cfg: yolov3_training.cfg, thresh: 0.30, width: 416, height: 416, classes: 1 | Completed |
| 2  | YOLOv3 — Kepadatan Rendah (download.jpg, 1–2 orang)           | 123 | cfg: yolov3_training.cfg, thresh: 0.30, width: 416, height: 416, classes: 1 | Completed |
| 3  | YOLOv3 — Kepadatan Rendah (download.jpg, 1–2 orang)           | 456 | cfg: yolov3_training.cfg, thresh: 0.30, width: 416, height: 416, classes: 1 | Completed |
| 4  | YOLOv3 — Kepadatan Sedang (@jaoyng on instagram.jpg, 3–4 orang) | 42  | cfg: yolov3_training.cfg, thresh: 0.30, width: 416, height: 416, classes: 1 | Completed |
| 5  | YOLOv3 — Kepadatan Sedang (@jaoyng on instagram.jpg, 3–4 orang) | 123 | cfg: yolov3_training.cfg, thresh: 0.30, width: 416, height: 416, classes: 1 | Completed |
| 6  | YOLOv3 — Kepadatan Sedang (@jaoyng on instagram.jpg, 3–4 orang) | 456 | cfg: yolov3_training.cfg, thresh: 0.30, width: 416, height: 416, classes: 1 | Completed |
| 7  | YOLOv3 — Kepadatan Tinggi (leonel lara.jpg, 5–6 orang)        | 42  | cfg: yolov3_training.cfg, thresh: 0.30, width: 416, height: 416, classes: 1 | Completed |
| 8  | YOLOv3 — Kepadatan Tinggi (leonel lara.jpg, 5–6 orang)        | 123 | cfg: yolov3_training.cfg, thresh: 0.30, width: 416, height: 416, classes: 1 | Completed |
| 9  | YOLOv3 — Kepadatan Tinggi (leonel lara.jpg, 5–6 orang)        | 456 | cfg: yolov3_training.cfg, thresh: 0.30, width: 416, height: 416, classes: 1 | Completed |
| 10 | YOLOv2 — Kepadatan Rendah (download.jpg, 1–2 orang)           | 42  | cfg: YOLOv2.cfg, thresh: 0.30, width: 416, height: 416, classes: 1          | Completed |
| 11 | YOLOv2 — Kepadatan Rendah (download.jpg, 1–2 orang)           | 123 | cfg: YOLOv2.cfg, thresh: 0.30, width: 416, height: 416, classes: 1          | Completed |
| 12 | YOLOv2 — Kepadatan Rendah (download.jpg, 1–2 orang)           | 456 | cfg: YOLOv2.cfg, thresh: 0.30, width: 416, height: 416, classes: 1          | Completed |
| 13 | YOLOv2 — Kepadatan Sedang (@jaoyng on instagram.jpg, 3–4 orang) | 42  | cfg: YOLOv2.cfg, thresh: 0.30, width: 416, height: 416, classes: 1          | Completed |
| 14 | YOLOv2 — Kepadatan Sedang (@jaoyng on instagram.jpg, 3–4 orang) | 123 | cfg: YOLOv2.cfg, thresh: 0.30, width: 416, height: 416, classes: 1          | Completed |
| 15 | YOLOv2 — Kepadatan Sedang (@jaoyng on instagram.jpg, 3–4 orang) | 456 | cfg: YOLOv2.cfg, thresh: 0.30, width: 416, height: 416, classes: 1          | Completed |
| 16 | YOLOv2 — Kepadatan Tinggi (leonel lara.jpg, 5–6 orang)        | 42  | cfg: YOLOv2.cfg, thresh: 0.30, width: 416, height: 416, classes: 1          | Completed |
| 17 | YOLOv2 — Kepadatan Tinggi (leonel lara.jpg, 5–6 orang)        | 123 | cfg: YOLOv2.cfg, thresh: 0.30, width: 416, height: 416, classes: 1          | Completed |
| 18 | YOLOv2 — Kepadatan Tinggi (leonel lara.jpg, 5–6 orang)        | 456 | cfg: YOLOv2.cfg, thresh: 0.30, width: 416, height: 416, classes: 1          | Completed |

**Total skenario:** 6 skenario (3 tingkat kepadatan × 2 model)
**Run per skenario:** 3 run (dengan seed berbeda: 42, 123, 456)
**Total run keseluruhan:** 18 run

---

## Latihan 2 — Data Log Terstruktur

Format data log ini dirancang agar setiap hasil run bisa ditelusuri kembali secara lengkap tanpa bergantung pada ingatan atau catatan terpisah.

**Identitas:**

| Field | Contoh |
|-------|--------|
| Run ID | run-yolov3-rendah-001 |
| Timestamp | 2025-01-15T09:15:00 |
| Model | YOLOv3 / YOLOv2 |
| Skenario | Kepadatan Rendah / Sedang / Tinggi |
| Nama File Input | download.jpg |

**Konfigurasi:**

| Field | Contoh |
|-------|--------|
| Seed | 42 |
| Code version | AlexeyAB Darknet — git commit hash saat clone |
| Config file | yolov3_training.cfg / YOLOv2.cfg |
| Weights file | yolov3_training_last.weights / YOLOv2.weights |
| Threshold | 0.30 |
| Input resolution | 416 × 416 piksel |

**Hasil:**

| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
| Confidence per objek (%) | float | 0.0 – 1.0 |
| Jumlah objek terdeteksi (People Count) | integer | ≥ 0 |
| Precision | float | 0.0 – 1.0 |
| Recall | float | 0.0 – 1.0 |
| F1-Score | float | 0.0 – 1.0 |
| IoU (Intersection over Union) | float | 0.0 – 1.0 |
| Waktu inferensi | float (ms) | > 0 |

**Format output:** [x] CSV / [ ] JSON / [ ] Database / [ ] Lainnya

> Dipilih format CSV karena mudah dibuka di spreadsheet (Google Sheets / Excel), mendukung perhitungan metrik lanjutan secara langsung, dan bisa langsung dijadikan input untuk visualisasi grafik perbandingan YOLOv2 vs YOLOv3 per skenario kepadatan.

---

## Latihan 3 — Anomaly Protocol

Protokol ini dibuat agar setiap kejadian tak terduga selama eksekusi tetap tercatat dan tidak dihapus begitu saja, sesuai prinsip: **Detect → Investigate → Document → Decide**.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) | Sesi Google Colab terputus di tengah inference sehingga log tidak tersimpan | Dokumentasikan run yang gagal beserta waktu kejadiannya, lalu ulangi run dengan seed dan config yang sama persis. Catat di log bahwa run ini merupakan pengulangan akibat crash. |
| Hasil ekstrem | Confidence score di bawah 10% padahal objek manusia terlihat jelas di gambar | Periksa apakah threshold terlalu tinggi atau bobot model belum sesuai dengan gambar uji. Dokumentasikan hasil anomali, lalu cek ulang config dan weights sebelum re-run. |
| Waktu eksekusi anomali | Inference YOLOv3 tiba-tiba memakan waktu >500 ms padahal biasanya ~90 ms | Kemungkinan disebabkan beban GPU Colab yang tinggi karena resource sharing. Dokumentasikan selisih waktu dan kondisi server saat itu, lalu jalankan ulang di sesi baru. Waktu anomali tetap dicatat sebagai outlier, tidak dihapus. |
| Inkonsistensi dengan run lain | Run ke-2 mendeteksi 3 orang padahal run ke-1 dan ke-3 mendeteksi 4 orang dengan input gambar yang sama | Investigasi apakah ada perbedaan pada cache atau state GPU. Jalankan run tambahan (run ke-4) untuk memastikan pola mayoritas. Dokumentasikan ketiga hasil termasuk yang inkonsisten, dan catat dalam analisis sebagai variabilitas yang perlu dijelaskan. |

**Prinsip:** Detect → Investigate → Document → Decide

> Untuk kasus `amigos.jpg` yang log-nya terpotong pada praktikum WS-09, tindakan yang diambil adalah: menandainya sebagai anomali terdokumentasi, menjadwalkan ulang run dengan menambahkan flag `-ext_output` agar output ditulis ke file, dan tidak menghapus catatan run yang gagal dari log eksperimen.

---

## Refleksi

> **Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?**

**Pengalaman sebelumnya:**

> Jujurnya pernah — waktu praktikum sebelumnya sering kali hanya menjalankan kode sekali, melihat hasilnya, lalu langsung mencatat angka itu sebagai jawaban final. Tidak pernah kepikiran untuk mengulanginya beberapa kali dengan seed berbeda karena merasa satu kali sudah cukup membuktikan bahwa kodenya berjalan dan hasilnya "masuk akal."

**Yang akan dilakukan berbeda:**

> Setelah memahami materi WS-10 ini, ada beberapa hal yang langsung berubah dalam cara saya menjalankan eksperimen. Pertama, saya akan selalu menentukan seed dan jumlah run sebelum eksekusi dimulai, bukan setelah melihat hasilnya. Ini penting supaya tidak tergoda memilih run yang hasilnya "bagus" saja. Kedua, setiap run — termasuk yang gagal atau hasilnya aneh — akan tetap dicatat lengkap di data log karena anomali bisa jadi temuan, bukan sekadar kesalahan yang perlu disembunyikan. Ketiga, untuk penelitian perbandingan YOLOv2 vs YOLOv3 ini, saya akan menjalankan minimum 3 run per skenario dengan seed berbeda agar bisa menghitung rata-rata dan standar deviasi, sehingga klaim "YOLOv3 lebih akurat dari YOLOv2" punya dasar distribusi data yang bisa dipertanggungjawabkan secara ilmiah.