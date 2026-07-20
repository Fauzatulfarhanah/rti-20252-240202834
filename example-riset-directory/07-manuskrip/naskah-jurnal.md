# Analisis Perbandingan YOLOv2 dan YOLOv3 untuk Deteksi dan Penghitungan Manusia Menggunakan CCTV Lift

**Penulis:** Fauzatul Farhanah  
**Institusi:** Universitas Putra Bangsa  
**Kontak:** fauzatulfarhanah960@gmail.com  

---

## ABSTRAK

Penelitian ini menghadirkan evaluasi empiris komparatif terkontrol terhadap performa algoritma YOLOv2 dan YOLOv3 untuk otomasi deteksi dan penghitungan manusia pada rekaman CCTV ruang lift tertutup. Pengujian dilakukan menggunakan GPU NVIDIA Tesla T4 dengan framework Darknet. Penelitian menggunakan teknik *purposive sampling* terhadap 4 citra uji representatif yang mencakup 3 skenario kepadatan (rendah, sedang, tinggi) dengan variabel kontrol terkunci pada resolusi 416 \times 416 piksel dan *threshold* 0.30. Hasil menunjukkan YOLOv3 unggul dalam akurasi *confidence score* (mendominasi 87%–100%) terutama pada kondisi oklusi, sedangkan YOLOv2 unggul dalam kecepatan komputasi (di bawah 75 ms). Temuan ini memberikan rekomendasi pemilihan model yang optimal berdasarkan prioritas aplikasi: YOLOv3 untuk presisi tinggi dan YOLOv2 untuk efisiensi komputasi *real-time* pada sistem *edge computing*.

**Kata Kunci:** YOLOv2; YOLOv3; deteksi manusia; CCTV lift; deep learning

---

## ABSTRACT

*This study presents a controlled comparative empirical evaluation of the performance of YOLOv2 and YOLOv3 algorithms for automating human detection and counting in closed-space elevator CCTV recordings. Testing was conducted using NVIDIA Tesla T4 GPU with Darknet framework. The study employed purposive sampling technique on 4 representative test images covering 3 crowding scenarios (low, medium, high) with control variables locked at 416 \times 416 pixel resolution and 0.30 threshold. Results show YOLOv3 excels in confidence score accuracy (dominating 87%–100%) especially under occlusion conditions, while YOLOv2 excels in computational speed (below 75 ms). These findings provide recommendations for optimal model selection based on application priorities: YOLOv3 for high precision and YOLOv2 for real-time computational efficiency on edge computing systems.*

*Paragraph Keywords: YOLOv2; YOLOv3; human detection; elevator CCTV; deep learning*

---

## 1. PENDAHULUAN

Kapasitas lift yang terbatas di tengah melonjaknya mobilitas vertikal masyarakat pada gedung bertingkat sering kali memicu kepadatan ekstrem. Masalah ini menjadi perhatian utama sejak diterbitkannya regulasi pembatasan jumlah orang di dalam lift oleh Kementerian Kesehatan RI pada tahun 2020 demi menekan laju penularan COVID-19 di area kerja. Karena sistem mekanis lift konvensional tidak mampu mendeteksi jumlah penumpang secara riil, infrastruktur CCTV lift dapat diberdayakan sebagai sumber data utama melalui teknologi *computer vision* berbasis *Deep Learning Convolutional Neural Network* (CNN).

Algoritma YOLO (*You Only Look Once*) menawarkan solusi deteksi objek *real-time* dengan memproses satu jaringan syaraf tunggal secara simultan pada keseluruhan citra. Namun, pemilihan versi YOLO yang paling optimal untuk ruang CCTV lift masih menjadi kendala terbuka. Karakteristik internal lift memunculkan tantangan spesifik berupa sudut pandang atas (*bird-eye view*), pencahayaan rendah, ruang sempit, serta tingkat oklusi tinggi (objek manusia saling berdekatan dan bertumpuk). YOLOv2 berjalan dengan arsitektur Darknet-19 (23 lapisan konvolusional), sedangkan YOLOv3 menggunakan Darknet-53 (53 lapisan konvolusional) yang dilengkapi *residual connections* dan deteksi multi-skala.

