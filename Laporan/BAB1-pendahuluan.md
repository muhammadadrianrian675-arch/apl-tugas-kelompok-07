# BAB I. Pendahuluan

**Penanggung jawab: Rendi Pratama**

## 1.1 Gambaran Layanan Inti

Subsistem yang dibahas dalam tugas ini adalah **Laboratory Management**, khususnya layanan peminjaman ruang laboratorium. Subsistem ini merupakan bagian dari sistem pengelolaan fasilitas akademik yang mendukung proses administrasi peminjaman, penjadwalan, dan penggunaan ruang laboratorium di Fakultas Ilmu Komputer Universitas Muslim Indonesia (FIKOM UMI).

Layanan peminjaman ruang laboratorium bertujuan untuk memudahkan mahasiswa, dosen, dan pihak terkait dalam mengajukan penggunaan ruang laboratorium untuk kegiatan akademik, seperti praktikum, penelitian, diskusi kelompok, pelatihan, maupun kegiatan lainnya yang memperoleh izin.

Layanan inti yang menjadi fokus pembahasan meliputi lima proses utama, yaitu:

1. **Pengecekan ketersediaan ruangan:** layanan untuk melihat informasi ruang laboratorium yang tersedia berdasarkan tanggal dan waktu penggunaan, sehingga peminjam dapat memilih jadwal yang tidak bertabrakan dengan kegiatan lain.

2. **Pengajuan peminjaman ruangan:** layanan yang memungkinkan mahasiswa atau dosen mengajukan permohonan peminjaman dengan mengisi informasi seperti identitas peminjam, tujuan penggunaan, ruangan yang dipilih, tanggal, dan waktu peminjaman.

3. **Verifikasi dan persetujuan peminjaman:** layanan untuk memeriksa kelengkapan pengajuan, kesesuaian jadwal, serta memberikan keputusan persetujuan atau penolakan oleh pihak pengelola laboratorium yang berwenang.

4. **Pencatatan penggunaan ruangan:** layanan untuk mencatat pelaksanaan peminjaman, termasuk waktu mulai dan selesai penggunaan, identitas pengguna, serta kondisi ruangan setelah digunakan.

5. **Pengelolaan riwayat peminjaman:** layanan untuk menyimpan dan menampilkan informasi peminjaman sebelumnya, termasuk status permohonan, durasi penggunaan, dan riwayat penggunaan masing-masing ruang laboratorium.

Pengelolaan layanan secara terintegrasi diharapkan dapat mengurangi risiko bentrokan jadwal, mempermudah proses administrasi, meningkatkan transparansi status peminjaman, serta membantu pengelola laboratorium dalam melakukan pemantauan penggunaan ruangan.

## 1.2 Ruang Lingkup (3–5 Kasus Penggunaan)

Ruang lingkup subsistem Laboratory Management difokuskan pada proses peminjaman dan pengelolaan penggunaan ruang laboratorium di FIKOM UMI.

Pembahasan mencakup lima kasus penggunaan utama berikut.

| Kasus Penggunaan | Aktor | Deskripsi |
|---|---|---|
| Melihat Ketersediaan Ruangan | Mahasiswa / Dosen | Pengguna melihat jadwal dan informasi ketersediaan ruang laboratorium sebelum melakukan peminjaman. |
| Mengajukan Peminjaman Ruangan | Mahasiswa / Dosen | Pengguna mengisi dan mengirimkan formulir peminjaman yang berisi identitas, tujuan, tanggal, waktu, dan ruangan yang ingin digunakan. |
| Memverifikasi dan Menyetujui Peminjaman | Admin Laboratorium / Pengelola Berwenang | Petugas memeriksa permohonan, memastikan jadwal tidak bertabrakan, kemudian menyetujui atau menolak pengajuan. |
| Mencatat Penggunaan Ruangan | Asisten Laboratorium / Admin Laboratorium | Petugas mencatat waktu penggunaan, identitas peminjam, serta status dan kondisi ruangan setelah digunakan. |
| Melihat Riwayat Peminjaman | Mahasiswa / Admin Laboratorium | Pengguna dapat melihat status serta riwayat peminjamannya, sedangkan admin dapat memantau riwayat penggunaan seluruh ruangan. |

