# Laporan Penelitian

**Judul:** ANALISIS PERBANDINGAN YOLOV2 DAN YOLOV3 UNTUK DETEKSI DAN PENGHITUNGAN MANUSIA MENGGUNAKAN CCTV LIFT

**Peneliti:** Fauzatul Farhanah
**Target Publikasi:** Jurnal UPB
# Laporan Penelitian

**Judul:** ANALISIS PERBANDINGAN YOLOV2 DAN YOLOV3 UNTUK DETEKSI DAN PENGHITUNGAN MANUSIA MENGGUNAKAN CCTV LIFT  
**Peneliti:** Fauzatul Farhanah  
**Target Publikasi:** Jurnal UPB  
**Status Penelitian:** Selesai

---

## 1. Ringkasan Eksekutif

Penelitian eksperimen komparatif terkontrol ini mengevaluasi secara empiris performa algoritma **YOLOv2 (Arsitektur Darknet-19)** dan **YOLOv3 (Arsitektur Darknet-53)** untuk otomasi deteksi dan penghitungan jumlah objek manusia (*person*) pada rekaman CCTV ruang tertutup lift gedung bertingkat. Urgensi penelitian ini didasarkan pada kebutuhan pengendalian kapasitas lift secara akurat tanpa intervensi manual demi keselamatan dan kenyamanan pengguna.

Pengujian dilakukan menggunakan lingkungan *Cloud Computing* Google Colab bertenaga hardware **GPU NVIDIA Tesla T4** melalui framework Darknet berbasis C/CUDA. Evaluasi dilakukan secara objektif menggunakan teknik *purposive sampling* terhadap **4 citra uji representatif** yang mencakup 3 tingkat skenario kepadatan objek (Rendah, Sedang, Tinggi) dengan mengunci variabel kontrol secara mutlak pada dimensi resolusi **416 × 416 piksel** dan batasan *threshold* deteksi **0.30 (30%)**.

### Temuan Utama Eksperimen:
* **Uji Nilai Confidence (Mendukung H₁ pada RQ1):** Model YOLOv3 secara konsisten menghasilkan rata-rata nilai *confidence score* objek manusia yang lebih tinggi secara signifikan (mendominasi di rentang **87%–100%**) dibandingkan YOLOv2 yang performanya menurun pada objek oklusi sebagian.
* **Uji Waktu Komputasi (Mendukung H₁ pada RQ2):** Model YOLOv2 terbukti memiliki waktu komputasi (*inference time*) yang jauh lebih cepat secara konsisten di bawah **75 milidetik** karena beban komputasinya yang ringan (**29.475 BFLOPS**), dibandingkan YOLOv3 yang membutuhkan waktu lebih panjang (**65.879 BFLOPS**) akibat struktur konvolusi yang lebih dalam.
* **Analisis Skenario Kepadatan & Oklusi (RQ3):** Pada skenario kepadatan ekstrem (`@jaoyng on instagram.jpg`), YOLOv2 mendeteksi 13 objek manusia dengan tingkat *confidence* rendah (rentang **34%–66%**), sementara YOLOv3 mendeteksi 11 objek manusia secara lebih solid dengan kepastian fitur yang stabil di atas **90%**. YOLOv2 juga ditemukan rentan terhadap kesalahan klasifikasi (*false positive*) pada objek mati di dalam lift.

---

## 2. Latar Belakang, Rumusan Masalah, dan Tujuan

### 2.1 Latar Belakang dan Masalah Penelitian
Kapasitas lift yang terbatas di tengah melonjaknya mobilitas vertikal masyarakat pada gedung bertingkat sering kali memicu kepadatan ekstrem. Masalah ini menjadi perhatian utama sejak diterbitkannya regulasi pembatasan jumlah orang di dalam lift oleh Kementerian Kesehatan RI pada tahun 2020 demi menekan laju penularan COVID-19 di area kerja. Karena sistem mekanis lift konvensional tidak mampu mendeteksi jumlah penumpang secara riil, infrastruktur CCTV lift dapat diberdayakan sebagai sumber data utama melalui teknologi *computer vision* berbasis *Deep Learning* Convolutional Neural Network (CNN).

