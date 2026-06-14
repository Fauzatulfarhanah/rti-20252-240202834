# WS-08: Proposal Integration (UTS)

> **Bab 8 — Proposal & Checkpoint**

---

## Ringkasan Materi

### Proposal = Satu Argumen Utuh

Proposal riset bukan kumpulan bab yang independen. Ia adalah **satu argumen** yang mengalir dari masalah ke rencana solusi. Jika satu koneksi putus, seluruh proposal kehilangan koherensi.

### Integration Map — 6 Koneksi Kritis

```
Problem (Bab 2) → Gap (Bab 3) → RQ & H (Bab 4) → Metrik (Bab 5) → Sistem (Bab 6) → Eksperimen (Bab 7)
```

| Koneksi | Pertanyaan Verifikasi |
|---------|----------------------|
| Problem → Gap | Apakah gap muncul dari analisis literatur terhadap masalah? |
| Gap → RQ | Apakah RQ langsung menjawab gap yang teridentifikasi? |
| RQ → Metrik | Apakah setiap variabel di RQ punya metrik terdefinisi? |
| Metrik → Sistem | Apakah setiap metrik bisa diukur oleh komponen sistem? |
| Sistem → Eksperimen | Apakah desain eksperimen menggunakan sistem sebagai instrumen? |

### Koherensi Vertikal + Horizontal

- **Vertikal** — Alur logis atas-ke-bawah (problem → experiment)
- **Horizontal** — Konsistensi terminologi (nama variabel di RQ = di hipotesis = di metrik = di desain)

### Jebakan Kognitif

| Jebakan | Deskripsi |
|---------|----------|
| "Selling" Introduction | Menulis promosi, bukan menyajikan data dan gap |
| Copy-paste Methodology | Menyalin deskripsi tekstbook tanpa menyesuaikan ke RQ |
| Optimistic Timeline | Meremehkan waktu implementasi; selalu tambah buffer 30-50% |
| No Possibility of Failure | Mengimplikasikan hasil pasti sukses — proposal jujur mengakui H₀ mungkin tidak ditolak |

### Struktur Proposal

1. **Pendahuluan** — Latar belakang + problem statement (Bab 1-2)
2. **Tinjauan Pustaka** — Literature review + gap + baseline (Bab 3)
3. **RQ / Kontribusi / Hipotesis** — (Bab 4)
4. **Metodologi** — Metrik + sistem + desain eksperimen (Bab 5-7)
5. **Timeline & Output**

### Istilah Penting

- **Integration Map** — Diagram 6 koneksi kritis antar komponen proposal
- **Vertical Coherence** — Alur logis atas-ke-bawah
- **Horizontal Coherence** — Konsistensi terminologi di semua bagian
- **Checkpoint** — Titik self-assessment sebelum transisi dari desain ke eksekusi

---

## Template A.8 — Integration Checklist

```
PROPOSAL INTEGRATION CHECKLIST

Koneksi Vertikal (Flow Atas-Bawah):
  [✅] Problem → Gap: masalah terdokumentasi di literatur
  [✅] Gap → RQ: pertanyaan menjawab gap spesifik
  [✅] RQ → Hypothesis: hipotesis memprediksi jawaban
  [✅] Hypothesis → Metric: metrik mengukur variabel dalam hipotesis
  [✅] Metric → System: komponen sistem menghasilkan/mengukur metrik
  [✅] System → Experiment: desain eksperimen menggunakan sistem

Koneksi Horizontal (Konsistensi):
  [✅] Istilah sama di semua bagian
  [✅] Variabel di RQ = variabel di hipotesis = metrik di desain
  [✅] Scope tidak berubah dari masalah ke eksperimen

Rubrik Self-Assessment:
| Kriteria | 1 (Lemah) | 2 (Cukup) | 3 (Baik) | Skor |
|----------|-----------|-----------|----------|------|
| Koherensi | Koneksi antar komponen tidak jelas | Sebagian koneksi ada tapi belum eksplisit | Semua 6 koneksi kritis terhubung jelas dan konsisten | 3 |
| Specificity | Metrik tidak terdefinisi numerik | Metrik ada tapi sebagian masih umum | Metrik numerik lengkap (confidence 0–1, threshold 0.30, 150 citra, 10 video, 3 skenario kepadatan) | 3 |
| Feasibility | Dataset/tools tidak tersedia | Tools tersedia, jadwal terlalu optimistis | Dataset teridentifikasi (1.500 train, 150 test), tools konkret, namun jadwal 7 minggu cukup padat dan bergantung pada GPU Colab gratis | 2 |
| Rigor | Tidak ada kontrol variabel | Ada kontrol variabel, analisis deskriptif saja tanpa prosedur yang jelas | Kontrol variabel ketat (dataset, threshold, hardware identik), namun analisis hanya deskriptif tanpa uji statistik inferensial untuk klaim "signifikan" | 2 |
```