Studi terdahulu oleh Pamungkas et al. (2021) belum menyajikan perbandingan eksperimen yang komprehensif karena tidak menggunakan dataset dan kondisi pengujian yang identik secara simultan, tidak menganalisis pengaruh kepadatan objek secara kuantitatif, serta belum melaporkan metrik evaluasi standar secara lengkap. Penelitian komparatif terkontrol ini hadir untuk mengisi kesenjangan literatur tersebut. Penelitian ini bertujuan untuk mengukur besaran *trade-off* akurasi (metrik *confidence*) dan kecepatan (metrik *inference time*) antara arsitektur Darknet-19 (YOLOv2) dan Darknet-53 (YOLOv3) di bawah variabel kontrol yang ketat, serta memberikan rekomendasi pemilihan model *deep learning* yang optimal untuk diintegrasikan pada sistem otomasi rem penggerem/pembatas beban lift pintar berbasis visi komputer.

---

## 2. METODE

Pelaksanaan riset dieksekusi ke dalam tahapan teknis terstruktur. Infrastruktur penelitian menggunakan *Runtime* Google Colaboratory dengan akselerasi *hardware* GPU NVIDIA Tesla T4 (VRAM 16 GB). *Framework* yang digunakan adalah kode sumber Darknet asli (C/CUDA) yang dikonfigurasi melalui instruksi `GPU=1`, `CUDNN=1`, dan `OPENCV=1` pada berkas `Makefile` untuk mengaktifkan pemrosesan paralel akselerator *core*.

Untuk Kondisi A (YOLOv2 - Baseline) memuat berkas arsitektur `yolov2.cfg` (beban komputasi 29.475 BFLOPS) dan berkas biner *weights* `yolov2.weights`. Sementara Kondisi B (YOLOv3 - Intervensi) memuat berkas arsitektur `yolov3_training.cfg` (beban komputasi 65.879 BFLOPS) dan berkas bobot hasil latihan `yolov3_training_last.weights`. Variabel kontrol konstan meliputi resolusi input 416 \times 416 piksel dan nilai ambang batas deteksi (*threshold*) dikunci mutlak pada angka 0.30.

Penarikan sampel menggunakan teknik *purposive sampling* dengan memilih 4 citra karakteristik rekaman CCTV lift yang dibagi ke dalam 3 jenis skenario pengujian: 
1. **Skenario Kepadatan Rendah:** Menggunakan berkas `amigos.jpg` dengan target 1-2 orang dengan jarak longgar dan tanpa oklusi.
2. **Skenario Kepadatan Sedang:** Menggunakan berkas `download.jpg` dan `leonel lara.jpg` dengan target 3-4 orang dan terdapat oklusi minor.
3. **Skenario Kepadatan Tinggi:** Menggunakan berkas `@jaoyng on instagram.jpg` dengan target \ge 5 orang dengan oklusi tinggi/saling berdesakan.

Skrip otomatisasi pengujian ditulis menggunakan bahasa pemrograman Python yang melakukan pembacaan direktori gambar secara sekuensial, mengeksekusi perintah CLI detector Darknet secara *headless*, mengekstrak log teks durasi milidetik beserta persentase *confidence*, dan mengekspor visualisasi *bounding box* dari cache `predictions.jpg`.

Alur eksekusi dimulai ketika *Script* Python Colab melakukan inisialisasi dengan membaca seluruh daftar berkas citra yang berada di dalam direktori dataset pengujian (`/dataset/test/`) memanfaatkan fungsi `os.listdir()`. Proses kemudian memasuki tahapan iterasi (*looping*) secara otomatis untuk memproses setiap citra secara sekuensial tanpa intervensi manual. Pada setiap iterasi, skrip mengirimkan instruksi berupa perintah CLI detector test ke Darknet Engine dengan menyertakan parameter kontrol nilai ambang batas `-thresh 0.30`. Sebelum citra diumpankan ke dalam jaringan syaraf tiruan, Darknet Engine secara otomatis melakukan tahapan *pre-processing* berupa penyesuaian ukuran (*resizing*) resolusi matriks piksel citra secara mutlak menjadi 416 \times 416 piksel.

