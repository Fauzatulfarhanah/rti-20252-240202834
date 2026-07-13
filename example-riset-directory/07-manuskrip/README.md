# 07-manuskrip

Draf naskah ilmiah — **Tahap 5**, target publikasi Sinta 2 (Jurnal RESTI).

## Naskah Konsolidasi

- [naskah-jurnal.md](naskah-jurnal.md) — Naskah lengkap hasil penggabungan seluruh bab dalam template standar (Judul/Penulis, Abstrak ID+EN, §1 Pendahuluan – §5 Kesimpulan, Daftar Pustaka).
- [naskah-jurnal.docx](naskah-jurnal.docx) — Hasil konversi ke format Microsoft Word (dibangun otomatis via `python build_docx.py` tanpa memerlukan pandoc).

## Struktur Naskah Per Bagian (Sumber / Draf Kerja)

Untuk mempermudah penulisan, draf artikel ilmiah dipecah ke dalam beberapa berkas kerja berikut:

* [00-outline.md](00-outline.md) — Outline penelitian, peta sumber data, dan daftar klaim kunci komparasi performa YOLOv2 vs YOLOv3 yang harus konsisten di seluruh bab.
* [01-abstrak.md](01-abstrak.md) — Abstrak bahasa Indonesia dan bahasa Inggris (berisi ringkasan latar belakang lift padat, tujuan komparasi, metodologi Darknet, dan ringkasan hasil metrik ms/*confidence score*).
* [02-pendahuluan.md](02-pendahuluan.md) — Pendahuluan (latar belakang pentingnya menghitung kapasitas manusia di dalam lift via CCTV, masalah oklusi/objek bertumpuk, rumusan masalah, dan kontribusi penelitian).
* [03-tinjauan-pustaka.md](03-tinjauan-pustaka.md) — Tinjauan Pustaka (teori *deep learning* untuk *object detection*, arsitektur jala surya Darknet-19 pada YOLOv2, arsitektur Darknet-53 pada YOLOv3, serta penelitian terdahulu terkait deteksi manusia).
* [04-metodologi.md](04-metodologi.md) — Metodologi (lingkungan eksperimen Google Colab + GPU Tesla T4, konfigurasi berkas `.cfg` dan `.weights`, penentuan *threshold* 0.30, serta karakteristik 4 citra uji lift yang digunakan).
* [05-hasil-analisis.md](05-hasil-analisis.md) — Hasil & Analisis (memaparkan data dari folder `06-output/`, analisis *trade-off* kecepatan vs akurasi, pembahasan fenomena deteksi 13 vs 11 orang pada citra `@jaoyng on instagram.jpg`, dan analisis *false positive* pada YOLOv2).
* [06-kesimpulan.md](06-kesimpulan.md) — Kesimpulan & Saran (jawaban atas model YOLO mana yang paling optimal direkomendasikan untuk CCTV lift beserta saran pengembangan riset ke depan).
* [07-daftar-pustaka.md](07-daftar-pustaka.md) — Daftar Pustaka penelitian (berisi referensi ilmiah utama yang dirujuk, disusun menggunakan format IEEE).

> *Catatan: File `naskah-jurnal.md`/`.docx` adalah gabungan final dari bagian-bagian di atas. Proses perapian akhir sesuai gaya selingkung (template kolom, margin, dan manajemen sitasi) Jurnal RESTI dilakukan secara mandiri oleh peneliti.*

## Acuan

* [../09-docs/tahap-5-draf-paper.md](../09-docs/tahap-5-draf-paper.md)
























# 07-manuskrip

Draf naskah ilmiah — **Tahap 5**, target publikasi Sinta 2 (Jurnal RESTI/Telematika) atau Scopus Q3-Q4.

## Naskah konsolidasi

- [naskah-jurnal.md](naskah-jurnal.md) — naskah lengkap dalam template jurnal standar (Judul/Penulis, Abstrak ID+EN, §1 Pendahuluan – §5 Kesimpulan, Daftar Pustaka)
- [naskah-jurnal.docx](naskah-jurnal.docx) — hasil konversi ke .docx (dibangun via `python build_docx.py`, lihat [build_docx.py](build_docx.py); tidak memerlukan pandoc)

## Struktur naskah per bagian (sumber/draf kerja)

- [00-outline.md](00-outline.md) — outline, peta sumber, dan daftar klaim kunci yang harus konsisten
- [01-abstrak.md](01-abstrak.md) — Abstrak (ID & EN)
- [02-pendahuluan.md](02-pendahuluan.md) — Pendahuluan (latar belakang, rumusan masalah, tujuan, kontribusi)
- [03-tinjauan-pustaka.md](03-tinjauan-pustaka.md) — Tinjauan Pustaka (JWT/JWKS, mitigasi, *related work*; lihat [../02-literatur/](../02-literatur/))
- [04-metodologi.md](04-metodologi.md) — Metodologi (arsitektur eksperimen, skema hybrid caching, skenario k6)
- [05-hasil-analisis.md](05-hasil-analisis.md) — Hasil & Analisis (mengacu pada [../06-output/](../06-output/))
- [06-kesimpulan.md](06-kesimpulan.md) — Kesimpulan & Saran Penelitian Lanjutan
- [07-daftar-pustaka.md](07-daftar-pustaka.md) — Daftar Pustaka (18 referensi, format IEEE; BibTeX di [../02-literatur/daftar-pustaka.bib](../02-literatur/daftar-pustaka.bib))

> `naskah-jurnal.md`/`.docx` adalah gabungan final dari bagian-bagian di atas. Pemindahan ke template jurnal tujuan (margin, sitasi, kolom spesifik) dilakukan oleh peneliti.

## Acuan

[../09-docs/tahap-5-draf-paper.md](../09-docs/tahap-5-draf-paper.md)
