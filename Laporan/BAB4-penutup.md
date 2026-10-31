# BAB IV. Penutup

**Penanggung jawab: Rendi Pratama**

## 4.1 Kesimpulan

Pembahasan ini berfokus pada subsistem *Laboratory Management*, khususnya layanan peminjaman ruang laboratorium di Fakultas Ilmu Komputer Universitas Muslim Indonesia (FIKOM UMI). Layanan yang dibahas mencakup pemeriksaan ketersediaan ruang, pengajuan peminjaman, verifikasi dan persetujuan, pencatatan penggunaan, serta penelusuran riwayat. Kebutuhan dan peran pengguna yang dihimpun menjadi dasar untuk mengenali kebutuhan mahasiswa, dosen, asisten laboratorium, admin laboratorium, dan kepala laboratorium atau pihak yang berwenang.

Analisis batasan dan kebutuhan arsitektural menunjukkan bahwa rancangan perlu mencegah jadwal ganda, mengelola perubahan aturan persetujuan, menjaga pencatatan penggunaan dan jejak perubahan, membatasi akses menurut peran, serta menjaga agar layanan dapat diakses. B2 mencantumkan sasaran usulan seperti nol jadwal ganda pada 30 pengajuan bersamaan, pemberitahuan perubahan dalam lima menit, pencatatan sesi yang lengkap, dan perubahan aturan paling lama satu jam kerja. A4 menetapkan target usulan ketersediaan minimal 99% dari jam kerja dalam sebulan, yang juga dipetakan pada B4. Sasaran tersebut merupakan kriteria yang diusulkan untuk pengujian, bukan hasil yang sudah dibuktikan.

B3 menyajikan rancangan konseptual melalui struktur modul, struktur komponen dan konektor, serta struktur alokasi. Ketiga struktur menghubungkan kebutuhan kualitas dengan pembagian tanggung jawab, interaksi layanan saat berjalan, dan lingkungan penempatan yang mungkin. A5 mencatat pilihan awal berupa *modular monolith*, REST API, dan RDBMS; B5 membahas prioritas konsistensi data atas kinerja murni serta keamanan atas kemudahan penggunaan. Rincian implementasi dan bukti pengujian tetap belum tersedia, sehingga rancangan B3 belum dapat dianggap sebagai sistem yang telah terbukti.

Keamanan, integritas data, kinerja, dan kemudahan pemeliharaan menjadi pertimbangan dalam rancangan. Konsistensi jadwal diprioritaskan saat terjadi pengajuan bersamaan; dampaknya terhadap waktu respons perlu diukur melalui pengujian.

Cakupan integrasi mencakup usulan penggunaan SIAKAD/SSO untuk mahasiswa dan dosen. Rincian integrasi dan mekanisme autentikasi petugas masih perlu ditetapkan.

## 4.2 Saran

1. Tetapkan target waktu respons dan skenario pengukuran kinerja agar dampak pengelolaan transaksi terhadap pengguna dapat dinilai.
2. Tetapkan cakupan integrasi SIAKAD/SSO dan mekanisme autentikasi petugas, serta rinci keputusan dan konsekuensi arsitektur sebelum implementasi.
3. Gunakan hasil wawancara sebagai dasar validasi kebutuhan dan batasan operasional. Konfirmasikan asumsi yang masih tercatat pada A3 kepada pengelola laboratorium dan dokumentasikan perubahan atau persetujuannya.
4. Setelah sistem atau prototipe tersedia, jalankan skenario pengujian B2. Laporkan hasil aktual secara terpisah dari target usulan, termasuk konfigurasi, jumlah pengulangan, dan bukti pengukuran.
5. Susun rencana operasional untuk pemulihan gangguan, pencadangan data, dan pemantauan layanan agar target ketersediaan dapat dievaluasi.

## 4.3 Batasan Kesimpulan

Kesimpulan ini didasarkan pada analisis kebutuhan dan rancangan konseptual layanan. Angka yang dicantumkan merupakan target pengujian yang diusulkan; implementasi dan pengujian diperlukan untuk menilai apakah rancangan dapat memenuhi target tersebut.
