# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi
jadi materi tersebut madalah materi 
### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database**: IEEE Xplore, ACM DL, Scopus, Google Scholar
2. **Boolean query** yang terdokumentasi eksplisit
3. **Snowballing**: backward (telusuri referensi) + forward (cari yang mengutip)
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Sistem rekomendasi dokter berbasis Content-Based Filtering pada kondisi data sparsity 
Database   : Google Scholar
Query      : "sistem rekomendasi dokter" AND "content-based filtering"
Tahun      : 2023-2025
Hasil awal : 12 paper → Screening → 5 paper final

Literature Matrix (concept-centric):
  
| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
| Prasetya et al. — *Peningkatan Akurasi Rekomendasi Dokter pada Kondisi Data Sparsity* | 2025 | Content-Based Filtering + Imputasi Mean/Mode + Pembobotan AHP + Cosine Similarity | 1.000 data dokter, 500 data pasien (dummy/sintetis), 5 atribut: spesialisasi, rating, biaya, lama praktik, jenis kelamin | MAE turun dari 0,145 → 0,102; RMSE turun dari 0,205 → 0,150 | Dataset dummy, belum diuji pada data real; hanya CBF, belum ada kombinasi hybrid |
| Yanuar et al. — *Implementasi Sistem Rekomendasi Dokter Berbasis CBF pada Layanan Konsultasi Kesehatan* | 2025 | Content-Based Filtering + TF-IDF + Cosine Similarity | Dataset profil dokter dari sumber terbuka (open source), 5 atribut: spesialisasi, lokasi, pengalaman, biaya, rating | Precision@3: 1,00; Recall@3: 0,60; F1@3: 0,75; Precision@5: 0,80; Recall@10: 0,90 | Tidak ada riwayat interaksi pengguna; tidak menangani data sparsity; hanya CBF murni |
| Yudha et al. — *Rancang Bangun Sistem Rekomendasi Artikel Kesehatan Anak Berbasis CBF* | 2025 | Content-Based Filtering + TF-IDF + Cosine Similarity + Text Preprocessing | 50+ artikel kesehatan anak (web scraping), domain spesifik anak | Precision: 67%; Recall: 100%; F1-Score: 80%; SUS Score: 69 (Okay) | Dataset sangat kecil, hanya 50 artikel; domain sangat terbatas; precision rendah (67%) |
| Permana & Miftahudin — *Penerapan CBF untuk Rekomendasi Resep Obat Berdasarkan Diagnosa Pasien* | 2025 | Content-Based Filtering + TF-IDF + Cosine Similarity | 47 data pasien dari Puskesmas, data diagnosa dan resep obat | Precision: 99,05%; Recall: 100%; F1-Score: 99,52% | Dataset sangat kecil (47 data); domain sangat spesifik (resep obat); hasil mungkin tidak bisa digeneralisasi ke konteks lain |
| Sugara et al. — *Peningkatan Sistem Rekomendasi Layanan Kesehatan Menggunakan UBCF dengan Imputasi KNN* | 2025 | User-Based Collaborative Filtering + Imputasi KNN + Pembobotan AHP + Weighted Pearson Correlation | 2.000 data dummy (interaksi pasien-dokter), 4 atribut: spesialisasi, gender, biaya, rating | RMSE turun dari 0,633 → 0,583 (turun 7,89%); MAE sedikit naik dari 0,502 → 0,511 | Dataset dummy; MAE sedikit meningkat setelah imputasi; UBCF masih mengalami kesulitan saat data sangat sparse |

Pola yang ditemukan:
  Metode dominan     : content-Based Filtering (CBF) dengan kombinasi TF-IDF dan Cosine Similarity adalah metode yang paling banyak dipakai. Hampir semua studi menggunakan cosine similarity sebagai dasar penghitungan kemiripan.
  Dataset umum       : Mayoritas penelitian (4 dari 5) menggunakan dataset dummy/sintetis karena sulitnya akses ke data pasien yang bersifat sensitif. Hanya Yudha et al. yang menggunakan data riil dari web scraping, itupun bukan data pasien melainkan artikel.
  Limitasi berulang  : Hampir semua studi memiliki dua kelemahan yang sama, yaitu penggunaan dataset sintetis sehingga belum tentu merepresentasikan kondisi nyata, dan belum ada yang mengkombinasikan CBF dengan pendekatan deep learning atau NLP yang lebih canggih untuk memahami konteks preferensi pengguna secara lebih mendalam.

GAP IDENTIFICATION

