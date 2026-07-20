# Tahap 2 — Implementasi Skrip Otomasi & Pipeline Inferensi Eksperimen

**Status:** Selesai
**Acuan arsitektur:** [tahap-1-perancangan-lingkungan-eksperimen.md](tahap-1-perancangan-lingkungan-eksperimen.md)
**Lokasi kode:** [../05-kode/skrip-eksperimen/](../05-kode/skrip-eksperimen/)

---

## Tujuan

Mengimplementasikan skrip otomasi pengujian (Python + Darknet Engine) yang mendukung dua kondisi pengujian model melalui variabel `MODE_PENGUJIAN`:

- `YOLOv2` — baseline, mengeksekusi inferensi gambar menggunakan arsitektur dangkal Darknet-19 (29.475 BFLOPS).
- `YOLOv3` — intervensi, mengeksekusi inferensi gambar menggunakan arsitektur dalam Darknet-53 dengan koneksi residual dan deteksi multi-skala (65.879 BFLOPS).

## Deliverable

- [x] Struktur skrip otomasi Python (`main_experiment.py`, `core/...`) — terbagi per modul fungsional eksperimen (`darknet_handler`, `metrics_extractor`, `drive_sync`, `visualizer`)
- [x] Skrip otomasi kompilasi `Makefile` Darknet yang otomatis mengonfigurasi arsitektur grafis sesuai spesifikasi runtime (`GPU=1`, `CUDNN=1`, `OPENCV=1`)
- [x] Manajemen dataset via skrip Python untuk otomatisasi pembacaan folder `/dataset/train/` dan folder `/dataset/test/`
- [x] Skrip inisialisasi (`scripts/init_weights.py`): memverifikasi integritas berkas bobot `.weights` dan berkas arsitektur `.cfg` di Google Drive sebelum eksperimen dimulai
- [x] Handler pembungkus (*wrapper*) perintah eksternal Darknet (`!./darknet detector test`) dengan parameter ketat `-thresh 0.30 -dont_show` yang mengimplementasikan aturan *fail-closed* dan *fail-open*
- [x] Modul Parser Log Terintegrasi (`utils/metrics_extractor.py`) untuk mengekstrak data waktu komputasi (*inference time* dalam milidetik) dan tingkat kepercayaan (*confidence score*) dari luaran tekstual konsol Darknet
- [x] Berkas konfigurasi variabel eksperimen (`config.json` atau berkas variabel lingkungan `.env`) untuk menentukan parameter *threshold* dan batas *epoch* pelatihan
- [x] Fungsi validasi visualisasi output menggunakan pustaka OpenCV (`cv2.imread`) dan patch lokal Google Colab (`cv2_imshow`) untuk memvalidasi berkas `predictions.jpg`
- [x] `README.md` dengan instruksi perintah mentah (perintah *mounting* Google Drive, kompilasi Darknet, eksekusi pengujian otomatis, dan saklar penggantian `MODE_PENGUJIAN`)

## Hasil Verifikasi End-to-End

Diverifikasi secara langsung di dalam *environment* Google Colab dengan akselerasi GPU Tesla T4 (hasil pengujian dapat dilihat pada catatan log runtime):

- **Mode YOLOv3 (Intervensi)**: Memproses 4 citra karakteristik uji kunci. Gambar yang memiliki tantangan oklusi tinggi dan objek bertumpuk (`amigos.jpg` dan `@jaoyng on instagram.jpg`) berhasil mendeteksi objek manusia dengan *confidence score* stabil; data koordinat spasial diperbarui ke penyimpanan; *inference time* per citra tercatat lebih lama akibat komputasi dalam 106 *layer*.
- **Mode YOLOv2 (Baseline)**: Memproses 4 citra uji kunci yang sama. Seluruh proses pengujian berjalan dengan *inference time* yang sangat cepat karena beban komputasi rendah (29.475 BFLOPS); namun, terjadi kegagalan deteksi (*missed detection*) pada manusia yang teroklusi sebagian di pojok lift; metrik akurasi tercatat lebih rendah.
- **Fail-closed**: Saat dilakukan simulasi dengan merusak indeks berkas citra uji atau sengaja menghapus file `yolov3_training_last.weights` dari Google Drive $\rightarrow$ skrip Python langsung melempar eksepsi *fatal error* `FileNotFoundError / Runtime Error` dan menghentikan seluruh antrean pengujian demi menjaga validitas nilai metrik *Precision* dan *Recall*.
- **Fail-open (Reconnection)**: Saat koneksi runtime Google Colab terputus di tengah jalan $\rightarrow$ skrip mampu mengenali posisi indeks pengujian terakhir yang tersimpan di folder `backup/` Google Drive, memulihkan status pengujian, dan melanjutkan komputasi tanpa mengulang dari iterasi pertama.

## Catatan Lingkungan Eksperimen

- Alokasi akselerasi perangkat keras pada Google Colab harus dipastikan berada pada tipe **GPU Tesla T4** sebelum skrip dijalankan. Jika runtime dialokasikan ke CPU standar, skrip akan mengeluarkan peringatan performa dan menghentikan proses eksekusi otomatis karena *inference time* akan melambung tinggi.
- Dikarenakan beberapa file citra uji dalam dataset memiliki spasi pada penamaannya (misalnya `leonel lara.jpg` dan `@jaoyng on instagram.jpg`), skrip otomasi Python diimplementasikan menggunakan pembungkus tanda kutip ganda eksplisit atau fungsi `shlex.quote()` saat mengirimkan argumen ke shell Darknet. Hal ini dilakukan untuk mencegah kesalahan pembacaan *path* file oleh sistem operasi Linux di lingkungan Colab.