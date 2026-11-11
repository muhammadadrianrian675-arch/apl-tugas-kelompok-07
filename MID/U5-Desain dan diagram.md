# BAB V DESAIN DAN DIAGRAM

**Nama:** Muhammad Adrian  
**NIM:** 13020240262  
**Bagian:** U5 – Desain dan Diagram  

Bab ini menyajikan desain layanan dalam empat diagram: diagram konteks, diagram arsitektur yang menerapkan pola pada BAB IV, serta dua diagram UML (diagram kelas dan diagram sequence). Setiap diagram dilengkapi keterangan, kemudian dijelaskan tiga prinsip desain yang diterapkan.

---

## 5.1 Diagram Konteks

Diagram konteks menunjukkan layanan sebagai satu kesatuan beserta pihak luar yang berinteraksi dengannya. Pihak luar diambil dari stakeholder pada BAB I (subbab 1.3).

![Gambar 5.1 Diagram Konteks Layanan Peminjaman Ruang Laboratorium FIKOM UMI](gambar-5.1.png)  
*Gambar 5.1 Diagram Konteks Layanan Peminjaman Ruang Laboratorium FIKOM UMI*

> **Keterangan:** Persegi panjang adalah entitas luar, elips adalah layanan, dan anak panah adalah aliran data beserta arahnya.

| Entitas | Data masuk ke layanan | Data keluar dari layanan |
| :--- | :--- | :--- |
| **Mahasiswa** | Permintaan cek ketersediaan dan pengajuan peminjaman | Informasi ketersediaan, status permohonan, dan aturan penggunaan |
| **Laboran** | Keputusan permohonan (setujui atau tolak) | Daftar permohonan masuk |
| **Asisten Laboratorium** | Permintaan melihat jadwal | Jadwal pemakaian ruangan |
| **Kepala Laboratorium** | Jadwal pengguna dan kebijakan penggunaan | Rekap jadwal dan pemakaian |

---

## 5.2 Diagram Arsitektur

Diagram arsitektur menunjukkan struktur internal layanan yang menerapkan tiga pola pada BAB IV: Layered pada pembagian lapisan, Repository pada lapisan akses data, dan State pada Layanan Status.

![Gambar 5.2 Diagram Arsitektur Layanan dengan Pola Layered, Repository, dan State](gambar-5.2.png)  
*Gambar 5.2 Diagram Arsitektur Layanan dengan Pola Layered, Repository, dan State*

| Elemen | Pola/Taktik | Fungsi |
| :--- | :--- | :--- |
| **Antarmuka Mahasiswa** | Taktik 3 | Menampilkan ketersediaan, menerima pengajuan, dan memeriksa status setiap 30 detik (polling) |
| **Antarmuka Laboran dan Kepala Laboratorium** | – | Laboran memutuskan permohonan; Kepala Laboratorium mengatur jadwal dan kebijakan |
| **Controller / API** | Layered (presentasi) | Menerima permintaan HTTP, memvalidasi, lalu meneruskan ke layanan |
| **Layanan Ketersediaan** | Layered; Taktik 1 | Menyusun daftar ruangan kosong dan terpakai beserta jadwalnya (ASR-1) |
| **Layanan Peminjaman** | Layered; Taktik 2 | Memproses pengajuan dengan transaksi dan penguncian agar tidak ada jadwal bentrok (ASR-2) |
| **Layanan Status** | State; Taktik 3 | Mengelola status menunggu, diterima, dan ditolak, lalu menyediakannya bagi mahasiswa (ASR-3) |
| **JadwalRepository dan PermohonanRepository** | Repository | Satu-satunya jalur akses data jadwal dan permohonan |
| **Basis Data Jadwal** | Taktik 1 | Menyimpan data ruangan, jadwal, dan permohonan dengan indeks pada tanggal dan jam |

---

## 5.3 Diagram UML – Diagram Kelas

Diagram kelas menggambarkan kelas utama layanan beserta hubungannya. Kelas berwarna biru adalah layanan, jingga adalah repository, dan kuning adalah kelas pola State.

![Gambar 5.3 Diagram Kelas Layanan Peminjaman Ruang Laboratorium](gambar-5.3.png)  
*Gambar 5.3 Diagram Kelas Layanan Peminjaman Ruang Laboratorium*

