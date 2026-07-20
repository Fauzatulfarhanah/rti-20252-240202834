# Tahap 5 — Penulisan Draf Paper Jurnal

**Status:** Konten naskah selesai — naskah konsolidasi tersedia di `07-manuskrip/naskah-jurnal.md`, tinjauan pustaka lengkap dengan referensi domain visi komputer terverifikasi (BibTeX di `02-literatur/daftar-pustaka.bib`). Sisa pekerjaan: keputusan bahasa final & pemindahan ke template jurnal tujuan (lihat "Yang Masih Perlu Dilengkapi").  
**Bergantung pada:** `tahap-4-analisis-data.md` — Selesai  
**Lokasi Berkas Dokumentasi:** `09-docs/tahap-5-draf-paper.md`

---

## Tujuan

Menyusun draf naskah ilmiah dengan gaya bahasa akademis formal, objektif, dan terstruktur mengenai komparasi performa YOLOv2 vs YOLOv3 untuk deteksi objek manusia pada ruang lift tertutup, disesuaikan untuk target publikasi Sinta 2 atau Jurnal Internasional Terindeks.

## Rencana Deliverable (Struktur Naskah & Pemetaan Folder)

Proses penulisan naskah didistribusikan dan diorganisasikan secara modular ke dalam struktur direktori riset sebagai berikut:

| Bagian Naskah | Lokasi Berkas Fisik | Status Konten |
|---|---|---|
| Naskah Utama Konsolidasi | `07-manuskrip/naskah-jurnal.md` | Selesai — Gabungan draf utuh dari pendahuluan hingga kesimpulan. |
| Abstrak (ID & EN) | Konten di dalam `07-manuskrip/naskah-jurnal.md` | Selesai — Ringkasan latar belakang lift padat, trade-off model, dan hasil final. |
| Pendahuluan | Konten di dalam `07-manuskrip/naskah-jurnal.md` | Selesai — Rumusan masalah mengenai oklusi objek manusia dan keterbatasan ruang CCTV lift. |
| Tinjauan Pustaka & Teori | `02-literatur/matriks-literatur.md`<br><br>`03-teori/arsitektur-dan-skema.md` | Selesai — Kajian komparatif struktur dalam Darknet-19 vs Darknet-53 serta dasar teori ekstraksi fitur multi-skala. |
| Metodologi Pengujian | Konten di dalam `07-manuskrip/naskah-jurnal.md` | Selesai — Alur otomatisasi skrip looping Python (`05-kode/YOLOv2` & `05-kode/YOLOv3`) di lingkungan Google Colab GPU Tesla T4. |
| Hasil & Analisis Pembahasan | Konten di dalam `07-manuskrip/naskah-jurnal.md` | Selesai — Mengacu langsung pada tabulasi data kuantitatif dari log konsol di folder `06-output/`. |
| Kesimpulan & Saran | Konten di dalam `07-manuskrip/naskah-jurnal.md` | Selesai — Rekomendasi pemilihan model berdasarkan ambang batas kecepatan real-time (30 FPS). |
| Daftar Pustaka (Bibliografi) | `02-literatur/daftar-pustaka.bib` | Selesai — Kumpulan sitasi ilmiah berformat BibTeX (terhubung ke Mendeley/Zotero). |

## Peta Sumber Daya Berdasarkan Direktori Kerja

Penyusunan manuskrip akhir memanfaatkan seluruh aset yang tersebar di dalam folder penelitian:

- `00-admin/` & `01-proposal/`: Digunakan sebagai acuan pemenuhan target timeline riset dan landasan awal justifikasi pemilihan topik visi komputer pada lift.
- `03-teori/`: Memuat gambar aset visual (`image.png` dan `Untitled Diagram.drawio (24).png`) yang merepresentasikan diagram alur pipa data (*pipeline*) pengujian citra dari Drive ke terminal Darknet Colab.
- `05-kode/`: Menyimpan dokumentasi skrip bersih automated-testing YOLOv2 dan YOLOv3 yang siap dilampirkan pada bagian lampiran paper atau di-share ke repositori publik.
- `06-output/`: Menjadi basis data utama penulisan Bab 4 Jurnal, berisi rangkuman performa inference time (ms) dan tingkat Confidence Score (%) per tingkatan skenario kepadatan citra.
- `08-laporan/` (`laporan-penelitian_example.md`): Menampung narasi deskriptif versi panjang (gaya laporan institusional/tugas akhir) yang menjadi jangkar perluasan pembahasan naskah jurnal.

## Yang Masih Perlu Dilengkapi Sebelum Submit

- **Keputusan Bahasa Final Naskah:** Penentuan akhir penggunaan bahasa. Jika ditargetkan ke Sinta 2, pertahankan isi naskah di `07-manuskrip/naskah-jurnal.md` dalam Bahasa Indonesia formal. Jika dialihkan ke Scopus, lakukan translasi menyeluruh ke Bahasa Inggris ilmiah.
- **Pemindahan ke Berkas Word (.docx):** Peneliti perlu menyalin teks dari berkas markdown `naskah-jurnal.md` ke dalam format dokumen Microsoft Word sesuai dengan gaya selingkung (author guidelines) dari jurnal tujuan.
- **Penyisipan Gambar Visualisasi Utama:** Memasukkan potongan gambar `predictions.jpg` (hasil render `cv2_imshow` dari Tahap 3) yang menunjukkan perbandingan grafis bounding box manusia pada kondisi oklusi tinggi sebagai Key Figure di bab hasil.
- **Kelengkapan Metadata Penulis:** Mengisi nama penulis, instansi/afiliasi, dan email korespondensi pada kolom placeholder yang terletak di baris atas naskah.