Dalam subsistem ini, terdapat beberapa aktor utama, yaitu:

1. **Mahasiswa:** pengguna yang mengajukan peminjaman ruang laboratorium untuk keperluan akademik.

2. **Dosen:** pengguna yang membutuhkan ruang laboratorium untuk kegiatan pembelajaran, penelitian, atau kegiatan akademik lainnya.

3. **Asisten Laboratorium:** pihak yang membantu pengelolaan penggunaan ruangan, pemeriksaan pelaksanaan peminjaman, dan pencatatan aktivitas laboratorium.

4. **Admin Laboratorium:** pihak yang mengelola informasi ruangan, memeriksa permohonan, serta menangani administrasi peminjaman.

5. **Kepala Laboratorium / Pengelola Berwenang:** pihak yang memberikan persetujuan apabila suatu peminjaman membutuhkan otorisasi khusus sesuai ketentuan laboratorium.

Pembahasan dibatasi pada pengelolaan peminjaman ruang laboratorium dan tidak mencakup peminjaman perangkat komputer, alat praktikum, atau inventaris laboratorium secara terpisah.

Prioritas penggunaan ruangan diberikan kepada kegiatan akademik yang telah terjadwal, seperti perkuliahan dan praktikum. Permohonan peminjaman lainnya perlu disesuaikan dengan ketersediaan ruangan dan ketentuan pengelola laboratorium.

## 1.3 Sumber Data

Analisis kebutuhan layanan peminjaman ruang laboratorium menggunakan hasil wawancara yang telah dilakukan dan pengalaman sebagai pengguna yang dicatat dalam A4. Informasi publik serta pengamatan langsung dapat digunakan sebagai sumber pendukung untuk melengkapi dan mengonfirmasi kebutuhan.

### 1. Pengalaman sebagai Pengguna

Pengumpulan data dapat dilakukan dengan mempelajari proses peminjaman ruang laboratorium dari sudut pandang mahasiswa, dosen, atau asisten laboratorium yang pernah terlibat dalam kegiatan penggunaan ruang laboratorium.

Informasi yang dikumpulkan mencakup prosedur pengajuan peminjaman, cara mengetahui ketersediaan ruangan, proses memperoleh izin penggunaan, serta kendala yang mungkin ditemukan.

Aspek yang menjadi fokus pengumpulan informasi meliputi:

1. **Proses pengajuan:** bagaimana pengguna mengajukan permohonan peminjaman ruangan.

2. **Informasi jadwal:** bagaimana pengguna mengetahui ruangan yang tersedia.

3. **Proses persetujuan:** bagaimana permohonan peminjaman diperiksa dan disetujui.

4. **Pelaksanaan penggunaan:** bagaimana pengguna memperoleh akses dan menggunakan ruangan.

5. **Pencatatan peminjaman:** bagaimana riwayat penggunaan ruangan didokumentasikan.

Informasi dari pengalaman pengguna dapat membantu mengidentifikasi kebutuhan sistem yang sesuai dengan kondisi penggunaan laboratorium.

### 2. Informasi Publik

