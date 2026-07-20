# PROPOSAL PENELITIAN
**Mata Kuliah Riset dan Teknologi Informasi**

## A. Judul Penelitian
**ANALISIS PERBANDINGAN YOLOV2 DAN YOLOV3 UNTUK DETEKSI DAN PENGHITUNGAN MANUSIA MENGGUNAKAN CCTV LIFT**

---

## B. Ringkasan
Penelitian ini bertujuan membandingkan performa algoritma YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung jumlah manusia pada rekaman CCTV, khususnya dalam lingkungan tertutup seperti lift gedung bertingkat. Konteks penelitian ini berangkat dari kebutuhan nyata pengendalian kapasitas lift selama pandemi COVID-19, di mana diperlukan sistem otomatis yang mampu mendeteksi jumlah pengguna secara akurat tanpa intervensi manual. Penelitian bersifat komparatif-evaluatif dengan desain eksperimen terkontrol menggunakan dataset yang sama antara kedua model. 

Variabel independen dalam penelitian ini adalah jenis model YOLO (YOLOv2 vs YOLOv3), sedangkan variabel dependen meliputi nilai confidence, jumlah objek terdeteksi, dan waktu proses (inference time). Pengujian dilakukan terhadap 4 citra representatif yang mengekstraksi variasi kepadatan objek di dalam lift menggunakan teknik purposive sampling. Hipotesis yang diuji adalah model YOLOv3 mampu mengungguli YOLOv2 dalam nilai confidence dan akurasi deteksi karena memiliki arsitektur Darknet-53 dengan 53 lapisan konvolusional yang lebih dalam, meskipun dengan konsekuensi waktu komputasi yang lebih panjang. Luaran penelitian ini berupa laporan analisis komparatif terukur yang memuat tabel metrik lengkap untuk kedua model pada tiga skenario kepadatan, serta rekomendasi pemilihan model berbasis bukti untuk implementasi sistem deteksi manusia pada CCTV lift.

**Kata Kunci:** YOLOv2; YOLOv3; deteksi manusia; penghitungan objek; rekaman CCTV

---

## C. Pendahuluan

### C.1 Latar Belakang dan Rumusan Masalah
Penggunaan lift pada gedung-gedung bertingkat merupakan fasilitas kritis yang mendukung efisiensi mobilitas pengguna di pusat perbelanjaan, perkantoran, hotel, apartemen, dan instansi lainnya. Kapasitas lift yang terbatas bertolak belakang dengan jumlah pengguna yang terus meningkat, sehingga menimbulkan masalah kepadatan. Kondisi ini semakin kritis ketika pada tahun 2020 pemerintah Indonesia melalui Kementerian Kesehatan RI menetapkan peraturan pembatasan jumlah orang di dalam lift sebagai upaya pencegahan penularan COVID-19 di tempat kerja.

Sistem kerja lift konvensional tidak dilengkapi dengan kemampuan mendeteksi jumlah penumpang secara akurat. Oleh karena itu, diperlukan sistem pendukung berbasis teknologi yang mampu memanfaatkan infrastruktur CCTV yang sudah terpasang di dalam lift untuk mendeteksi dan menghitung jumlah manusia secara otomatis. Rekaman video CCTV di dalam lift dapat dijadikan sumber data untuk diproses menggunakan algoritma computer vision berbasis deep learning.

Dalam bidang computer vision dan object detection, metode Convolutional Neural Network (CNN) telah terbukti menjadi pendekatan paling efektif untuk pengenalan citra. CNN merupakan pengembangan dari Multi Layer Perceptron (MLP) yang berusaha meniru sistem pengenalan citra pada visual cortex manusia. YOLO (You Only Look Once) adalah salah satu algoritma deep learning berbasis CNN untuk deteksi objek yang menggunakan pendekatan berbeda: menerapkan jaringan syaraf tunggal secara sekaligus pada keseluruhan citra, sehingga jauh lebih cepat dibandingkan metode berbasis region proposal.