Gap 1: [Jenis:  Data Gap]
  Deskripsi    : seluruh penelitian yang ditemukan tentang rekomendasi dokter menggunakan dataset dummy atau sintetis. Tidak ada yang menggunakan data nyata dari platform kesehatan seperti Halodoc atau Alodokter.
  Bukti        : Prasetya et al. (2025) secara eksplisit menyatakan menggunakan "dataset dummy yang dibuat secara sintetik dengan bantuan Python." Sugara et al. (2025) juga menggunakan "simulasi data (Data Dummy)." Yanuar et al. (2025) menggunakan dataset profil dokter dari sumber terbuka. Tidak ada satu pun studi yang melibatkan interaksi pengguna nyata.
  Signifikansi  : Sistem rekomendasi yang hanya diuji pada data dummy belum tentu bisa bekerja baik di kondisi nyata. Data pasien asli memiliki pola yang jauh lebih kompleks dan beragam dibanding data sintetis. Hasil evaluasi yang bagus di data dummy tidak selalu bisa dijadikan jaminan performa di lapangan.

Gap 2: [Jenis: Method Gap]
  Deskripsi     : Semua penelitian CBF yang ditemukan baru menggunakan teknik pemrosesan fitur konvensional seperti TF-IDF dan one-hot encoding. Belum ada yang mencoba pendekatan representasi fitur yang lebih canggih, misalnya word embedding atau semantic similarity, untuk memahami preferensi pasien dari sisi tekstual yang lebih dalam.
  Bukti         : Yudha et al. (2025) dalam sarannya secara langsung menyebutkan perlunya "penggunaan metode pemrosesan bahasa alami (NLP) yang lebih lanjut, seperti word embedding atau semantic similarity." Yanuar et al. (2025) juga hanya mengandalkan TF-IDF untuk representasi fitur teks.Signifikansi  : Preferensi pasien dalam memilih dokter seringkali bersifat kontekstual dan sulit ditangkap hanya dengan TF-IDF biasa. Pendekatan NLP yang lebih canggih berpotensi meningkatkan relevansi rekomendasi secara signifikan.

Gap 3: [Jenis: Performance Gap]
  Deskripsi     :Pada sistem rekomendasi dokter berbasis CBF yang belum menangani data sparsity, precision masih rendah. Yanuar et al. mendapat precision 80% di Top-5 dan Yudha et al. hanya 67%. Bahkan Prasetya et al. sebelum imputasi memiliki MAE 0,145 dan RMSE 0,205 yang masih cukup tinggi.
  Bukti        : Yudha et al. (2025) menyatakan bahwa "Precision masih dapat ditingkatkan dengan memperbaiki algoritma rekomendasi." Prasetya et al. (2025) menunjukkan bahwa imputasi berhasil menurunkan MAE menjadi 0,102, namun masih belum mencapai hasil yang optimal karena atribut yang digunakan terbatas.
  Signifikansi  : Dalam konteks layanan kesehatan, rekomendasi yang tidak presisi bisa merugikan pasien karena mereka bisa mendapatkan dokter yang tidak sesuai dengan kebutuhan medisnya. Peningkatan akurasi di domain ini punya dampak yang lebih serius dibanding domain lain seperti hiburan atau e-commerce.

---

**Gap utama yang dipilih:** Kombinasi dari Data Gap dan Performance Gap
 penelitian tentang rekomendasi dokter masih sangat bergantung pada data dummy sehingga performa yang dilaporkan belum bisa dijadikan tolok ukur yang valid untuk kondisi nyata. Di sisi lain, teknik penanganan data sparsity yang ada (imputasi mean/mode atau KNN) sudah cukup membantu tapi belum optimal, terutama ketika atribut yang digunakan masih terbatas.

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
| CBF + Cosine Similarity tanpa penanganan data sparsity | Menyelesaikan problem yang sama persis yaitu merekomendasikan item berbasis kecocokan atribut profil pasien dan dokter, tanpa memerlukan data pengguna lain | Digunakan di 3 dari 5 paper yang ditemukan sehingga mewakili cara yang paling umum dilakukan sebelum ada teknik penanganan sparsity | Yanuar et al. (2025); Yudha et al. (2025); Permana & Miftahudin (2025) |
| CBF + Imputasi Mean/Mode + Pembobotan AHP + Cosine Similarity | Ini adalah pengembangan langsung dari kondisi tanpa sparsity handling, dan merupakan metode yang menjadi fokus utama penelitian yang digunakan sebagai acuan | Mewakili pendekatan terbaru di tahun 2025 untuk domain rekomendasi dokter yang sudah mengintegrasikan penanganan data sparsity, diterbitkan di jurnal Buana Informatika | Prasetya, Khudori & Pradini (2025) |

