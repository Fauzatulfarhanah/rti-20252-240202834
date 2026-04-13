# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Sistem Rekomendasi
  Konteks  : Aplikasi layanan kesehatan (rekomendasi dokter)

System Context
  Input       : Data dokter (spesialisasi, rating, biaya, pengalaman, jenis kelamin) dan data kebutuhan pasien
  Process     : Data diolah menggunakan metode Content-Based Filtering dan teknik imputasi untuk mengatasi data yang tidak lengkap
  Output      : Daftar rekomendasi dokter
  Outcome     : Pasien lebih mudah menemukan dokter yang sesuai
  Constraints : Banyak data yang tidak lengkap
  Stakeholders: Pasien, dokter, dan penyedia aplikasi

Fenomena → Problem
  Fenomena yang diamati             : Aplikasi kesehatan sudah menyediakan fitur rekomendasi dokter
  Gejala (symptom) yang terukur     : Hasil rekomendasi sering tidak sesuai dengan kebutuhan pasien, dengan nilai error yang masih cukup tinggi (MAE 0.142 dan RMSE 0.205)
  Masalah yang didiagnosis          : Data yang digunakan tidak lengkap sehingga sistem sulit mencocokkan
  Masalah riset (researchable)      : Bagaimana meningkatkan akurasi sistem rekomendasi dokter pada kondisi data tidak lengkap menggunakan pendekatan Content-Based Filtering
  Variabel yang terukur             : Nilai MAE dan RMSE

Problem Quality Check
  [✅] Clarity — Apakah satu orang membaca akan paham?
  [✅] Measurability — Apakah ada metrik kuantitatif?
  [✅] Relevance — Apakah penting untuk domain?
  [✅] Testability — Apakah bisa gagal?
  [✅] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
  Saat ini banyak aplikasi kesehatan yang menyediakan rekomendasi dokter untuk membantu pasien. Namun, hasil rekomendasi yang diberikan sering tidak sesuai dengan kebutuhan pengguna. Salah satu penyebabnya adalah data yang digunakan tidak lengkap, sehingga sistem kesulitan dalam mencocokkan dokter dengan kebutuhan pasien. Kondisi ini menunjukkan bahwa sistem yang ada masih belum optimal dalam menangani data yang terbatas. Karena itu, perlu dilakukan penelitian untuk melihat bagaimana cara meningkatkan akurasi sistem rekomendasi dokter pada kondisi data yang tidak lengkap. Untuk mengukurnya, digunakan nilai MAE dan RMSE agar bisa diketahui seberapa baik sistem bekerja.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Sistem rekomendasi dokter pada kondisi data tidak lengkap

| Tahap | Hasil |
|-------|-------|
| Reality | Aplikasi kesehatan membantu pasien memilih dokter |
| Observed Issue (Symptom) | Nilai error sistem masih cukup tinggi (MAE 0.142 dan RMSE 0.205) |
| Diagnosed Problem (Root Cause) | Data dokter tidak lengkap |
| Researchable Problem | Bagaimana meningkatkan akurasi rekomendasi saat data tidak lengkap |
| Measurable Variable | MAE dan RMSE |

**Apakah terjebak solution-first thinking?** [ ] Ya / [x] Tidak, karena permasalahan ditentukan terlebih dahulu dari kondisi nyata dan penyebabnya, baru kemudian mengarah ke solusi.

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Data dokter dan kebutuhan pasien |
| Process | Sistem mengolah data menggunakan Content-Based Filtering dan teknik imputasi untuk mengatasi data yang tidak lengkap |
| Output | Rekomendasi dokter |
| Outcome | Pasien lebih cepat menemukan dokter yang cocok |
| Constraints | Data yang tidak lengkap (data sparsity) dan keterbatasan informasi pada atribut dokter |
| Stakeholders | Pasien, dokter, dan penyedia aplikasi kesehatan |

**Komponen mana yang paling relevan dengan masalah riset?** Process, karena di sini data yang tidak lengkap diolah. Dari sini bisa dilihat apakah sistem bisa tetap memberikan rekomendasi yang tepat atau tidak.

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 5 | Mudah dipahami |
| Measurability | 5 | Menggunakan MAE dan RMSE |
| Relevance | 5 | Masalah nyata |
| Testability | 4 | Bisa diuji menggunakan data dan metode tertentu, tapi membutuhkan dataset yang cukup |
| Impact | 5 | Berguna bagi pengguna |

**Skor total:** 24 / 25

**Problem statement versi final (1 paragraf):**
> Sistem rekomendasi dokter pada aplikasi kesehatan sebenarnya sangat membantu pengguna. Tapi, hasil rekomendasi masih sering tidak sesuai dengan kebutuhan pasien. Hal ini terjadi karena data yang digunakan oleh sistem tidak lengkap, sehingga proses pencocokan kurang akurat. Karena itu, perlu dicari cara agar sistem bisa memberikan rekomendasi yang lebih akurat meskipun datanya tidak lengkap. Untuk melihat hasilnya, digunakan MAE dan RMSE sebagai ukuran seberapa baik rekomendasi yang dihasilkan.
---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah saat coding biasanya langsung terlihat, seperti program error atau tidak berjalan. Kita bisa fokus mencari letak kesalahannya lalu memperbaikinya. Misalnya saat menggunakan Visual Studio Code, biasanya sudah terlihat bagian mana yang error, jadi lebih mudah untuk diperbaiki. Sedangkan dalam riset, masalahnya tidak selalu terlihat jelas. Kita perlu memahami dulu kondisi yang terjadi, mencari penyebab utamanya, lalu merumuskan masalah tersebut agar bisa dianalisis lebih lanjut. Setelah itu, kita menentukan cara untuk melihat seberapa besar masalah tersebut, misalnya dengan menggunakan data atau hasil pengukuran tertentu. Dari situ baru bisa dinilai apakah masalahnya sudah teratasi atau belum. Jadi, riset membutuhkan pemikiran yang lebih terstruktur dibandingkan memperbaiki error pada coding.