YOLOv2 merupakan generasi kedua algoritma YOLO yang menggunakan arsitektur Darknet-19 dengan 23 lapisan konvolusional. Sementara itu, YOLOv3 adalah generasi ketiga yang menggunakan arsitektur Darknet-53 dengan 53 lapisan konvolusional, dilengkapi residual connections (shortcut) dan kemampuan deteksi multi-skala. Kedua versi ini telah diaplikasikan secara luas dalam berbagai skenario deteksi objek, termasuk deteksi pejalan kaki (pedestrian detection) yang relevan dengan konteks penelitian ini.

Permasalahan utama yang dihadapi adalah bagaimana memilih algoritma deteksi objek yang paling tepat untuk skenario penghitungan manusia dalam lift berbasis rekaman CCTV. Kedua versi YOLO memiliki karakteristik yang berbeda: YOLOv3 memiliki jumlah layer lebih banyak sehingga diharapkan menghasilkan akurasi lebih tinggi, sementara YOLOv2 memiliki arsitektur lebih ringan sehingga lebih cepat. Namun, belum ada analisis komparatif yang sistematis antara YOLOv2 dan YOLOv3 pada dataset spesifik rekaman CCTV lift dengan kondisi pencahayaan rendah, sudut pandang terbatas (bird-eye view), dan objek yang saling berdekatan.

Studi yang dilakukan oleh Pamungkas et al. (2021) telah menggunakan YOLOv3 dan YOLOv2 dalam konteks deteksi manusia di dalam lift, namun penelitian tersebut belum melakukan perbandingan eksperimen secara komprehensif. Hal ini terlihat dari beberapa keterbatasan, yaitu:
1. Tidak menggunakan dataset dan kondisi pengujian yang identik untuk kedua model secara simultan.
2. Tidak melaporkan metrik evaluasi standar seperti precision, recall, dan F1-score secara komprehensif.
3. Tidak menganalisis secara kuantitatif pengaruh kepadatan objek terhadap performa masing-masing model.

Kesenjangan (literature gap) inilah yang menjadi landasan penelitian komparatif ini.

### C.2 Pendekatan Pemecahan Masalah
Penelitian ini bertujuan untuk:
1. Membandingkan nilai confidence rata-rata yang dihasilkan oleh YOLOv2 dan YOLOv3 dalam mendeteksi manusia pada rekaman CCTV lift.
2. Membandingkan akurasi penghitungan jumlah manusia yang terdeteksi antara YOLOv2 and YOLOv3.
3. Menganalisis waktu komputasi (processing time) yang dibutuhkan oleh masing-masing model.
4. Mengidentifikasi kondisi skenario (jumlah orang, kepadatan) di mana masing-masing model menunjukkan performa terbaik.

Penelitian ini mengusulkan pendekatan eksperimen komparatif terkontrol sebagai cara menjawab rumusan masalah secara empiris. YOLOv3 dipilih sebagai intervensi karena merupakan generasi yang lebih baru dengan arsitektur lebih dalam (53 layer) dan kemampuan deteksi multi-scale, sehingga secara teoritis seharusnya menghasilkan akurasi lebih tinggi. YOLOv2 ditetapkan sebagai baseline karena merupakan generasi sebelumnya yang lebih ringan dan telah digunakan dalam studi rujukan utama (Pamungkas et al., 2021), sehingga tersedia pembanding yang sah. Dengan menempatkan keduanya dalam kondisi eksperimen yang identik, penelitian ini dapat membuktikan apakah keunggulan teoritis YOLOv3 benar-benar terkonfirmasi secara empiris pada konteks spesifik CCTV lift.

Penelitian ini menggunakan tipe research question comparison untuk membandingkan performa YOLOv2 dan YOLOv3 pada proses deteksi dan penghitungan manusia menggunakan rekaman CCTV.

