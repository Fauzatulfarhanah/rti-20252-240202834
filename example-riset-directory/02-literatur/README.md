# 02-literatur

Kumpulan referensi & paper terkait untuk mendukung Tinjauan Pustaka (Tahap 5).

## Topik Referensi yang Relevan
* **Keamanan JWT/JWKS:** Fokus pada kelas kerentanan JWKS Endpoint Flooding (terkait mitigasi serangan yang mengeksploitasi pengambilan kunci publik secara berulang).
* **Strategi Caching Multi-layer:** Implementasi Redis sebagai L1 (untuk akses instan) dan PostgreSQL sebagai L2/Source of Truth (untuk konsistensi data).
* **Negative Caching:** Teknik mitigasi untuk menangani flooding/cache-busting dengan menyimpan status "data tidak ditemukan" atau "permintaan tidak valid" dalam waktu singkat.
* **Rate Limiting:** Penerapan pada API Gateway atau microservices untuk membatasi volume permintaan per klien guna mencegah *resource exhaustion*.
* **Metodologi Load Testing dengan k6:** Prosedur pengujian kinerja sistem di bawah tekanan trafik tinggi untuk memvalidasi efektivitas skema mitigasi.

## Isi yang Diharapkan
Berikut adalah ringkasan dari 18 literatur utama yang telah dikumpulkan:
1. **Strategi Pertahanan JWKS:** Literatur menekankan pentingnya validasi token di tingkat gateway dan penggunaan cache untuk menyimpan kunci publik (JWKS) guna menghindari beban berlebih pada Identity Provider (IdP).
2. **Optimasi Caching (Redis & PostgreSQL):** Penelitian (misal: Lin et al., 2016) menunjukkan bahwa arsitektur hibrida memori bersama dan meta-table dapat meningkatkan kecepatan kueri hingga puluhan kali lipat, yang krusial dalam menangkis serangan flooding.
3. **Mekanisme Rate Limiting:** Penggunaan algoritma *dynamic token-bucket* yang diintegrasikan dengan Redis dan Zookeeper terbukti efektif dalam menjaga latensi tetap rendah sekaligus memberikan ketahanan terhadap serangan DDoS (Zenodo, 2024).
4. **Validasi Kinerja dengan k6:** Metodologi pengujian beban menggunakan k6 digunakan untuk mensimulasikan pola trafik agresif, mengukur titik jenuh sistem, dan memastikan *threshold rate limiting* sudah dikonfigurasi dengan tepat.

## Berkas
* `matriks-literatur.md` — Matriks literatur lengkap yang memetakan 7 topik ke 18 referensi terverifikasi, termasuk analisis kontribusi terhadap mitigasi flooding.
* `daftar-pustaka.bib` — Bibliografi format BibTeX yang berisi 18 entri lengkap, siap diimpor ke aplikasi manajemen referensi seperti Mendeley atau Zotero.