```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan Google Scholar atau database lain.

**Topik riset:** Sistem Rekomendasi Dokter Berbasis Content-Based Filtering dengan Penanganan Data Sparsity pada Platform Layanan Kesehatan Digital
**Query pencarian:** "sistem rekomendasi dokter content-based filtering", "doctor recommendation data sparsity", "collaborative filtering healthcare recommendation system"
**Database:** Google Scholar, JATI Jurnal Mahasiswa Teknik Informatika, Prosiding SENATIB, Jurnal SAINTEKOM

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Prasetya, Khudori & Pradini — *Peningkatan Akurasi Rekomendasi Dokter pada Kondisi Data Sparsity Menggunakan Algoritma CBF*, Jurnal Buana Informatika | 2025 | CBF + Imputasi Mean/Mode + Pembobotan AHP + Cosine Similarity | Dummy: 1.000 dokter, 500 pasien (Python-generated), sparsity 20% | MAE: 0,102; RMSE: 0,150 (turun signifikan setelah imputasi) | Dataset dummy, tidak diuji pada data real; saran ke depan: model hybrid dengan collaborative filtering atau deep learning |
| 2 | Yanuar, Aini, Samhan, Supriyanto & Al'Azzam — *Implementasi Sistem Rekomendasi Dokter Berbasis CBF pada Layanan Konsultasi Kesehatan*, SENATIB 2025 | 2025 | CBF + TF-IDF + Cosine Similarity | Dataset profil dokter open source (nama, spesialisasi, lokasi, pengalaman, biaya, rating) | Precision@3: 1,00; F1@3: 0,75; Precision@5: 0,80; Recall@10: 0,90 | Tidak menangani data sparsity; tidak ada riwayat interaksi pengguna; belum hybrid |
| 3 | Yudha, Ngoyem, Supangat & Dwi — *Rancang Bangun Sistem Rekomendasi Artikel Kesehatan Anak Berbasis CBF*, JATI Vol.9 No.5 | 2025 | CBF + TF-IDF + Cosine Similarity + Text Preprocessing (stemming, stopword removal) | 50+ artikel kesehatan anak (web scraping dari sumber terpercaya) | Precision: 67%; Recall: 100%; F1: 80%; SUS: 69 (Okay) | Dataset terlalu kecil; precision rendah; tidak bisa digeneralisasi ke topik lain |
| 4 | Permana & Miftahudin — *Penerapan CBF untuk Rekomendasi Resep Obat Berdasarkan Diagnosa Pasien*, Jurnal SAINTEKOM Vol.1 No.1 | 2025 | CBF + TF-IDF + Cosine Similarity | 47 data pasien dari kuesioner Puskesmas | Precision: 99,05%; Recall: 100%; F1: 99,52% | Dataset sangat kecil (47 data); domain sangat spesifik; hasil tidak bisa digeneralisasi |
| 5 | Sugara, Khudori & Haris — *Peningkatan Sistem Rekomendasi Layanan Kesehatan Menggunakan UBCF dengan Imputasi KNN*, JATI Vol.9 No.6 | 2025 | User-Based CF + Imputasi KNN + Pembobotan AHP + Weighted Pearson Correlation + 5-fold cross validation | 2.000 data dummy (pasien-dokter), 4 atribut | RMSE: 0,583 (turun 7,89%); MAE: 0,511 (sedikit naik dari 0,502) | Dataset dummy; MAE meningkat setelah imputasi; KNN masih kurang optimal untuk data sangat sparse |


**Pola yang terlihat:**
- **Metode dominan:** CBF dengan TF-IDF dan Cosine Similarity mendominasi hampir semua penelitian. AHP untuk pembobotan atribut juga mulai banyak digunakan.
- **Limitasi yang berulang:** Hampir semua penelitian masih menggunakan data dummy/sintetis, sehingga validitasnya di kondisi nyata belum teruji. Selain itu, teknik imputasi yang digunakan masih tergolong sederhana (mean, mode, atau KNN dasar).
______________________________

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | ✅ Ya | Precision sistem CBF rekomendasi dokter masih ada yang hanya mencapai 67% (Yudha et al.) dan 80% (Yanuar et al.). Bahkan pada sistem yang sudah menangani sparsity (Prasetya et al.), MAE masih 0,102 yang menunjukkan masih ada ruang perbaikan. Imputasi KNN pada Sugara et al. justru menaikkan MAE sedikit meski RMSE turun. |
| Method Gap | ✅ Ya | Belum ada penelitian rekomendasi dokter yang menggunakan representasi fitur berbasis NLP modern (word embedding, semantic similarity) untuk memahami preferensi pasien secara lebih kontekstual. Semua masih bergantung pada TF-IDF atau one-hot encoding yang sifatnya literal, bukan semantik. |
| Data Gap | ✅ Ya | Seluruh penelitian yang berfokus pada rekomendasi dokter menggunakan data dummy atau sintetis. Tidak ada yang diuji menggunakan data nyata dari platform kesehatan. Ini membuat validitas hasil evaluasi perlu dipertanyakan. |
| Context Gap | Tidak | Tidak ditemukan bukti eksplisit dari kelima jurnal yang menunjukkan gap konteks ini. Klaim tersebut tidak bisa dimasukkan karena tidak ada satu pun jurnal yang menyebutkannya secara langsung |

**Gap utama yang dipilih:**
Data Gap + Performance Gap (kombinasi keduanya)

**Mengapa gap ini penting:**
> Semua penelitian yang ada membuktikan bahwa CBF dengan imputasi memang bisa meningkatkan akurasi. Tapi karena datanya sintetis, kita tidak tahu apakah peningkatan itu juga akan terjadi di data nyata yang lebih kompleks dan beragam. Di sisi performa, teknik imputasi yang ada masih cenderung sederhana dan belum mempertimbangkan hubungan kompleks antar atribut, misalnya hubungan antara spesialisasi dokter dengan rentang biaya yang wajar atau pola rating berdasarkan pengalaman praktik. Gap ini penting karena di domain kesehatan, keakuratan rekomendasi punya dampak langsung ke keselamatan dan kepuasan pasien, bukan sekadar soal pengalaman belanja atau hiburan.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | CBF murni dengan TF-IDF + Cosine Similarity tanpa penanganan sparsity (pendekatan standar) | Menyelesaikan masalah yang persis sama: merekomendasikan dokter berdasarkan kecocokan atribut profil. Ini adalah cara paling umum yang digunakan sebelum ada penanganan sparsity. | Digunakan di 3 dari 5 paper yang ditemukan (Yanuar et al., Yudha et al., Permana & Miftahudin), sehingga mewakili *common practice* dalam domain ini. | Bukan SOTA, tapi ini adalah common practice yang jadi titik perbandingan yang jujur sebelum ditambahkan teknik penanganan sparsity. | Yanuar et al. (2025);  Yudha et al. (2025);  Permana & Miftahudin (2025) |
| 2 | CBF + Imputasi Mean/Mode + Pembobotan AHP (pendekatan dengan penanganan sparsity sederhana) | Ini adalah pengembangan langsung dari baseline pertama yang sudah menambahkan penanganan sparsity. Sangat relevan karena ini adalah metode yang menjadi fokus penelitian utama (Prasetya et al. 2025). | Mewakili state-of-the-art terbaru untuk domain rekomendasi dokter berbasis CBF dengan sparsity handling. Sudah diterbitkan di Jurnal Buana Informatika (2025) dan menjadi rujukan penelitian selanjutnya. | Ya, ini adalah pendekatan terbaru dan paling relevan di tahun 2025 untuk problem yang sama persis. | Prasetya, Khudori & Pradini (2025) |

**Apakah pemilihan baseline ini bisa dianggap straw man?** ❌ Tidak

> **Justifikasi:** Baseline pertama (CBF murni tanpa sparsity handling) dipilih bukan karena lemah, tapi karena memang itulah kondisi awal yang ingin diperbaiki. Ini setara dengan membandingkan sebelum dan sesudah treatment, bukan membanding-bandingkan metode yang tidak sebanding. Baseline kedua adalah yang paling kuat dan relevan yang tersedia di literatur terbaru. Kedua baseline ini dipilih untuk menggambarkan perkembangan nyata dari kondisi tanpa imputasi ke kondisi dengan imputasi, sehingga perbandingannya bermakna secara ilmiah.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Kalau kita bilang "belum ada yang meneliti ini" tanpa bukti apa-apa, itu cuma asumsi yang bisa langsung runtuh kalau reviewer menemukan satu paper saja yang ternyata sudah membahasnya. Gap yang valid itu beda dia muncul dari proses pencarian yang terdokumentasi, bukan dari ketidaktahuan kita.
> Cara membuktikan gap itu nyata ada beberapa langkah yang perlu dilakukan. Pertama, cari di database yang kredibel dengan query yang jelas dan tercatat. Kedua, bangun tabel perbandingan yang sistematis, kalau semua paper punya limitasi yang sama berulang, itu tanda bahwa gap memang ada. Ketiga, kutip langsung kalimat dari paper yang menyarankan penelitian lanjutan (misalnya saran Yudha et al. tentang NLP lebih lanjut, atau saran Prasetya et al. tentang model hybrid). Keempat, tunjukkan konsekuensi nyata dari gap itu. kenapa gap ini penting untuk ditutup, bukan cuma "karena belum ada yang meneliti."