* **RQ Utama:** Bagaimana perbandingan performa YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia pada rekaman CCTV lift berdasarkan nilai confidence, akurasi deteksi, dan waktu komputasi?

Berdasarkan tujuan penelitian di atas, pertanyaan penelitian spesifik yang diajukan adalah:
* **RQ1:** Apakah YOLOv3 menghasilkan nilai confidence rata-rata yang lebih tinggi dibandingkan YOLOv2 dalam mendeteksi manusia pada citra CCTV lift?
* **RQ2:** Bagaimana perbandingan waktu komputasi (inference time) antara YOLOv2 dan YOLOv3 dalam proses deteksi manusia?
* **RQ3:** Pada skenario kepadatan manakah (rendah, sedang, tinggi) performa kedua model menunjukkan perbedaan paling signifikan?

**Hipotesis Penelitian (Testable & Terhubung ke RQ):**
* **Hipotesis 1 (Terkait RQ1 - Uji Akurasi/Confidence):**
  * H0: Tidak terdapat perbedaan signifikan pada nilai confidence score objek manusia yang dihasilkan oleh model YOLOv2 dan YOLOv3.
  * H1: Model YOLOv3 menghasilkan rata-rata nilai confidence score objek manusia yang lebih tinggi secara signifikan dibandingkan model YOLOv2.
* **Hipotesis 2 (Terkait RQ2 - Uji Waktu Komputasi):**
  * H0: Tidak terdapat perbedaan waktu komputasi (inference time) yang signifikan antara model YOLOv2 dan YOLOv3.
  * H1: Model YOLOv2 memiliki waktu komputasi (inference time) yang lebih cepat secara signifikan dibandingkan model YOLOv3.

### C.3 State of the Art dan Kebaruan Penelitian
Deteksi manusia berbasis deep learning menggunakan YOLO telah diaplikasikan secara luas dalam berbagai konteks. Redmon et al. (2016) memperkenalkan YOLO sebagai pendekatan deteksi objek real-time yang memproses seluruh citra dalam satu lintasan jaringan syaraf tunggal. Redmon & Farhadi (2017) mengembangkannya menjadi YOLOv2 dengan arsitektur Darknet-19 dan teknik anchor box, sedangkan Redmon & Farhadi (2018) memperkenalkan YOLOv3 dengan arsitektur Darknet-53 yang lebih dalam, dilengkapi residual connections dan kemampuan deteksi multi-skala. Lan et al. (2018) membuktikan efektivitas YOLO pada deteksi pejalan kaki dalam kondisi nyata. 

Pamungkas et al. (2021) menerapkan YOLOv2 dan YOLOv3 untuk deteksi manusia dalam lift dan melaporkan confidence rata-rata YOLOv3 sebesar 0.90 dibanding YOLOv2 sebesar 0.61. Khairunnas et al. (2021) menggunakan YOLOv4 pada mobile robot dan memperoleh mAP 87.03% dengan precision 0.83 and recall 0.86. Sugandi & Hartono (2022) mengimplementasikan YOLOv5 pada quadcopter dengan mAP 86.8%, serta Yanto et al. (2023) menunjukkan YOLOv8 mencapai mAP 95% pada deteksi pemakaian masker wajah.

Dari kajian tersebut, terlihat tiga pola yang berulang: 
1. Setiap generasi YOLO yang lebih baru menghasilkan akurasi lebih tinggi namun dengan waktu komputasi lebih panjang.
2. Studi-studi yang ada mengevaluasi satu versi YOLO secara mandiri, bukan membandingkan dua versi secara bersamaan dalam kondisi yang identik.
3. Tidak ada studi yang secara spesifik menganalisis performa YOLOv2 versus YOLOv3 pada konteks CCTV lift dengan variasi skenario kepadatan objek dan metrik evaluasi yang lengkap. 

