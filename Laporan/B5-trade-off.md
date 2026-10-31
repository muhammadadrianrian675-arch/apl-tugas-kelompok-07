# B5. Trade-off Arsitektur

Dalam merancang Sistem Peminjaman Ruangan dan Laboratorium, tim memprioritaskan atribut kualitas tertentu berdasarkan ISO 25010, yang menghasilkan beberapa kompromi (*trade-off*):

## 1. Konsistensi Data (Reliability) vs. Kinerja (Performance)
*   **Analisis:** Saat periode sibuk (misalnya awal semester atau masa ujian), banyak mahasiswa atau dosen mungkin mengakses sistem secara bersamaan untuk mem-*booking* ruangan.
*   **Keputusan Trade-off:** Sistem lebih memprioritaskan **Konsistensi Data** dibandingkan **Kinerja murni**. Penggunaan mekanisme transaksi *database* yang ketat (untuk mencegah *double-booking*) mungkin menambah waktu respons (*latency*) sebesar beberapa milidetik. Hal ini dapat diterima karena keandalan jadwal jauh lebih penting daripada kecepatan antarmuka yang instan tetapi menghasilkan jadwal yang tumpang tindih.

## 2. Keamanan (Security) vs. Kemudahan Penggunaan (Usability)
*   **Analisis:** Kepala Laboratorium dan Admin memiliki hak akses destruktif dan berwenang (menyetujui/menolak jadwal).
*   **Keputusan Trade-off:** Untuk peran Admin dan Kepala Lab, sistem menerapkan pembatasan sesi yang ketat (misalnya *auto-logout* setelah beberapa menit tidak aktif) dan validasi otorisasi berlapis. Hal ini sedikit mengurangi kenyamanan (*Usability*) mereka karena harus sering *login*, namun menekan risiko **Keamanan** dari penyalahgunaan akun di komputer fasilitas kampus yang sering digunakan bersama.