---

## Latihan 1 — Kompilasi Proposal Mini

Kumpulkan hasil dari WS-02 sampai WS-07 menjadi satu ringkasan proposal.

| Komponen | Sumber | Isi (1–2 kalimat) |
|----------|--------|-------------------|
| Problem Statement | WS-02 | Sistem lift konvensional tidak mampu mendeteksi jumlah penumpang secara otomatis, padahal diperlukan pembatasan kapasitas lift. Oleh karena itu dibutuhkan sistem berbasis CCTV untuk mendeteksi dan menghitung manusia secara otomatis. |
| Gap | WS-03 | Penelitian sebelumnya telah menggunakan YOLOv2 dan YOLOv3 untuk deteksi manusia di lift, namun belum melakukan perbandingan komprehensif dengan dataset, threshold, dan kondisi pengujian yang identik serta metrik evaluasi yang lengkap. |
| RQ | WS-04 | Bagaimana perbandingan performa YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia pada rekaman CCTV lift berdasarkan confidence, akurasi deteksi, dan waktu komputasi? |
| Hipotesis | WS-04 | H₁: Terdapat perbedaan signifikan performa antara YOLOv2 dan YOLOv3 berdasarkan confidence, precision, recall, F1-score, dan waktu komputasi pada deteksi manusia menggunakan CCTV. |
| Variabel & Metrik | WS-05 | IV = jenis model YOLO (YOLOv2 vs YOLOv3). DV = confidence, jumlah objek terdeteksi, dan waktu komputasi. Metrik evaluasi meliputi Precision, Recall, F1-Score, IoU, dan Confidence rata-rata. |
| Sistem | WS-06 | Sistem menggunakan Darknet, Google Colab GPU, Python + OpenCV, LabelImg, Google Drive, timer Python, dan spreadsheet pencatatan metrik untuk proses training, inference, dan evaluasi. |
| Desain Eksperimen | WS-07 | Eksperimen komparatif terkontrol menggunakan dataset yang sama (150 citra dan 10 video CCTV lift), threshold 0,30, perangkat keras identik, serta tiga skenario kepadatan (rendah, sedang, tinggi). |

---

## Latihan 2 — Integration Checklist

Verifikasi 6 koneksi kritis. Isi dengan merujuk tabel di Latihan 1.

| Koneksi | Status | Bukti |
|----------|---------|---------|
| Problem → Gap | ✅ | Gap muncul langsung dari analisis literatur terhadap masalah. Penelitian Pamungkas et al. (2021) telah menggunakan YOLOv2 dan YOLOv3 untuk deteksi manusia di lift, namun belum melakukan perbandingan komprehensif dengan dataset, threshold, dan kondisi pengujian yang identik serta belum melaporkan metrik evaluasi lengkap seperti precision, recall, dan F1-score. |
| Gap → RQ | ✅ | RQ utama secara langsung menjawab gap yang ditemukan, yaitu membandingkan performa YOLOv2 dan YOLOv3 pada deteksi dan penghitungan manusia menggunakan CCTV lift berdasarkan confidence, akurasi deteksi, dan waktu komputasi. |
| RQ → Hypothesis | ✅ | H₁ memprediksi adanya perbedaan signifikan performa antara YOLOv2 dan YOLOv3 berdasarkan confidence, precision, recall, F1-score, dan waktu komputasi. H₀ menyatakan tidak terdapat perbedaan signifikan sehingga kemungkinan hasil tidak sesuai prediksi tetap diakomodasi. |
| Hypothesis → Metric | ✅ | Seluruh variabel dalam hipotesis memiliki metrik yang terdefinisi. Confidence diukur menggunakan nilai confidence rata-rata (0–1), akurasi deteksi diukur menggunakan precision, recall, F1-score, dan IoU, sedangkan efisiensi model diukur menggunakan waktu proses dalam satuan detik. |
| Metric → System | ✅ | Setiap metrik dapat dihasilkan dan diukur oleh komponen sistem. Darknet menghasilkan nilai confidence dan hasil deteksi objek, LabelImg menyediakan ground truth untuk perhitungan precision, recall, F1-score, dan IoU, sedangkan timer Python digunakan untuk mengukur waktu komputasi. |
| System → Experiment | ✅ | Sistem digunakan secara langsung dalam desain eksperimen. YOLOv2 dan YOLOv3 dijalankan menggunakan Darknet pada Google Colaboratory GPU dengan dataset yang sama (150 citra dan 10 video), threshold identik (0,30), serta tiga skenario kepadatan (rendah, sedang, tinggi) sehingga hasil kedua model dapat dibandingkan secara adil. |