Kondisi ideal yang dibutuhkan adalah adanya evaluasi komparatif terkontrol yang menggunakan dataset, threshold, dan prosedur pengujian yang identik untuk kedua model. Kondisi aktual menunjukkan bahwa hal ini belum dilakukan secara komprehensif, bahkan dalam studi yang paling relevan sekalipun (Pamungkas et al., 2021) yang melaporkan kedua model tetapi tidak membandingkannya dalam satu skenario eksperimen yang setara secara mendalam. 

Posisi penelitian ini adalah mengisi kesenjangan evaluatif tersebut. Kebaruan yang ditawarkan bukan pengembangan algoritma baru, melainkan tersedianya data komparatif yang valid secara metodologis dengan metrik lengkap (confidence, precision, recall, F1-score, IoU, dan waktu komputasi) pada skenario kepadatan berbeda yang menjadi dasar pemilihan model yang dapat dipertanggungjawabkan secara ilmiah.

### C.4 Peta Jalan Penelitian
Penelitian ini disusun secara bertahap mengikuti rangkaian worksheet (WS1–WS7) pada mata kuliah Riset dan Teknologi Informasi. Pada WS1 dilakukan identifikasi sistem dan konteks, yaitu kebutuhan deteksi otomatis pengguna lift berbasis CCTV. WS2 dan WS3 menghasilkan rumusan masalah dan identifikasi literature gap, yang menjadi dasar fokus penelitian komparatif ini. WS4 menghasilkan research question dan hipotesis, WS5 menetapkan variabel, metrik, dan instrumen pengukuran. WS6 berfokus pada persiapan sistem eksperimen meliputi pengumpulan dataset, konfigurasi Darknet, dan penetapan lingkungan komputasi. WS7 menghasilkan desain eksperimen lengkap mencakup skenario kepadatan, prosedur pengujian, dan mekanisme evaluasi. 

Tahap lanjutan yang diimplementasikan adalah eksekusi eksperimen pada citra uji CCTV lift yang telah disiapkan, analisis komparatif performa nyata YOLOv2 dan YOLOv3 melalui framework Darknet, serta penyusunan kesimpulan dan rekomendasi berbasis bukti hasil pengujian.

---

## D. Metode Penelitian

### D.1 Desain Penelitian, Unit Analisis, dan Penarikan Sampel
Penelitian ini menggunakan desain eksperimen komparatif terkontrol (controlled comparative experiment). Kondisi eksperimen dibuat identik untuk kedua model, yang mencakup penggunaan dataset training yang sama, nilai threshold yang sama (0.30), lingkungan perangkat keras GPU yang sama, serta metrik evaluasi yang sama. 

* **Unit Analisis:** Unit analisis dalam penelitian ini adalah berkas citra (image file) tunggal hasil ekstraksi rekaman video CCTV di dalam lift gedung bertingkat. Setiap citra diproses oleh masing-masing model YOLO untuk menghasilkan prediksi bounding box, nilai confidence, dan jumlah objek manusia.
* **Populasi Penelitian:** Populasi dalam penelitian ini adalah seluruh data visual (frame/citra) yang menangkap aktivitas manusia di dalam lingkungan internal lift gedung bertingkat dengan karakteristik sudut pandang atas (bird-eye view).
* **Sampel dan Teknik Sampling:** Sampel diambil menggunakan teknik **Purposive Sampling** (penarikan sampel bertujuan) sebanyak **4 citra karakteristik** yang berhasil diekstraksi dan divalidasi oleh sistem framework Darknet. Sampel sengaja dipilih secara selektif untuk mewakili kluster variasi tingkat kepadatan objek (rendah, sedang, dan tinggi) guna menguji batas kemampuan deteksi layer kedua model secara ekstrem.
* **Kriteria Inklusi dan Eksklusi Sampel:**
  1. *Kriteria Inklusi:* Citra berformat standar (.jpg/.png), diambil dari sudut pandang CCTV lift (bird-eye view), dan memuat objek kelas person (manusia) dengan variasi jumlah objek untuk membentuk skenario kepadatan.
  2. *Kriteria Eksklusi:* Citra yang mengalami kerusakan berkas (corrupted file), citra dengan pencahayaan ekstrem total yang merusak matriks piksel dasar, atau frame kosong yang tidak mengandung objek manusia sama sekali.