Data pendukung dapat diperoleh dari informasi resmi Universitas Muslim Indonesia melalui situs [umi.ac.id](https://umi.ac.id), informasi Fakultas Ilmu Komputer, pengumuman laboratorium, serta dokumen atau pedoman penggunaan fasilitas akademik yang dapat diakses.

Informasi yang diperlukan meliputi ketentuan penggunaan laboratorium, jadwal kegiatan akademik, prosedur administrasi peminjaman, serta tanggung jawab pengguna selama menggunakan fasilitas laboratorium.

Data tersebut dapat digunakan sebagai referensi untuk memahami aturan dan batasan yang perlu dipertimbangkan dalam perancangan layanan peminjaman ruang laboratorium.

Apabila terdapat prosedur internal yang tidak dipublikasikan, informasi tersebut perlu dikonfirmasi kepada pihak pengelola laboratorium.

### 3. Wawancara

Wawancara telah dilakukan untuk memperoleh informasi mengenai kebutuhan, pengalaman, dan kendala yang berkaitan dengan proses peminjaman ruang laboratorium. Hasilnya menjadi salah satu dasar pembahasan layanan dan kebutuhan dalam laporan ini.

Pihak yang berkaitan dengan layanan dan perannya adalah sebagai berikut.

| Stakeholder | Kelompok | Peran dalam Layanan |
|---|---|---|
| Mahasiswa | Pengguna Akhir | Mengajukan peminjaman dan menggunakan ruangan untuk kegiatan akademik. |
| Dosen | Pengguna Akhir | Mengajukan penggunaan laboratorium untuk pembelajaran, penelitian, atau kegiatan lainnya. |
| Asisten Laboratorium | Petugas Operasional | Membantu pemantauan penggunaan ruangan dan pencatatan aktivitas laboratorium. |
| Admin Laboratorium | Pengelola Sistem | Mengelola jadwal, memverifikasi permohonan, dan mencatat riwayat peminjaman. |
| Kepala Laboratorium | Pengambil Keputusan | Menetapkan kebijakan penggunaan serta memberikan persetujuan apabila diperlukan. |

Pokok pertanyaan yang relevan untuk pengumpulan dan pendalaman informasi meliputi:

1. Bagaimana prosedur peminjaman ruang laboratorium yang berlaku saat ini?

2. Bagaimana mahasiswa atau dosen mengetahui ketersediaan ruang laboratorium?

3. Siapa pihak yang berwenang menyetujui permohonan peminjaman?

4. Apakah pernah terjadi bentrokan jadwal penggunaan ruangan?

5. Bagaimana proses pencatatan identitas peminjam dan durasi penggunaan?

6. Apa kendala yang paling sering muncul dalam proses peminjaman?

7. Apakah diperlukan sistem yang dapat menampilkan ketersediaan ruangan dan status peminjaman secara langsung?

Hasil wawancara menjadi masukan untuk mengidentifikasi kebutuhan fungsional dan kebutuhan nonfungsional sistem. Asumsi yang masih tercatat pada A3 tetap perlu dikonfirmasi kepada pengelola laboratorium.

### 4. Pengamatan Langsung

Pengamatan langsung direncanakan untuk memahami alur penggunaan dan pengelolaan ruang laboratorium di Fakultas Ilmu Komputer Universitas Muslim Indonesia (FIKOM UMI).

Pengamatan difokuskan pada proses pengajuan peminjaman, pengecekan jadwal, pemberian izin, pelaksanaan penggunaan ruangan, dan pencatatan riwayat peminjaman.

Aspek yang diamati meliputi:

1. **Ketersediaan ruangan:** cara pengelola menentukan apakah ruang laboratorium dapat digunakan pada tanggal dan waktu tertentu.

2. **Pengajuan peminjaman:** prosedur yang harus dilakukan mahasiswa atau dosen untuk mengajukan penggunaan ruang laboratorium.

3. **Verifikasi dan persetujuan:** proses pemeriksaan pengajuan serta pihak yang bertanggung jawab memberikan keputusan.

4. **Pelaksanaan peminjaman:** proses penggunaan ruangan sesuai jadwal yang telah disetujui, termasuk pencatatan waktu mulai dan selesai.

5. **Riwayat penggunaan:** cara pengelola mendokumentasikan identitas peminjam, tujuan penggunaan, jadwal, dan kondisi ruangan setelah digunakan.

Melalui pengamatan tersebut, diharapkan dapat diperoleh gambaran mengenai proses bisnis yang berjalan, kendala operasional, dan kebutuhan sistem yang dapat mendukung pengelolaan peminjaman ruang laboratorium secara lebih efektif dan terstruktur.
