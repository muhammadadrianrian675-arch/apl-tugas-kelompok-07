# BAB I PENDAHULUAN

## 1.1 Ringkasan Layanan

**Layanan Peminjaman Ruang Laboratorium Fakultas Ilmu Komputer (FIKOM) UMI** adalah layanan di bawah subsistem **Layanan Pendukung Kampus** (Kelompok III-7) pada Smart Campus UMI. Layanan ini membantu mahasiswa mengetahui aturan penggunaan laboratorium, melihat ketersediaan ruangan, mengajukan peminjaman di luar jadwal praktikum, dan memantau status permohonan. Mahasiswa yang tidak memiliki laptop juga dapat memakai komputer laboratorium untuk tugas kelompok dan proyek kuliah dengan izin pengelola.

Menurut pengelola laboratorium, mahasiswa boleh memakai laboratorium di luar jadwal praktikum selama ruangan tidak dipakai kegiatan lain dan izin sudah diperoleh. Saat ini izin diajukan dengan menemui atau menghubungi laboran secara langsung.

## 1.2 Masalah Utama dan Bukti

Berdasarkan hasil wawancara, masalah utama yang ditemukan adalah:

Informasi ketersediaan laboratorium belum dapat diketahui mahasiswa secara mandiri karena mahasiswa harus bertanya langsung kepada laboran untuk mengetahui ruangan yang kosong atau sedang digunakan.

Masalah tersebut didukung oleh bukti wawancara berikut.

**Bukti 1 – Wawancara Mahasiswa (R1)**

Ketika ditanya apakah mengetahui cara mengecek ruangan laboratorium yang sedang kosong, mahasiswa menjawab:

> Tidak.

<img width="953" height="443" alt="Screenshot 2026-11-10 193019" src="https://github.com/user-attachments/assets/c7f74f63-8e71-4fe8-a0f5-913c77a7fc72" />


*Gambar 1.1 Dokumentasi Bukti 1*

**Bukti 2 – Wawancara Asisten Laboratorium (R2)**

Ketika ditanya bagaimana cara mengetahui laboratorium yang sedang kosong, pengelola menjelaskan:

> Mahasiswa bertanya langsung kepada laboran.

<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/d4e75dc3-116e-4ba3-b286-764a994bf651" />


*Gambar 1.2 Dokumentasi Bukti 2*

**Bukti 3 – Wawancara Mahasiswa (R1)**

Ketika ditanya apakah ingin mengetahui permohonan peminjamannya diterima atau ditolak, mahasiswa menjawab:

> Ya.

<img width="953" height="443" alt="Screenshot 2026-11-10 193019" src="https://github.com/user-attachments/assets/6df0ef58-0762-488e-9f6b-244094333f48" />


*Gambar 1.3 Dokumentasi Bukti 3*

**Bukti tambahan – Wawancara Asisten Laboratorium (R2)**

Pengelola juga menyampaikan bahwa salah satu kendala peminjaman adalah jadwal penggunaan laboratorium yang bertabrakan.

**Kesimpulan masalah utama:**

Mahasiswa belum memiliki akses informasi ketersediaan laboratorium secara langsung. Mereka masih bergantung pada laboran untuk mengetahui ruangan yang kosong. Kondisi ini juga berpotensi menimbulkan benturan jadwal penggunaan laboratorium.

## 1.3 Stakeholder

| No. | Stakeholder | Peran | Kepentingan utama |
|---|---|---|---|
| 1 | Mahasiswa | Mengajukan peminjaman dan memakai fasilitas laboratorium | Mengetahui ketersediaan ruangan dan status permohonan tanpa bertanya langsung |
| 2 | Laboran | Mengelola operasional laboratorium dan memutuskan permohonan | Tidak ada jadwal bentrok dan beban tanya-jawab berkurang |
| 3 | Asisten Laboratorium | Membantu kegiatan laboratorium dan mengawasi pemakaian fasilitas | Mengetahui siapa memakai ruangan dan kapan |
| 4 | Kepala Laboratorium | Bertanggung jawab mengatur jadwal pengguna laboratorium dan menetapkan kebijakan penggunaan | Jadwal pengguna laboratorium tertata, tidak bentrok, dan sesuai kebijakan |

Pembagian tugas: Kepala Laboratorium mengatur jadwal secara keseluruhan dan menetapkan kebijakan, sedangkan Laboran menangani operasional harian dan memutuskan permohonan peminjaman individu.

## 1.4 Kebutuhan Fungsional Layanan

Kebutuhan berikut menjelaskan fungsi layanan. Kebutuhan yang berpengaruh besar pada arsitektur dirumuskan sebagai ASR pada subbab 1.6.