**Koneksi mana yang paling lemah?** Hypothesis → Metric,  karena hipotesis menyatakan adanya perbedaan signifikan antara YOLOv2 dan YOLOv3, sedangkan metrik yang direncanakan hanya dianalisis menggunakan statistik deskriptif. Belum dijelaskan metode statistik inferensial yang digunakan untuk membuktikan apakah perbedaan tersebut benar-benar signifikan.

**Bagaimana cara memperkuatnya?**
> Tambahkan metode uji statistik inferensial, seperti independent t-test atau Mann-Whitney test, untuk membandingkan nilai confidence, precision, recall, F1-score, IoU, dan waktu komputasi antara YOLOv2 dan YOLOv3. Dengan demikian, keputusan menerima atau menolak H₀ dapat didasarkan pada bukti statistik yang jelas.

**Konsistensi horizontal — apakah istilah dan scope konsisten?** [✅] Ya / [ ] Tidak
> Seluruh istilah utama digunakan secara konsisten dari Problem Statement hingga Desain Eksperimen. Variabel yang diteliti tetap sama, yaitu perbandingan YOLOv2 dan YOLOv3 untuk deteksi dan penghitungan manusia pada rekaman CCTV lift. Metrik yang digunakan (confidence, precision, recall, F1-score, IoU, dan waktu komputasi) juga konsisten muncul pada RQ, hipotesis, variabel dan metrik, sistem, serta desain eksperimen. Scope penelitian tetap berfokus pada deteksi manusia pada CCTV lift dan tidak berubah ke konteks atau objek lain.

---

## Latihan 3 — Rubrik Self-Assessment

Evaluasi proposal mini menggunakan rubrik.

| Kriteria | Skor (1-3) | Justifikasi |
|-----------|-----------|-------------|
| Koherensi | 3 | Alur proposal sudah runtut mulai dari identifikasi masalah, gap penelitian, research question, hipotesis, metrik, sistem, hingga desain eksperimen. Setiap bagian saling mendukung dan tidak terdapat perubahan fokus penelitian. |
| Specificity | 3 | Variabel, metrik, dataset, threshold, jumlah sampel, serta skenario pengujian telah dijelaskan secara spesifik dan terukur sehingga prosedur penelitian dapat direplikasi. |
| Feasibility | 2 | Kebutuhan dataset, perangkat lunak, dan lingkungan komputasi sudah teridentifikasi dengan jelas. Namun, jadwal penelitian selama tujuh minggu cukup padat karena mencakup proses persiapan data, konfigurasi model, pengujian, analisis, dan penyusunan laporan. |
| Rigor | 2 | Penelitian telah mengontrol beberapa variabel penting seperti dataset, threshold, dan perangkat keras agar perbandingan kedua model berlangsung adil. Namun, analisis yang direncanakan masih terbatas pada statistik deskriptif sehingga belum sepenuhnya mendukung pengujian signifikansi hipotesis. |

**Skor total:** 10 / 12

**Apakah proposal siap untuk fase eksekusi?** [✅] Ya / [ ] Belum
> Proposal sudah memiliki tujuan, variabel, metrik, sistem, dan desain eksperimen yang jelas. Sebelum implementasi, akan lebih baik jika ditambahkan metode uji statistik inferensial untuk memperkuat proses pengambilan kesimpulan terhadap hipotesis penelitian.

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-08, bagian mana yang paling mudah dan paling sulit? Mengapa? Apa yang akan dilakukan berbeda jika mengulang dari awal?

**Bagian termudah:** Menentukan topik dan merumuskan problem statement karena masalah yang diangkat memiliki konteks yang jelas serta didukung oleh penelitian sebelumnya mengenai deteksi manusia menggunakan YOLO pada CCTV lift.

**Bagian tersulit:** Menyusun gap penelitian dan menghubungkannya dengan research question, hipotesis, serta desain eksperimen. Bagian ini membutuhkan analisis literatur yang lebih teliti agar setiap komponen proposal saling terhubung dan tidak keluar dari fokus penelitian.

**Yang akan dilakukan berbeda:**
> Jika mengulang dari awal, saya akan mengumpulkan dan memetakan referensi penelitian terlebih dahulu sebelum menyusun research question dan hipotesis agar proses identifikasi gap menjadi lebih terarah.

> Saya juga akan mulai menyusun rancangan eksperimen sejak awal sehingga penentuan variabel, metrik, dan kebutuhan data dapat disesuaikan dengan tujuan penelitian secara lebih konsisten.