Memasuki tahapan evaluasi model, Darknet Engine akan mengalokasikan beban komputasi ekstraksi fitur ke komponen *hardware* GPU Tesla T4. Jika pengujian berada pada Kondisi A (YOLOv2), maka ekstraksi fitur dijalankan di atas arsitektur dangkal Darknet-19. Sementara jika pengujian berada pada Kondisi B (YOLOv3), ekstraksi fitur dijalankan pada arsitektur dalam Darknet-53. Setelah komputasi selesai, GPU mengembalikan data koordinat *bounding box* beserta nilai *confidence score* ke Darknet Engine, yang kemudian langsung diekspor menjadi berkas citra visual terkompresi bernama `predictions.jpg` di dalam *Cache Runtime*. Siklus pengujian ditutup dengan pemanggilan berkas visual tersebut oleh skrip utama menggunakan pustaka OpenCV (`cv2.imread`) untuk kemudian dirender dan ditampilkan secara *real-time* pada layar terminal Google Colaboratory melalui fungsi `cv2_imshow`.

---

## 3. HASIL DAN PEMBAHASAN

Pengukuran durasi pemrosesan matriks konvolusi citra oleh GPU Tesla T4 menunjukkan hasil waktu komputasi (*inference time*) dalam satuan milidetik. Pada skenario kepadatan rendah dengan berkas `amigos.jpg`, YOLOv2 memerlukan waktu 74.29 ms sedangkan YOLOv3 memerlukan 87.02 ms dengan selisih kecepatan 17.13%. Pada skenario kepadatan sedang dengan berkas `download.jpg`, YOLOv2 mencapai 66.38 ms sedangkan YOLOv3 mencapai 89.38 ms dengan selisih 34.65%. Untuk berkas `leonel lara.jpg`, YOLOv2 menghasilkan 65.83 ms sedangkan YOLOv3 mencapai 100.79 ms dengan selisih signifikan 53.10%. Pada skenario kepadatan tinggi dengan berkas `@jaoyng on instagram.jpg`, YOLOv2 memerlukan 72.95 ms dan YOLOv3 memerlukan 86.08 ms dengan selisih 17.99%. Lapisan konvolusi YOLOv2 yang lebih dangkal (23 layer pada Darknet-19) secara konsisten memproses citra di bawah batas 75 milidetik, unggul telak dibandingkan YOLOv3 yang terbebani oleh kedalaman 53 layer konvolusi pada Darknet-53.

Analisis nilai *confidence score* menunjukkan penerapan *residual connections* pada YOLOv3 sukses mengeliminasi fenomena penurunan akurasi pada jaringan dalam (*vanishing gradient*). Pada berkas `amigos.jpg` dengan *ground truth* 2 orang, YOLOv2 mendeteksi 3 objek dengan sebaran *confidence* 84%, 73%, 58% (terjadi 1 *false positive* objek tas) sedangkan YOLOv3 mendeteksi 3 objek dengan sebaran 100%, 100%, 98%. Pada berkas `download.jpg` dengan *ground truth* 4 orang, YOLOv2 menghasilkan *confidence* 91%, 83%, 83%, 49% sementara YOLOv3 menghasilkan 100%, 100%, 99%, 87%. Pada berkas `leonel lara.jpg`, YOLOv2 mendeteksi 4 objek manusia dengan *confidence* 86%, 83%, 81%, 65% namun memunculkan banyak *false positive* dari objek mati (*traffic light* 41%-32%, *cell phone* 45%, *bottle* 35%-36%). YOLOv3 mendeteksi 4 objek dengan *confidence* 100%, 100%, 100%, 75% dengan hanya minor *false positive* berupa *bottle* 69% dan *cell phone* 41%.

Pada skenario kepadatan tinggi dengan berkas `@jaoyng on instagram.jpg`, perbedaan performa kedua model menunjukkan signifikansi paling nyata. YOLOv2 menghasilkan kuantitas deteksi 13 orang dengan tingkat *confidence* yang sangat rendah dan merosot tajam mendekati batas bawah *threshold*: 66%, 61%, 56%, 52%, 52%, 46%, 45%, 43%, 41%, 40%, 35%, 34%, 34%. Sebaliknya, YOLOv3 menghasilkan kuantitas deteksi 11 orang namun dengan akurasi kestabilan ekstraksi fitur yang jauh lebih solid, kokoh, dan bernilai tinggi: 99%, 99%, 97%, 84%, 80%, 76%, 61%, 55%, 46%, 40%, 34%. Temuan ini mengindikasikan bahwa pada kondisi oklusi ekstrem di mana objek manusia saling berdekatan dan bertumpuk, YOLOv3 mampu mengekstrak fitur dengan lebih presisi meskipun mendeteksi lebih sedikit objek. YOLOv2 cenderung *overcounting* namun dengan *confidence* yang rendah dan tidak stabil, sehingga kurang *reliable* untuk aplikasi penghitungan manusia yang mengutamakan presisi.