**Komparasi Kondisi Eksperimen:**
* **Kondisi A (Baseline):** Pengujian deteksi manusia menggunakan model **YOLOv2** dengan konfigurasi arsitektur Darknet-19 (23 lapisan konvolusional) memanfaatkan berkas bobot YOLOv2.weights yang berperan sebagai tolok ukur efisiensi kecepatan komputasi.
* **Kondisi B (Intervention):** Pengujian deteksi manusia menggunakan model **YOLOv3** dengan konfigurasi arsitektur Darknet-53 (53 lapisan konvolusional) memanfaatkan berkas bobot yolov3_training_last.weights yang berperan sebagai intervensi teknologi untuk meningkatkan akurasi deteksi multi-skala.

### D.2 Variabel, Metrik, Instrumen, dan Data

#### Definisi Variabel Eksplisit
1. **Variabel Independen (Independent Variable - IV):** Jenis arsitektur model algoritma YOLO yang digunakan pada framework Darknet, yaitu variabel nominal dikotomis: **YOLOv2** (Arsitektur Darknet-19) dan **YOLOv3** (Arsitektur Darknet-53).
2. **Variabel Dependen (Dependent Variable - DV):**
   * *DV1 - Nilai Confidence (%):* Skor keyakinan atau probabilitas yang mengeluarkan model bahwa objek di dalam bounding box adalah benar kelas manusia (rentang 0-100%).
   * *DV2 - Waktu Komputasi (milli-seconds):* Durasi pemrosesan (inference time) yang dibutuhkan sistem untuk menyelesaikan komputasi deteksi per satu citra.
   * *DV3 - Jumlah Objek Terdeteksi:* Banyaknya kuantitas manusia yang berhasil diidentifikasi dan diberi bounding box oleh model dibandingkan dengan ground truth.
3. **Variabel Kontrol:** Resolusi dimensi input gambar (416 x 416 piksel), nilai threshold deteksi (0.30), dan spesifikasi hardware environment (GPU Tesla T4).

#### Metrik Evaluasi
| Metrik | Definisi |
| :--- | :--- |
| Confidence Rata-rata | Rata-rata nilai confidence score seluruh objek terdeteksi dalam satu frame. |
| Precision | Rasio deteksi benar (True Positive) dari total objek yang diprediksi oleh model. |
| Recall | Rasio deteksi benar (True Positive) dari total keseluruhan objek ground truth. |
| F1-Score | Nilai rata-rata harmonik antara metrik Precision dan Recall. |
| Waktu Proses (ms) | Durasi total komputasi tingkat milidetik (milli-seconds) per sesi inference citra. |

#### Instrumen Pengukuran
1. **Framework Darknet:** Platform open-source berbasis C dan CUDA untuk eksekusi deteksi YOLOv2 dan YOLOv3.
2. **Google Colaboratory (GPU):** Lingkungan komputasi awan menggunakan akselerasi perangkat keras GPU Tesla T4.
3. **Python 3.x + OpenCV:** Bahasa pemrograman dan pustaka pendukung untuk penyiapan data, pre-processing, dan visualisasi luaran objek.
4. **LabelImg / Annotation Tool:** Alat pelabelan koordinat bounding box manusia untuk menentukan data ground truth (format .txt YOLO).
5. **Google Drive:** Tempat penyimpanan cloud terintegrasi untuk mengamankan dataset, file .cfg, dan berkas .weights.

