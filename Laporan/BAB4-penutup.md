# BAB IV. Penutup

**Penanggung jawab: Rendi Pratama**

## 4.1 Kesimpulan

Pembahasan ini berfokus pada subsistem *Laboratory Management*, khususnya layanan peminjaman ruang laboratorium di Fakultas Ilmu Komputer Universitas Muslim Indonesia (FIKOM UMI). Layanan yang dibahas mencakup pemeriksaan ketersediaan ruang, pengajuan peminjaman, verifikasi dan persetujuan, pencatatan penggunaan, serta penelusuran riwayat. Kebutuhan dan peran pengguna yang dihimpun menjadi dasar untuk mengenali kebutuhan mahasiswa, dosen, asisten laboratorium, admin laboratorium, dan kepala laboratorium atau pihak yang berwenang.

Analisis batasan dan kebutuhan arsitektural menunjukkan bahwa rancangan perlu mencegah jadwal ganda, mengelola perubahan aturan persetujuan, menjaga pencatatan penggunaan dan jejak perubahan, membatasi akses menurut peran, serta menjaga agar layanan dapat diakses. B2 menetapkan sasaran usulan seperti nol jadwal ganda pada 30 pengajuan bersamaan, pemberitahuan perubahan dalam lima menit, pencatatan sesi yang lengkap, perubahan aturan paling lama satu jam kerja, dan ketersediaan 99% pada jam kerja. Sasaran tersebut merupakan kriteria yang diusulkan untuk pengujian, bukan hasil yang sudah dibuktikan.

B3 menyajikan rancangan konseptual melalui struktur modul, struktur komponen dan konektor, serta struktur alokasi. Ketiga struktur menghubungkan kebutuhan kualitas dengan pembagian tanggung jawab, interaksi layanan saat berjalan, dan lingkungan penempatan yang mungkin. A5 kini mencatat pilihan awal berupa *modular monolith*, REST API, dan RDBMS; B5 membahas prioritas konsistensi data atas kinerja murni serta keamanan atas kemudahan penggunaan. Rincian implementasi dan bukti pengujian tetap belum tersedia, sehingga rancangan B3 belum dapat dianggap sebagai sistem yang telah terbukti.

Prioritas kualitas dalam dokumen juga perlu diselaraskan. B1 memilih keamanan, kinerja, dan integritas data sebagai tiga karakteristik pendorong. Sementara itu, ukuran pada B2 dan pemetaan B4 berfokus pada keamanan, keandalan/integritas data, serta kemudahan pemeliharaan; B4 menyebut efisiensi kinerja bukan prioritas. B5 memilih konsistensi data di atas kinerja murni, tetapi belum memberikan target kinerja yang dapat diukur. Maka, prioritas akhir dan keterkaitan antara karakteristik, ASR, ukuran, keputusan, dan struktur arsitektur belum konsisten sepenuhnya.

## 4.2 Saran

1. Selaraskan prioritas karakteristik kualitas pada B1, B2, dan B4. Tetapkan apakah kinerja merupakan prioritas; jika iya, rumuskan ASR, target ukur, skenario uji, dan pemetaan ISO/IEC 25010 yang sesuai.
2. Lengkapi rincian A1, A5, dan B5. Pastikan konteks SIAKAD/SSO serta gateway notifikasi di A1 selaras dengan rancangan B3, dokumentasikan alasan dan konsekuensi keputusan A5 secara lebih lengkap, dan lengkapi analisis trade-off B5 agar keputusan arsitektur dapat ditelusuri.
3. Gunakan hasil wawancara sebagai dasar validasi kebutuhan dan batasan operasional. Konfirmasikan asumsi yang masih tercatat pada A3 kepada pengelola laboratorium dan dokumentasikan perubahan atau persetujuannya.
4. Setelah sistem atau prototipe tersedia, jalankan skenario pengujian B2. Laporkan hasil aktual secara terpisah dari target usulan, termasuk konfigurasi, jumlah pengulangan, dan bukti pengukuran.
5. Samakan ruang lingkup dan status pekerjaan pada README dengan isi laporan terbaru. Lengkapi lampiran pembagian tugas dan susun PDF laporan akhir setelah semua bagian kelompok selesai.

## 4.3 Batasan Kesimpulan

Kesimpulan ini didasarkan pada berkas yang tersedia di repositori saat penyusunan BAB IV. A1, A5, B5, dan daftar pustaka telah tersedia, tetapi rincian keputusan dan pembuktian melalui implementasi/pengujian masih perlu dilengkapi; PDF laporan akhir juga belum tersedia. B3 merupakan rancangan konseptual, sedangkan angka pada B2 merupakan target pengujian yang diusulkan. Dengan demikian, dokumen ini menyimpulkan kebutuhan dan arah rancangan awal, bukan keberhasilan pengujian sistem.