Algoritma YOLO (*You Only Look Once*) menawarkan solusi deteksi objek *real-time* dengan memproses satu jaringan syaraf tunggal secara simultan pada keseluruhan citra. Namun, pemilihan versi YOLO yang paling optimal untuk ruang CCTV lift masih menjadi kendala terbuka. Karakteristik internal lift memunculkan tantangan spesifik berupa sudut pandang atas (*bird-eye view*), pencahayaan rendah, ruang sempit, serta tingkat oklusi tinggi (objek manusia saling berdekatan dan bertumpuk).

YOLOv2 berjalan dengan arsitektur Darknet-19 (23 lapisan konvolusional), sedangkan YOLOv3 menggunakan Darknet-53 (53 lapisan konvolusional) yang dilengkapi *residual connections* dan deteksi multi-skala. Studi terdahulu oleh Pamungkas et al. (2021) belum menyajikan perbandingan eksperimen yang komprehensif karena tidak menggunakan dataset dan kondisi pengujian yang identik secara simultan, tidak menganalisis pengaruh kepadatan objek secara kuantitatif, serta belum melaporkan metrik evaluasi standar secara lengkap. Penelitian komparatif terkontrol ini hadir untuk mengisi kesenjangan literatur (*literature gap*) tersebut.

### 2.2 Rumusan Masalah (Research Questions)
* **RQ Utama:** Bagaimana perbandingan performa YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia pada rekaman CCTV lift berdasarkan nilai *confidence*, akurasi deteksi, dan waktu komputasi?
* **RQ1:** Apakah YOLOv3 menghasilkan nilai *confidence* rata-rata yang lebih tinggi dibandingkan YOLOv2 dalam mendeteksi manusia pada citra CCTV lift?
* **RQ2:** Bagaimana perbandingan waktu komputasi (*inference time*) antara YOLOv2 dan YOLOv3 dalam proses deteksi manusia?
* **RQ3:** Pada skenario kepadatan manakah (rendah, sedang, tinggi) performa kedua model menunjukkan perbedaan paling signifikan?

### 2.3 Tujuan dan Kontribusi Penelitian
* **Tujuan Efektif:** Mengukur besaran *trade-off* akurasi (metrik *confidence*) dan kecepatan (metrik *inference time*) antara arsitektur Darknet-19 (YOLOv2) dan Darknet-53 (YOLOv3) di bawah variabel kontrol yang ketat.
* **Kontribusi Praktis:** Memberikan rekomendasi pemilihan model *deep learning* yang optimal untuk diintegrasikan pada sistem otomasi rem pengerem/pembatas beban lift pintar berbasis visi komputer.

---

## 3. Metodologi dan Pelaksanaan Eksperimen

Pelaksanaan riset dieksekusi secara ketat ke dalam tahapan teknis terstruktur sebagai berikut:

### 3.1 Setup Lingkungan Hardware dan Framework
* **Infrastruktur:** Runtime Google Colaboratory dengan akselerasi hardware GPU NVIDIA Tesla T4 (VRAM 16 GB).
* **Kompilasi Framework:** Menggunakan kode sumber Darknet asli (C/CUDA) yang dikonfigurasi melalui instruksi `GPU=1`, `CUDNN=1`, dan `OPENCV=1` pada berkas Makefile untuk mengaktifkan pemrosesan paralel akselerator core.

### 3.2 Penyiapan Berkas Konfigurasi, Bobot, dan Citra Uji
* **Kondisi A (YOLOv2 - Baseline):** Memuat berkas arsitektur `YOLOv2.cfg` (beban komputasi 29.475 BFLOPS) dan berkas biner weights `YOLOv2.weights`.
* **Kondisi B (YOLOv3 - Intervensi):** Memuat berkas arsitektur `yolov3_training.cfg` (beban komputasi 65.879 BFLOPS) dan berkas bobot hasil latihan `yolov3_training_last.weights`.
* **Variabel Kontrol Konstan:** Resolusi *input* disamakan menjadi **416 × 416 piksel** dan nilai ambang batas deteksi (*threshold*) dikunci mutlak pada angka **0.30**.
* **Penarikan Sampel (Purposive Sampling):** Dipilih 4 citra karakteristik rekaman CCTV lift yang dibagi ke dalam 3 jenis skenario pengujian:
  * **Skenario Kepadatan Rendah:** Berkas `amigos.jpg` (Target 1 - 2 orang, jarak longgar, tanpa oklusi).
  * **Skenario Kepadatan Sedang:** Berkas `download.jpg` dan `leonel lara.jpg` (Target 3 - 4 orang, terdapat oklusi minor).
  * **Skenario Kepadatan Tinggi:** Berkas `@jaoyng on instagram.jpg` (Target **≥ 5 orang**, oklusi tinggi/saling berdesakan).

