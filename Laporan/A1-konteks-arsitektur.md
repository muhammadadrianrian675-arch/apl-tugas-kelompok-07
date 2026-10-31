# A1. Konteks Arsitektur

Sistem Peminjaman Ruangan dan Laboratorium berinteraksi dengan berbagai aktor pengguna dan sistem eksternal untuk mengelola jadwal, pengajuan, dan persetujuan fasilitas secara terpusat.

## 1. Aktor (Pengguna Sistem)
*   **End User (Mahasiswa & Dosen):** Mengakses sistem untuk melihat jadwal ketersediaan ruangan/laboratorium, melakukan pengajuan peminjaman, dan memantau status persetujuan.
*   **Tim Operasional (Asisten Laboratorium):** Memantau jadwal harian, mencatat waktu penggunaan *real-time*, dan melaporkan kondisi ruangan pasca-penggunaan.
*   **Tim Pengelola (Admin Laboratorium):** Memverifikasi pengajuan, mencegah bentrokan jadwal (*double-booking*), dan mengelola data master ruangan.
*   **Manajer (Kepala Laboratorium/Pengelola Berwenang):** Memantau laporan aktivitas peminjaman dan memberikan persetujuan untuk pengajuan khusus di luar jam operasional standar.

## 2. Sistem Eksternal
*   **Sistem Informasi Akademik (SIAKAD) / SSO Kampus:** Sistem eksternal untuk autentikasi pengguna (Single Sign-On). Digunakan untuk memvalidasi identitas dan status keaktifan Mahasiswa/Dosen secara otomatis.
*   **Layanan Notifikasi (Email / WhatsApp Gateway):** Digunakan untuk mengirimkan pemberitahuan otomatis kepada pemohon terkait perubahan status pengajuan (disetujui/ditolak) dan pengingat jadwal.

## 3. Diagram Konteks
Sistem ini bertindak sebagai pusat layanan yang menerima *request* dari Mahasiswa/Dosen, melakukan validasi identitas ke SIAKAD, meneruskan alur persetujuan ke Admin dan Kepala Laboratorium, lalu mendistribusikan informasi jadwal final kepada Asisten Laboratorium dan mengirimkan notifikasi persetujuan kepada pemohon.