#### Sumber Data
Dataset yang digunakan dalam penelitian ini terdiri dari dua sumber:
1. **Data Primer:** Berupa 1.500 citra hasil ekstraksi rekaman video CCTV lift untuk kebutuhan fase training model yang mengacu pada basis metodologi Pamungkas et al. (2021). Untuk pengujian aktual (testing), digunakan 4 citra representatif yang divalidasi secara ketat dan dikunci nilai ground truth-nya sebelum pengujian dimulai.
2. **Data Sekunder:** Subset kelas person dari COCO Dataset (Common Objects in Context) yang digunakan sebagai data latih tambahan untuk memperkaya bobot model terhadap variasi anatomi manusia.

### D.3 Skenario dan Prosedur Pengujian
Pengujian dilakukan pada tiga tingkat skenario berdasarkan volume kepadatan manusia di dalam frame citra:

| Skenario | Deskripsi Kondisi Visual | Target Jumlah Orang | Sampel Citra Uji |
| :--- | :--- | :--- | :--- |
| **Skenario A (Rendah)** | Objek terlihat utuh, jarak longgar, tidak ada oklusi. | 1 - 2 Orang | amigos.jpg |
| **Skenario B (Sedang)** | Objek berdekatan, terdapat oklusi sebagian/minor. | 3 - 4 Orang | leonel lara.jpg, download.jpg |
| **Skenario C (Tinggi)** | Objek saling berdesakan, oklusi tinggi/tumpang tindih. | 5 - 6 Orang atau lebih | @jaoyng on instagram.jpg |

*Nilai batasan threshold deteksi dikunci mutlak sebesar 0.30 (30%) untuk Kondisi A dan Kondisi B.*

#### Prosedur Pengujian (Step-by-Step)
1. Menyiapkan 4 citra uji terpiih (@jaoyng on instagram.jpg, leonel lara.jpg, amigos.jpg, download.jpg) di direktori `/content/drive/MyDrive/RTI/dataset/test/`.
2. Melakukan langkah pre-processing citra: penyesuaian ukuran (resize) ke dimensi 416 x 416 piksel agar sesuai dengan layer input konfigurasi jaringan.
3. Mengaktifkan framework Darknet pada Google Colab dengan memuat spesifikasi parameter komputasi GPU Tesla T4.
4. Menjalankan perintah inference untuk **Kondisi A (YOLOv2)** menggunakan file YOLOv2.cfg dan YOLOv2.weights dengan parameter `-thresh 0.30`.
5. Mencatat output log YOLOv2 yang meliputi: waktu proses (milli-seconds) dan daftar persentase confidence score dari objek person yang muncul.
6. Mengulangi langkah 4-5 untuk **Kondisi B (YOLOv3)** menggunakan berkas konfigurasi yolov3_training.cfg dan bobot yolov3_training_last.weights.
7. Mengompilasi seluruh data log kuantitatif dari kedua model ke dalam tabel ringkasan metrik evaluasi.

### D.4 Artifact dan Setup Implementasi
Spesifikasi teknis lingkungan implementasi komparatif disusun secara transparan pada tabel berikut:

| Komponen | YOLOv2 (Kondisi A - Baseline) | YOLOv3 (Kondisi B - Intervensi) |
| :--- | :--- | :--- |
| **Framework** | Darknet (C/CUDA) | Darknet (C/CUDA) |
| **Arsitektur Dasar** | Darknet-19 (23 Layers) | Darknet-53 (53 Layers) |
| **Beban Komputasi** | 29.475 BFLOPS | 65.879 BFLOPS |
| **File Konfigurasi** | YOLOv2.cfg | yolov3_training.cfg |
| **File Bobot (Weights)** | YOLOv2.weights | yolov3_training_last.weights |
| **Lingkungan Perangkat Keras** | GPU Tesla T4 (Cloud Env) | GPU Tesla T4 (Cloud Env) |
| **Dimensi Input** | 416 x 416 piksel | 416 x 416 piksel |
| **Jumlah Sampel Uji** | 4 Citra (Purposive) | 4 Citra (Purposive - Identik) |
| **Nilai Batasan Threshold** | 0.30 | 0.30 |