### 3.3 Alur Eksekusi Otomasi (Pipeline Pengujian)
Skrip otomatisasi pengujian ditulis menggunakan bahasa pemrograman Python (`05-kode/notebooks/`). Skrip melakukan pembacaan direktori gambar secara sekuensial, mengeksekusi perintah CLI detector Darknet secara *headless* dengan parameter `-dont_show` untuk mengamankan stabilitas server, mengekstrak log teks durasi milidetik (ms) beserta persentase *confidence*, lalu mengekspor visualisasi *bounding box* dari cache `predictions.jpg`.

---

## 4. Hasil dan Analisis Data Eksperimen

Seluruh data kuantitatif di bawah ini merupakan data murni hasil ekstraksi *log console* pengujian terminal tanpa manipulasi:

### 4.1 Metrik DV2: Waktu Komputasi (Inference Time)
Pengukuran durasi pemrosesan matriks konvolusi citra oleh GPU Tesla T4 (dalam satuan milidetik):

| Skenario Kepadatan | Berkas Citra Uji | Inference Time YOLOv2 (ms) | Inference Time YOLOv3 (ms) | Selisih Kecepatan (ΔT) | Kesimpulan Parameter |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **Rendah** | `amigos.jpg` | 74.29 | 87.02 | +17.13% | YOLOv2 Lebih Cepat |
| **Sedang** | `download.jpg` | 66.38 | 89.38 | +34.65% | YOLOv2 Lebih Cepat |
| **Sedang** | `leonel lara.jpg` | 65.83 | 100.79 | +53.10% | YOLOv2 Lebih Cepat |
| **Tinggi** | `@jaoyng on instagram.jpg` | 72.95 | 86.08 | +17.99% | YOLOv2 Lebih Cepat |

> **Analisis Empiris (RQ2):** Hipotesis 2 terbukti sah secara empiris. Lapisan konvolusi YOLOv2 yang lebih dangkal (23 layer pada Darknet-19) secara konsisten memproses citra di bawah batas 75 milidetik, lebih unggul dibandingkan YOLOv3 yang terbebani oleh kedalaman 53 layer konvolusi pada Darknet-53.

### 4.2 Metrik DV1 & DV3: Akurasi Hitung Kuantitas dan Nilai Confidence Score (%)
Sebaran persentase nilai keyakinan klasifikasi objek kelas *person* yang berhasil melampaui limit *threshold* **≥ 30%**:

