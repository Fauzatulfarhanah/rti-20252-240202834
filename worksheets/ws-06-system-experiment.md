# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: Bagaimana perbandingan kinerja YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia berdasarkan nilai confidence pada citra dari video CCTV?

Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
| Jenis metode (YOLOv2 dan YOLOv3) | IV | Modul deteksi objek YOLO | Mengganti model YOLOv2 atau YOLOv3 saat proses pengujian |
| Hasil deteksi manusia | DV | Output deteksi dan modul perhitungan objek | Mengukur nilai confidence dan jumlah manusia yang terdeteksi pada setiap frame |
| Kondisi input (citra CCTV yang sama) | CV | Dataset input video CCTV | Menggunakan dataset dan frame video yang sama pada kedua metode |


4 Prinsip Desain:
  [✅] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [✅] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [✅] Measurement Integration — Pengukuran DV built-in
  [✅] Reproducibility — Setup bisa direkonstruksi

Experimental Setup:
  Input data     : Frame citra dari video CCTV
  Parameter      : Model YOLOv2 dan YOLOv3 dengan threshold 0.30
  Output format  :  Nilai confidence dan jumlah manusia yang terdeteksi
```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** Bagaimana perbandingan kinerja YOLOv2 dan YOLOv3 dalam mendeteksi dan menghitung manusia berdasarkan nilai confidence pada citra dari video CCTV?

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
| Jenis metode (YOLOv2 dan YOLOv3) | IV | Modul deteksi objek YOLO | Mengganti model YOLOv2 dan YOLOv3 saat proses pengujian |
| Hasil deteksi manusia | DV | Modul output deteksi dan perhitungan objek | Mengukur nilai confidence dan jumlah manusia yang terdeteksi pada setiap frame |
| Kondisi input (citra CCTV yang sama) | CV | Dataset video CCTV | Menggunakan dataset dan frame video yang sama pada kedua metode |

**Apakah semua variabel bisa di-map?** [✅] Ya / [ ] Tidak
>  Semua variabel penelitian sudah memiliki komponen sistem yang sesuai.

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability | ✅ | Setiap variabel penelitian memiliki komponen sistem yang jelas, seperti jenis metode YOLOv2 dan YOLOv3 sebagai variabel bebas dan output deteksi sebagai variabel terikat |
| Modularity | ✅ | Model YOLOv2 dan YOLOv3 dapat diganti tanpa mengubah bagian sistem lainnya |
| Controllability | ✅ | Dataset video CCTV dan parameter pengujian dibuat sama untuk kedua metode agar hasil perbandingan tetap adil |
| Measurability | ✅ | Sistem secara otomatis menghasilkan output berupa nilai confidence dan jumlah manusia yang terdeteksi pada setiap frame |

**Prinsip mana yang paling sulit dipenuhi?** Controllability
**Strategi untuk mengatasinya:**
> Menggunakan dataset, parameter, dan kondisi pengujian yang sama agar hasil perbandingan antara YOLOv2 dan YOLOv3 tetap adil dan konsisten.

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|-------------|-------------|-------------|-----------------------|
| Full | ✅ YOLOv2/YOLOv3 | ✅ Confidence threshold | ✅ Dataset CCTV | Hasil deteksi dan perhitungan manusia berjalan optimal |
| – A | ❌ YOLOv3 (diganti YOLOv2) | ✅ | ✅ | Kemampuan deteksi kemungkinan menurun dibanding kondisi full |
| – B | ✅ | ❌ Tanpa confidence threshold | ✅ | Hasil deteksi menjadi kurang akurat karena objek yang terdeteksi bisa lebih banyak noise |
| – C | ✅ | ✅ | ❌ Dataset CCTV yang sama| Hasil pengujian menjadi kurang konsisten karena data input berbeda |

**Komponen mana yang diprediksi paling berkontribusi?**  
Komponen A (model YOLO)
**Mengapa?**
> Karena model YOLO merupakan komponen utama yang menentukan kemampuan sistem dalam mendeteksi dan menghitung manusia. Perbedaan arsitektur antara YOLOv2 dan YOLOv3 dapat memengaruhi nilai confidence dan jumlah objek yang terdeteksi.
---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Jika sistem dibangun seperti produk dengan banyak fitur sekaligus, maka hasil eksperimen bisa menjadi sulit dianalisis karena terlalu banyak faktor yang memengaruhi hasil penelitian. Hal ini dapat membuat variabel penelitian tidak terkontrol dengan baik.
> Arsitektur modular penting dalam riset karena memudahkan peneliti untuk mengubah atau menguji satu komponen tertentu tanpa memengaruhi komponen lainnya. Dengan begitu, proses pengujian menjadi lebih teratur dan hasil penelitian lebih mudah dibandingkan serta dianalisis.