### D.5 Teknik Analisis dan Validitas
Metode analisis data dilakukan secara deskriptif-komparatif dengan membandingkan nilai parameter performa antar kedua model secara berpasangan (side-by-side analysis) untuk setiap citra uji yang mewakili skenario kepadatan.

* **Validitas Internal:** Dijamin melalui standarisasi variabel kontrol. Tidak ada perbedaan hardware, nilai threshold, ataupun urutan pembacaan gambar. Semua elemen dikondisikan konstan, sehingga perbedaan hasil murni dipengaruhi oleh perbedaan arsitektur internal model (IV).
* **Validitas Eksternal:** Batasan generalisasi hasil pengujian ini berlaku secara spesifik pada karakteristik visual CCTV lift (sudut pandang atas, jarak vertikal dekat, pencahayaan dalam ruang).
* **Reliabilitas Pengukuran:** Pengukuran reliabel karena seluruh data performa (confidence score dan waktu proses) ditarik langsung dari output log otomatis framework Darknet berbasis sistem komputer tanpa melibatkan penilaian subjektif manusia.

Penelitian menerapkan integritas ilmiah dengan mencatat nilai orisinal performa apa adanya sesuai luaran sistem komputasi tanpa manipulasi. Isu privasi data diantisipasi dengan menggunakan sampel citra akademik dari data riset terdahulu (Pamungkas et al., 2021) dan dataset publik COCO, serta membatasi analisis visual hanya pada pemrosesan bounding box objek tanpa melakukan identifikasi identitas personal individu (facial recognition).

### D.6 Batasan dan Asumsi Penelitian
* **Asumsi Penelitian:**
  1. Unit pemroses grafis (GPU Tesla T4) berada pada kondisi alokasi performa puncak yang stabil tanpa mengalami pembatasan bandwidth komputasi oleh penyedia cloud selama pengujian berlangsung.
  2. Pengujian menggunakan citra simulasi dengan perspektif horizontal/sejajar mata (eye-level view) memanfaatkan pantulan cermin interior lift untuk merepresentasikan ruang terbatas secara optimal.
  
* **Batasan Penelitian:**
  1. Penelitian difokuskan eksklusif pada objek kelas tunggal yaitu person (manusia). Kemunculan deteksi objek lain (seperti tas, ponsel, lampu) diabaikan dari kalkulasi akurasi utama.
  2. Jumlah data pengujian (testing) dibatasi pada 4 citra representatif menggunakan teknik purposive sampling. Batasan ini diterapkan sebagai langkah mitigasi teknis akibat adanya kendala I/O latency lag yang masif pada direktori Google Drive serta keterbatasan runtime memory pada Google Colab yang memicu crash (Out of Memory) saat pengujian skala besar.
  3. Sistem berjalan murni menggunakan kompilasi Darknet asli tanpa penambahan ekspansi modul optimasi visual dari pustaka OpenCV eksternal.

---

## E. Hasil yang Diharapkan
Berdasarkan fondasi teori arsitektur dan rumusan hipotesis, hasil eksperimen yang diharapkan adalah:
1. **Akurasi & Confidence Score:** YOLOv3 diharapkan mendominasi perolehan nilai confidence score (mendekati 100%) dibandingkan YOLOv2 pada seluruh citra uji. Hal ini dikarenakan adanya kontribusi fitur residual connections pada Darknet-53 yang mencegah degradasi akurasi pada jaringan dalam.
2. **Ketahanan Skenario Kepadatan (Oklusi):** Pada skenario kepadatan tinggi (@jaoyng on instagram.jpg), YOLOv3 diproyeksikan mampu mendeteksi objek manusia secara lebih solid dan meminimalisir risiko miss-detection berkat kemampuan multi-scale detection (deteksi pada 3 skala ukuran layer berbeda), sementara YOLOv2 diprediksi akan mengalami penurunan performa deteksi akibat efek oklusi objek yang berdempetan.
3. **Efisiensi Komputasi:** YOLOv2 akan mengungguli YOLOv3 secara konsisten dari aspek kecepatan pemrosesan (inference time). Dengan beban komputasi yang hanya 29.475 BFLOPS (dibandingkan YOLOv3 sebesar 65.879 BFLOPS), YOLOv2 diharapkan mencatatkan waktu proses di bawah 75 milidetik, menjadikannya opsi paling efisien untuk kebutuhan sistem real-time berspesifikasi rendah.