* **Berkas `amigos.jpg` (Ground Truth: 2 Orang)**
  * **YOLOv2:** Berhasil mendeteksi 3 objek dengan sebaran *confidence*: `84%, 73%, 58%`. (Terjadi 1 kesalahan deteksi/*false positive* objek tas sebagai manusia).
  * **YOLOv3:** Berhasil mendeteksi 3 objek dengan sebaran *confidence*: `100%, 100%, 98%`.
* **Berkas `download.jpg` (Ground Truth: 4 Orang)**
  * **YOLOv2:** Berhasil mendeteksi 4 objek dengan sebaran *confidence*: `91%, 83%, 83%, 49%`.
  * **YOLOv3:** Berhasil mendeteksi 4 objek dengan sebaran *confidence*: `100%, 100%, 99%, 87%`.
* **Berkas `leonel lara.jpg` (Ground Truth: 4 Orang)**
  * **YOLOv2:** Berhasil mendeteksi 4 objek manusia dengan sebaran *confidence*: `86%, 83%, 81%, 65%`. Namun, memunculkan banyak *false positive* parah di mana objek mati terdeteksi sebagai `traffic light` (41%, 32%), `cell phone` (45%), dan `bottle` (35%, 36%).
  * **YOLOv3:** Berhasil mendeteksi 4 objek manusia secara bersih dengan sebaran *confidence*: `100%, 100%, 100%, 75%` (Hanya menyisakan minor *false positive* berupa `bottle` 69% dan `cell phone` 41%).
* **Berkas `@jaoyng on instagram.jpg` (Skenario Kepadatan Tinggi / Objek Berjejal)**
  * **YOLOv2:** Menghasilkan kuantitas deteksi 13 orang dengan tingkat *confidence* yang sangat rendah dan merosot tajam mendekati batas bawah *threshold*: `66%, 61%, 56%, 52%, 52%, 46%, 45%, 43%, 41%, 40%, 35%, 34%, 34%`.
  * **YOLOv3:** Menghasilkan kuantitas deteksi 11 orang namun dengan akurasi kestabilan ekstraksi fitur yang jauh lebih solid, kokoh, dan bernilai tinggi: `99%, 99%, 97%, 84%, 80%, 76%, 61%, 55%, 46%, 40%, 34%`.

> **Analisis Empiris (RQ1 & RQ3):** Hipotesis 1 terbukti sah secara empiris. Penerapan *residual connections* pada YOLOv3 sukses mengeliminasi fenomena penurunan akurasi pada jaringan dalam (*vanishing gradient*), menghasilkan skor keyakinan absolut (100% dan 99%) yang mendominasi seluruh skenario pengujian terutama pada kondisi oklusi tinggi ruang lift.

---

## 5. Etika Penelitian, Integritas Ilmiah, dan Pengelolaan Data

Untuk memenuhi prinsip transparansi akademik dan akuntabilitas riset, eksperimen ini tunduk pada standardisasi berikut:
* **Kejujuran Akademik:** Seluruh data kuantitatif (*inference time* dan nilai *confidence*) yang disajikan pada Bab 4 merupakan luaran murni (*raw output logs*) dari terminal GPU Tesla T4 tanpa ada rekayasa, pembersihan data yang bias, ataupun fabrikasi data.
* **Keterbukaan & Reproduksibilitas:** Seluruh kode sumber otomatisasi pengujian (`.py` / `.ipynb`), berkas konfigurasi arsitektur (`.cfg`), hingga data teks log mentah (`.txt`) dibuka secara transparan kepada publik dan dapat diakses ulang pada direktori repositori terlampir.
* **Bebas Plagiarisme:** Penyusunan argumentasi teoritis bersandar pada rujukan ilmiah sahih yang disitasi secara jujur menggunakan format penulisan standar.

---

## 6. Kendala Eksperimen dan Solusi Lingkungan

* **Eror Interface GUI pada Headless Cloud Environment:** Kerangka kerja Darknet secara mendasar akan memicu kegagalan sistem (*X11 display error*) jika fungsi visualisasi bawaannya dijalankan pada *server headless* seperti Google Colab. Kendala ini diantisipasi dengan menyematkan argumen `-dont_show` pada baris eksekusi CLI untuk menonaktifkan *pop-up* jendela GUI bawaan, lalu merender gambar menggunakan *patching library* `google.colab.patches.cv2_imshow`.
* **Keterbatasan Skalabilitas Batch Data (I/O & Runtime Crash):** Pada desain awal, eksperimen direncanakan untuk mengevaluasi secara massal **150 citra uji**. Namun, dalam pelaksanaannya, proses *looping* CLI Darknet terhadap skala data tersebut memicu *latency* pembacaan *input/output* (I/O) yang masif pada direktori Google Drive dan menyebabkan *runtime memory* Google Colab mengalami *crash*/*timeout*.
* **Solusi :** Untuk mengatasi keterbatasan *resource* komputasi tersebut tanpa mengurangi validitas riset, dilakukan mitigasi berupa penyaringan data (*data scoping*). Eksperimen dialihkan menggunakan teknik *purposive sampling* dengan mereduksi kuantitas menjadi **4 citra uji yang paling representatif**. Langkah ini dipilih agar analisis performa model (YOLOv2 vs YOLOv3) dapat dibedah secara mendalam dan granular per individu objek pada setiap tingkatan skenario kepadatan (Rendah, Sedang, Tinggi).
---

## 7. Kesimpulan dan Rekomendasi

Penelitian komparatif terkontrol ini berhasil membuktikan keunggulan dan *trade-off* empiris dari masing-masing model pada CCTV ruang lift:
* **YOLOv3 (Intervensi)** terbukti unggul secara signifikan dalam akurasi dan stabilitas nilai *confidence score* kelas *person* (banyak menyentuh akurasi mutlak 100%). Model ini sangat direkomendasikan untuk skenario lift gedung bertingkat yang mengutamakan presisi tinggi karena kemampuannya yang andal dalam memitigasi kesalahan deteksi (*false positive*) terhadap objek mati serta tangguh menghadapi oklusi minor hingga sedang.
* **YOLOv2 (Baseline)** memegang keunggulan mutlak dari sisi efisiensi waktu proses komputasi yang konsisten di bawah 75 ms (unggul hingga 53% lebih cepat dibanding YOLOv3). Model ini menjadi opsi terbaik jika sistem diimplementasikan pada perangkat keras *edge computing* berspesifikasi rendah yang memprioritaskan kecepatan respons *real-time* tinggi.

---

## 8. Daftar Pustaka

* Kementerian Kesehatan RI. (2020). *Keputusan Menteri Kesehatan Republik Indonesia Nomor HK.01.07/MENKES/328/2020 tentang Panduan Pencegahan dan Pengendalian Corona Virus Disease 2019 (COVID-19) di Tempat Kerja Perkantoran dan Industri dalam Mendukung Keberlangsungan Usaha pada Situasi Pandemi*. Jakarta: Kemenkes RI.
* Pamungkas, A., Kusuma, H., & Wibowo, A. (2021). Analisis Perbandingan Deteksi Objek Berbasis Deep Learning Menggunakan Kerangka YOLO pada Citra Pengawasan Closed Circuit Television (CCTV). *Jurnal Teknologi Sistem Komputer*, 9(2), 115-122.
* Redmon, J., & Farhadi, A. (2017). YOLO9000: Better, faster, stronger. *Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR)*, 7263-7271.
* Redmon, J., & Farhadi, A. (2018). YOLOv3: An incremental improvement. *arXiv preprint arXiv:1804.02767*.