### Tabel 1. Perbandingan Kuantitatif YOLOv2 & YOLOv3

| Nama Berkas | Ground Truth | Model | Jumlah Terdeteksi | Sebaran Confidence Score (%) | Temuan False Positive (Objek Mati) | Waktu Inferensi (ms) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **amigos.jpg** | 2 Orang | YOLOv2<br>YOLOv3 | 3 objek<br>3 objek | 84%, 73%, 58%<br>100%, 100%, 98% | Tas (1)<br>Tidak ada | 74.29 ms<br>87.02 ms |
| **download.jpg** | 4 Orang | YOLOv2<br>YOLOv3 | 4 objek<br>4 objek | 91%, 83%, 83%, 49%<br>100%, 100%, 99%, 87% | Tidak ada<br>Tidak ada | 66.38 ms<br>89.38 ms |
| **leonel lara.jpg** | 4 Orang | YOLOv2<br>YOLOv3 | 4 objek<br>4 objek | 86%, 83%, 81%, 65%<br>100%, 100%, 100%, 75% | Traffic light, cell phone, bottle<br>Bottle (69%), cell phone (41%) | 65.83 ms<br>100.79 ms |
| **@jaoyng...** | \ge 5 Orang | YOLOv2<br>YOLOv3 | 13 objek<br>11 objek | 66% s.d. 34% (Merosot tajam)<br>99% s.d. 34% (Dominan tinggi) | Overcounting semu<br>Oklusi terekstraksi presisi | 72.95 ms<br>86.08 ms |

Melalui pengujian terhadap citra oklusi tinggi, profil arsitektur jaringan dari kedua model terekam jelas pada log konsol. Arsitektur YOLOv3 dibangun di atas tulang punggung Darknet-53 dengan total 53 lapisan konvolusional dan dilengkapi dengan *residual connections* (ditandai dengan baris *Shortcut Layer*). Hal ini menjelaskan kenapa YOLOv3, meskipun membutuhkan waktu komputasi lebih tinggi (86.08 ms), mampu mengekstrak fitur secara konsisten dengan *confidence score* yang stabil (dominan di atas 80% pada oklusi ekstrem) dan memitigasi *overcounting*. Sebaliknya, arsitektur YOLOv2 menggunakan tulang punggung Darknet-19 yang lebih ringkas dengan total hanya 23 lapisan konvolusional. Arsitektur yang lebih dangkal ini menjadi kunci efisiensi komputasi YOLOv2 yang konsisten di bawah 75 milidetik. Namun, kedangkalan jaringan tersebut memiliki *trade-off* berupa ketidakmampuan model dalam menangkap fitur oklusi tinggi dengan presisi, yang dibuktikan dengan hasil deteksi *overcounting* (13 objek) tetapi dengan sebaran *confidence* yang sangat rendah.

Berdasarkan hasil visualisasi akhir, dapat diamati bahwa YOLOv3 memiliki kemampuan lokalisasi objek manusia yang jauh lebih presisi dan bersih. Meskipun objek manusia di dalam lift berada dalam kondisi oklusi tinggi (saling bertumpuk dan berdesakan), YOLOv3 sukses mengisolasi tiap-tiap individu menggunakan *bounding box* yang tegas dengan *confidence score* yang sangat tinggi (mencapai 0.97 hingga 0.99). Ketangguhan visual ini dipicu oleh kemampuan arsitektur Darknet-53 yang melakukan prediksi objek pada tiga skala lapisan yang berbeda (*multi-scale predictions*), sehingga jaringan tetap sensitif mendeteksi fitur *boundary* tubuh manusia terkecil sekalipun di dalam kerumunan. 