Luaran konkret dari riset ini adalah dokumen laporan analisis komparatif performa kuantitatif yang dilengkapi visualisasi bounding box objek sebagai rujukan saintifik penentuan model deteksi terbaik pada infrastruktur CCTV lift.

---

## F. Jadwal Penelitian
Rencana rangkaian aktivitas riset terbagi ke dalam alokasi waktu 7 minggu pelaksanaan:

| Kegiatan | M1 | M2 | M3 | M4 | M5 | M6 | M7 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 1. Studi Literatur & Pengumpulan Dataset | ✓ | ✓ | | | | | |
| 2. Persiapan Lingkungan Jaringan (Darknet & GPU) | | ✓ | ✓ | | | | |
| 3. Pre-processing & Pelabelan Ground Truth | | | ✓ | ✓ | | | |
| 4. Konfigurasi dan Training Model YOLO | | | | ✓ | ✓ | | |
| 5. Pengujian Eksperimen (Inference 4 Citra) | | | | | ✓ | ✓ | |
| 6. Analisis Data Komparatif Metrik | | | | | | ✓ | ✓ |
| 7. Penyusunan Laporan Jurnal & Simpulan | | | | | | | ✓ |

---

## G. Daftar Pustaka
* **[1]** Lan, W., Dang, J., Wang, Y., & Wang, S. (2018). Pedestrian Detection Based on YOLO Network Model. *2018 IEEE International Conference on Mechatronics and Automation (ICMA)*, Changchun, China, hal. 1547–1551. DOI: 10.1109/ICMA.2018.8484698
* **[2]** Pamungkas, B. P. G., Nugroho, B., & Anggraeny, F. (2021). Deteksi dan Menghitung Manusia Menggunakan YOLO-CNN. *Jurnal Informatika dan Sistem Informasi (JIFoSI)*, 2(1), 67–76.
* **[3]** Khairunnas, Yuniarno, E. M., & Zaini, A. (2021). Pembuatan Modul Deteksi Objek Manusia Menggunakan Metode YOLO untuk Mobile Robot. *Jurnal Teknik ITS*, 10(1), A50–A55. ISSN: 2337-3539
* **[4]** Sugandi, A. N., & Hartono, B. (2022). Implementasi Pengolahan Citra pada Quadcopter untuk Deteksi Manusia Menggunakan Algoritma YOLO. *Prosiding The 13th Industrial Research Workshop and National Seminar (IRWNS)*, Bandung, hal. 183–188.
* **[5]** Yanto, Aziz, F., & Irmawati. (2023). YOLO-V8 Peningkatan Algoritma untuk Deteksi Pemakaian Masker Wajah. *JATI (Jurnal Mahasiswa Teknik Informatika)*, 7(3), 1437–1444.
* **[6]** Redmon, J., Divvala, S., Girshick, R., & Farhadi, A. (2016). You Only Look Once: Unified, Real-Time Object Detection. *Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR)*, hal. 779–788. DOI: 10.1109/CVPR.2016.91
* **[7]** Redmon, J., & Farhadi, A. (2017). YOLO9000: Better, Faster, Stronger. *Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR 2017)*, hal. 7263–7271. arXiv:1612.08242
* **[8]** Redmon, J., & Farhadi, A. (2018). YOLOv3: An Incremental Improvement. *arXiv preprint*, arXiv:1804.02767, University of Washington.