**Keterangan:**
* Anak panah putus-putus dengan kepala terbuka menunjukkan ketergantungan: layanan menggunakan repository melalui antarmukanya.
* Anak panah putus-putus dengan segitiga kosong menunjukkan realisasi: `JadwalRepositoryDB` dan `PermohonanRepositoryDB` mengimplementasikan antarmuka repository, sedangkan `StatusMenunggu`, `StatusDiterima`, dan `StatusDitolak` mengimplementasikan `StatusPermohonan`.
* Satu `Ruangan` memiliki banyak `SlotJadwal` (1 ke banyak). Setiap `Permohonan` menempati tepat satu `SlotJadwal` dan memiliki tepat satu status aktif.
* Permohonan yang ditolak melepas `SlotJadwal`-nya sehingga ruangan dapat dipinjam pengguna lain. Aturan ini merupakan asumsi desain tim.
* `Layanan Peminjaman` mengelola banyak `Permohonan` (1 ke banyak).

---

## 5.4 Diagram UML – Diagram Sequence Pengajuan Peminjaman

Diagram sequence menunjukkan urutan interaksi saat mahasiswa mengajukan peminjaman dan memperlihatkan bagaimana Taktik 2 bekerja untuk Skenario 2.

![Gambar 5.4 Diagram Sequence Pengajuan Peminjaman Ruangan](gambar-5.4.png)  
*Gambar 5.4 Diagram Sequence Pengajuan Peminjaman Ruangan*

> **Keterangan:** Garis tegas adalah pemanggilan, garis putus-putus adalah balasan, dan kotak alt menunjukkan dua kemungkinan alur.

1. **Langkah 1–3:** Permintaan mahasiswa diteruskan dari antarmuka ke `Layanan Peminjaman`, lalu ke `JadwalRepository`.
2. **Langkah 4:** Repository memulai transaksi, mengunci slot, dan memeriksa ketersediaannya. Penguncian membuat permintaan lain pada slot yang sama harus menunggu.
3. **Alur slot masih kosong (5–8):** Permohonan disimpan dengan status Menunggu, transaksi di-*commit*, dan mahasiswa melihat statusnya.
4. **Alur slot sudah terisi (5'–8'):** Transaksi di-*rollback* dan mahasiswa menerima pemberitahuan bahwa ruangan sudah terisi. Dari 100 permintaan bersamaan, satu mengikuti alur pertama dan 99 mengikuti alur kedua, sesuai ASR-2.

---

## 5.5 Prinsip Desain yang Diterapkan

Tiga prinsip desain berikut diterapkan pada layanan ini.

| Prinsip | Penerapan pada layanan | Manfaat |
| :--- | :--- | :--- |
| **Separation of Concerns** *(pemisahan tanggung jawab)* | Tampilan, aturan peminjaman, akses data, dan penyimpanan dipisah ke dalam empat lapisan (Gambar 5.2) | Perubahan tampilan tidak memengaruhi logika anti-bentrok; tiap lapisan dapat diuji sendiri |
| **Single Responsibility** *(satu kelas satu tanggung jawab)* | `LayananKetersediaan` hanya menyajikan ketersediaan; `LayananPeminjaman` hanya mengelola siklus peminjaman; `LayananStatus` hanya menyajikan status; setiap kelas status hanya mengatur satu status (Gambar 5.3) | Kelas kecil dan mudah dipahami; perubahan satu fitur tidak merusak fitur lain |
| **Dependency Inversion** *(bergantung pada abstraksi)* | Layanan bergantung pada antarmuka `JadwalRepository` dan `PermohonanRepository`, bukan pada kelas yang memakai SQL (Gambar 5.3) | Layanan dapat diuji tanpa basis data nyata dan basis data dapat diganti tanpa mengubah layanan |

---

## 5.6 Ringkasan Desain

| ASR | Taktik (BAB III) | Pola (BAB IV) | Diagram yang menunjukkan |
| :--- | :--- | :--- | :--- |
| **ASR-1** | Database Indexing dan Query Optimization | Layered, Repository | Gambar 5.2 (Layanan Ketersediaan, JadwalRepository, Basis Data Jadwal) dan Gambar 5.3 |
| **ASR-2** | Transaction Management dan Concurrency Control | Layered, Repository | Gambar 5.4 (transaksi, penguncian, commit/rollback) dan Gambar 5.3 |
| **ASR-3** | Automatic Status Update dan Periodic Polling | Layered, State | Gambar 5.2 (polling 30 detik, Layanan Status) dan Gambar 5.3 (kelas State) |