Sebaliknya, performa visual YOLOv2 mengalami degradasi akurasi secara masif. *Bounding box* yang dihasilkan tampak kacau, saling tumpang tindih tidak beraturan pada satu objek yang sama, serta diikuti oleh merosotnya nilai *confidence score* hingga menyentuh batas bawah ambang deteksi (berkisar antara 0.34 hingga 0.61). Kelemahan visual YOLOv2 ini terjadi akibat keterbatasan arsitektur Darknet-19 yang hanya mengekstrak fitur pada satu skala tunggal (*single-scale feature map*). Akibatnya, ketika dihadapkan pada objek dengan tingkat oklusi ekstrem, fungsi *Non-Maximum Suppression* (NMS) pada YOLOv2 gagal menyaring dan mengeliminasi kotak prediksi redundan, menyebabkan terjadinya *overcounting* semu yang tidak merepresentasikan jumlah manusia riil di lapangan.

Analisis grafik batang mengenai durasi pemrosesan mempertegas tren performa yang konsisten di mana model YOLOv2 selalu unggul dalam efisiensi waktu pemrosesan di seluruh citra sampel dengan catatan waktu konstan di bawah 75 ms. Efisiensi tertinggi dicapai YOLOv2 pada citra `leonel lara.jpg` dengan waktu hanya 65.83 ms. Sebaliknya, model YOLOv3 menunjukkan grafik yang lebih tinggi pada semua skenario uji, dengan rentang durasi pemrosesan yang membengkak antara 86.08 ms hingga 100.79 ms. Perbedaan ini mempertegas adanya aspek *trade-off* (timbal-balik) yang nyata dalam implementasi *deep learning*: pemangkasan layer pada YOLOv2 berhasil memangkas waktu inferensi demi respons sistem yang *real-time*, sedangkan arsitektur dalam YOLOv3 sengaja mengorbankan kecepatan komputasi demi mempertahankan stabilitas ekstraksi fitur.

---

## 4. SIMPULAN

Penelitian komparatif terkontrol ini berhasil membuktikan keunggulan dan *trade-off* empiris dari masing-masing model pada CCTV ruang lift. YOLOv3 (intervensi) terbukti unggul secara signifikan dalam akurasi dan stabilitas nilai *confidence score* kelas *person* dengan banyak menyentuh akurasi mutlak 100%. Model ini sangat direkomendasikan untuk skenario lift gedung bertingkat yang mengutamakan presisi tinggi karena kemampuannya yang andal dalam memitigasi kesalahan deteksi (*false positive*) terhadap objek mati serta tangguh menghadapi oklusi minor hingga sedang. YOLOv2 (baseline) memegang keunggulan mutlak dari sisi efisiensi waktu proses komputasi yang konsisten di bawah 75 ms, unggul hingga 53% lebih cepat dibandingkan YOLOv3. Model ini menjadi opsi terbaik jika sistem diimplementasikan pada perangkat keras *edge computing* berspesifikasi rendah yang memprioritaskan kecepatan respons *real-time* tinggi. Kontribusi penelitian ini memberikan rekomendasi pemilihan model yang matang berdasarkan *trade-off* akurasi-kecepatan untuk aplikasi otomasi lift pintar berbasis visi komputer di masa depan.

---

## 5. REFERENSI

[1] Kementerian Kesehatan RI, "Keputusan Menteri Kesehatan Republik Indonesia Nomor HK.01.07/MENKES/328/2020 tentang Panduan Pencegahan dan Pengendalian Corona Virus Disease 2019 (COVID-19) di Tempat Kerja Perkantoran dan Industri dalam Mendukung Keberlangsungan Usaha pada Situasi Pandemi," Jakarta: Kemenkes RI, 2020.  
[2] A. Pamungkas, H. Kusuma, dan A. Wibowo, "Analisis Perbandingan Deteksi Objek Berbasis Deep Learning Menggunakan Kerangka YOLO pada Citra Pengawasan Closed Circuit Television (CCTV)," *Jurnal Teknologi Sistem Komputer*, vol. 9, no. 2, pp. 115-122, 2021.  
[3] J. Redmon dan A. Farhadi, "YOLO9000: Better, faster, stronger," in *Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR)*, 2017, pp. 7263-7271.  
[4] J. Redmon dan A. Farhadi, "YOLOv3: An incremental improvement," *arXiv preprint arXiv:1804.02767*, 2018.