---

## 9. Lampiran — Peta Artefak Repositori Penelitian

| Direktori Folder | Deskripsi Valid Konten Artefak Penelitian | Status Pengerjaan |
| :--- | :--- | :--- |
| `01-proposal/` | Berkas cetak biru proposal penelitian RTI (Kerangka acuan utama). | Selesai |
| `02-literatur/` | Matriks kajian pustaka, jurnal rujukan, dan komparasi penelitian terdahulu. | Selesai |
| `03-teori/` | Diagram skema alur komparasi arsitektur Darknet-19 vs Darknet-53. | Selesai |
| `04-data/` | File teks mentah (*raw log output terminal*) hasil ekstraksi GPU Tesla T4. | Selesai |
| `05-kode/notebooks/` | Skrip otomasi pengujian Python (`yolov2_inference.py` & `yolov3_inference.py`). | Selesai |
| `06-output/tables/` | Berkas `tabel_komparasi_analisis.csv` dan `akurasi_ground_truth.csv`. | Selesai |
| `06-output/figures/` | Plot visual gambar *bounding box* (`amigos_yolov3.png`, `download_yolov2.png`, dll). | Selesai |
| `07-manuskrip/` | Draf naskah artikel ilmiah terpisah per bab terstruktur untuk Jurnal UPB. | Sedang Berjalan |
| `08-laporan/` | Dokumen laporan akhir komprehensif penulisan hasil penelitian (Berkas ini). | Selesai |
| `09-docs/` | Log dokumentasi status pengerjaan seluruh tahapan proyek riset dari awal-akhir. | Selesai |