| Kode | Kebutuhan Fungsional |
|---|---|
| KF-1 | Menampilkan ruangan yang kosong atau sedang dipakai beserta jadwalnya |
| KF-2 | Mahasiswa mengajukan peminjaman, laboran memberi keputusan |
| KF-3 | Menampilkan status permohonan (menunggu, diterima, ditolak) |
| KF-4 | Menyediakan aturan dan persyaratan penggunaan laboratorium |
| KF-5 | Kepala Laboratorium mengatur jadwal pengguna dan kebijakan penggunaan laboratorium |

## 1.5 Karakteristik Pendorong

Karakteristik pendorong dipilih dari masalah utama dan kebutuhan stakeholder [1], [2].

| Kode | Karakteristik | Alasan Dipilih |
|---|---|---|
| K1 | **Performance** (kinerja) | Pengecekan ketersediaan harus cepat agar mahasiswa tidak perlu bertanya ke laboran, terutama saat banyak yang mengakses bersamaan. |
| K2 | **Reliability** (keandalan, konsistensi jadwal) | Jadwal dan status harus benar. Dua peminjaman tidak boleh menempati ruangan dan jam yang sama (kendala pada Bukti tambahan). |
| K3 | **Usability** (kemudahan penggunaan) | Mahasiswa harus bisa menemukan ketersediaan dan status dengan mudah, tanpa pelatihan dan tanpa menghubungi laboran. |

## 1.6 Architecturally Significant Requirements (ASR)

ASR adalah kebutuhan kualitas yang paling memengaruhi keputusan arsitektur dan dapat diukur [1]. Setiap ASR punya **ukuran respons**, yaitu target angka yang bisa diuji. Tiap ASR dipetakan ke satu karakteristik pendorong, dan ukuran responsnya menjadi dasar skenario di BAB II.

| Kode | Karakteristik | Kebutuhan | Ukuran Respons |
|---|---|---|---|
| ASR-1 | K1 Performance | Mahasiswa dapat melihat ketersediaan ruangan dengan cepat, walaupun banyak yang membuka bersamaan. | Saat **300 mahasiswa** membuka halaman ketersediaan di waktu yang sama, hasilnya tampil dalam **2 detik**. |
| ASR-2 | K2 Reliability | Satu ruangan pada jam yang sama tidak boleh dipinjam dua orang. | Jika **100 mahasiswa** memesan ruangan dan jam yang sama secara bersamaan, **hanya 1 orang yang mendapat ruangan**, dan 99 lainnya diberi tahu bahwa ruangan sudah terisi. |
| ASR-3 | K3 Usability | Mahasiswa mengetahui status permohonan tanpa bertanya kepada laboran. | Setelah laboran menyetujui atau menolak, mahasiswa melihat statusnya dalam **1 menit**. |
## 1.7 Bagian yang Diperbarui dari Tugas Kelompok 1

| Bagian Tugas Kelompok 1 | Isi sebelumnya | Pembaruan pada UTS |
|---|---|---|
| Identifikasi Masalah | Membahas permasalahan jadwal laboratorium yang dapat berbenturan dengan kegiatan lain serta perubahan jadwal yang informasinya disampaikan melalui grup chat. | Dipersempit menjadi satu masalah utama, yaitu mahasiswa belum bisa mengetahui ketersediaan laboratorium secara mandiri. Masalah diperkuat dengan bukti hasil wawancara mahasiswa dan laboran. |
| Kebutuhan Sistem | Kebutuhan arsitektural mencakup konsistensi jadwal, pengaturan persetujuan, pencatatan penggunaan laboratorium, dan ketersediaan layanan. | Kebutuhan fungsional diperinci menjadi KF-1 sampai KF-5, sedangkan kebutuhan kualitas difokuskan menjadi ASR-1 sampai ASR-3. |
| Stakeholder | Melibatkan Mahasiswa, Dosen, Asisten Laboratorium, Admin Laboratorium, dan Kepala Laboratorium atau pihak pengelola berwenang. | Stakeholder disesuaikan menjadi empat pihak utama, yaitu Mahasiswa, Laboran, Asisten Laboratorium, dan Kepala Laboratorium, serta dilengkapi dengan kepentingan masing-masing. |
| Karakteristik Kualitas | Mencakup Keandalan, Konsistensi Data, Konfigurabilitas, Modifiabilitas, Keamanan, dan Ketersediaan Layanan. | Difokuskan pada tiga karakteristik kualitas utama, yaitu Performance (K1), Reliability (K2), dan Usability (K3), yang kemudian dijabarkan dalam skenario ASR. |

