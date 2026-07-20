# Jadwal & Log Pelaksanaan Penelitian

Catatan kronologis pelaksanaan tiap tahap (sumber: riwayat commit git & dokumen `09-docs/tahap-N-*.md`). Tanggal mengikuti data log pada repositori lokal.

## Log Pelaksanaan

| Tanggal | Tahap | Aktivitas | Referensi |
|---|---|---|---|
| 2026-05-1 s.d. 2026-05-31 | Tahap 1 & 2 | Perancangan skema eksperimen komparatif terkontrol; studi literatur perbedaan arsitektur Darknet-19 (YOLOv2) vs Darknet-53 (YOLOv3); setup environment Google Colab bertenaga GPU NVIDIA Tesla T4; kompilasi kerangka Darknet asli berbasis C/CUDA via berkas Makefile (`GPU=1`, `CUDNN=1`, `OPENCV=1`). | [09-docs/tahap-1-studi-arsitektur.md](../09-docs/tahap-1-studi-arsitektur.md), [09-docs/tahap-2-setup-darknet.md](../09-docs/tahap-2-setup-darknet.md) |
| 2026-06-06 | Tahap 3 | Pengumpulan dataset awal sebanyak **150 citra uji**. Eksekusi pengujian skala besar massal dilakukan melalui terminal CLI, namun memicu kendala teknis berupa *I/O latency lag* yang masif pada direktori Google Drive serta menyebabkan *runtime memory* Google Colab mengalami *crash*/*timeout* (Out of Memory). | [09-docs/tahap-3-pengujian-otomatisasi.md](../09-docs/tahap-3-pengujian-otomatisasi.md) |
| 2026-06-13 s.d. 2026-07-1 | Tahap 3 | **Peralihan Strategi Metodologis:** Mitigasi kendala *resource constraint* dilakukan dengan menerapkan teknik *purposive sampling*, mereduksi kuantitas menjadi **4 citra uji yang paling representatif** mencakup skenario kepadatan Rendah (`amigos.jpg`), Sedang (`download.jpg`, `leonel lara.jpg`), dan Tinggi (`@jaoyng on instagram.jpg`). Eksekusi ulang dijalankan secara sekuensial menggunakan parameter *headless* `-dont_show` untuk mengamankan stabilitas server. | commit "Mitigasi runtime crash via purposive sampling 4 citra representatif dan aktivasi headless mode" (2026-06-14) |
| 2026-07-3 | Tahap 4 | Pembangunan pipeline analisis data untuk mengekstraksi data kuantitatif dari *raw log console* terminal. Data metrik *inference time* (milidetik) dan *confidence score* (%) berhasil direkapitulasi ke dalam berkas `tabel_komparasi_analisis.csv` di folder output. Resolusi *error X11 display* ditangani menggunakan skrip *patching* `cv2_imshow` untuk mengekspor visualisasi *bounding box*. | [09-docs/tahap-4-analisis-data.md](../09-docs/tahap-4-analisis-data.md), [06-output/](../06-output/) |
| 2026-07-10 | Tahap 5 | Penyusunan draf konten naskah ilmiah (8 bagian terstruktur) di direktori `07-manuskrip/` dengan target publikasi ke Jurnal UPB. Proses pembaruan data kuantitatif berbasis hasil eksperimen 4 citra representatif diintegrasikan secara menyeluruh ke dokumen proposal (`01-proposal/`), tinjauan pustaka (`02-literatur/`), dan laporan akhir (`08-laporan/`). | [09-docs/tahap-5-draf-paper.md](../09-docs/tahap-5-draf-paper.md), [08-laporan/laporan-penelitian_example.md](../08-laporan/laporan-penelitian_example.md) |
| 2026-07-12 | Tahap 5 | Identifikasi dan pencarian referensi literatur utama nyata (termasuk *paper* fundamental YOLO oleh Joseph Redmon & Ali Farhadi, serta studi komparasi sejenis oleh Pamungkas et al., 2021). Penyusunan bibliografi secara terstruktur menggunakan Mendeley dan melakukan sinkronisasi dokumen sitasi pada `daftar-pustaka.bib`. | [02-literatur/matriks-literatur.md](../02-literatur/matriks-literatur.md), [02-literatur/daftar-pustaka.bib](../02-literatur/daftar-pustaka.bib), [07-manuskrip/naskah-jurnal.md](../07-manuskrip/naskah-jurnal.md) |

## Status Ringkas

- **Tahap 1–4**: Selesai (Dataset final berbasis 4 citra uji representatif multi-skenario kepadatan berhasil diekstraksi secara kuantitatif per tanggal 2026-06-14).
- **Tahap 5**: Konten naskah utama selesai dengan pembahasan *trade-off* komparasi parameter komputasi Darknet-19 vs Darknet-53; menyisakan pemindahan format ke gaya selingkung Jurnal UPB.

## Item Tindak Lanjut (Checklist Sebelum Submission)

- [x] Lengkapi matriks literatur dengan paper *related work* nyata (Pamungkas et al., Redmon & Farhadi) — Referensi terverifikasi sahih
- [x] Dokumentasikan mitigasi teknis *runtime crash* akibat batas kapasitas komputasi Google Colab pada Bab Kendala Eksperimen
- [ ] Sesuaikan bahasa dan format penulisan naskah akhir di [07-manuskrip/naskah-jurnal.md](../07-manuskrip/naskah-jurnal.md) dengan panduan penulis (*author guidelines*) Jurnal UPB
- [ ] Pindahkan konten draf manuskrip ke dalam template resmi dokumen Jurnal UPB (`.docx`)
- [ ] Finalisasi penempatan visual gambar hasil deteksi *bounding box* sesuai dengan urutan pembahasan skenario kepadatan
- [ ] Review akhir seluruh klaim numerik metrik *inference time* dan persentase *confidence score* agar konsisten dan sinkron antar dokumen laporan

## Korespondensi
