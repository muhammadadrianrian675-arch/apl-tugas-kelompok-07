
# BAB III TAKTIK DAN POLA

**Nama:** Muh. Fahmi Ashar  
**NIM:** 13020240333  
**Bagian:** U3 – Taktik dan Pola

## 3.1 Taktik (U3)

Taktik merupakan langkah teknis yang diterapkan untuk mencapai karakteristik kualitas sistem yang telah ditentukan pada BAB II. Pada Layanan Peminjaman Ruang Laboratorium FIKOM UMI, taktik dirancang untuk mendukung kinerja, keandalan, dan kemudahan penggunaan sistem.

Berikut taktik yang diterapkan pada masing-masing skenario.

### A. Taktik 1 – Optimasi Pencarian Ketersediaan Ruangan (Performance)

**Permasalahan:**

Mahasiswa harus bertanya langsung kepada laboran untuk mengetahui ruangan laboratorium yang kosong atau sedang digunakan. Sistem harus mampu menampilkan informasi tersebut dengan cepat, termasuk ketika diakses oleh 300 mahasiswa secara bersamaan.

**Taktik yang digunakan: Database Indexing dan Query Optimization**

**Cara Kerja:**

Sistem menggunakan indeks pada database untuk mempercepat pencarian informasi jadwal laboratorium. Ketika mahasiswa membuka halaman ketersediaan, sistem hanya mengambil data ruangan dan jadwal yang dibutuhkan. Dengan demikian, proses pencarian tidak perlu membaca seluruh data satu per satu.

**Harga yang Dibayar (Trade-off):**

Penggunaan indeks membutuhkan ruang penyimpanan tambahan pada database. Selain itu, proses penambahan dan perubahan data jadwal dapat sedikit lebih lambat karena indeks juga harus diperbarui.

### B. Taktik 2 – Pencegahan Jadwal Peminjaman Bentrok (Reliability)

**Permasalahan:**

Asisten Laboratorium (R2) menyampaikan bahwa salah satu kendala peminjaman adalah jadwal penggunaan laboratorium yang bertabrakan. Oleh karena itu, sistem harus memastikan satu ruangan tidak dapat dipinjam oleh dua pengguna pada waktu yang sama.

**Taktik yang digunakan: Transaction Management dan Concurrency Control**

**Cara Kerja:**

Ketika mahasiswa mengajukan peminjaman, sistem akan memeriksa terlebih dahulu ketersediaan ruangan berdasarkan tanggal dan waktu yang dipilih. Pemeriksaan dan penyimpanan peminjaman dilakukan dalam satu transaksi database. Sistem menggunakan penguncian data (locking) agar permintaan yang masuk secara bersamaan tidak dapat menggunakan slot ruangan yang sama.

Jika slot masih tersedia, sistem menyimpan permohonan. Namun, jika slot sudah digunakan oleh pengguna lain, sistem menolak permohonan dan menampilkan pemberitahuan bahwa ruangan sudah terisi.

**Harga yang Dibayar (Trade-off):**

Penggunaan transaksi dan penguncian data dapat menyebabkan proses peminjaman menjadi sedikit lebih lambat ketika banyak pengguna mengajukan permohonan secara bersamaan. Selain itu, implementasinya lebih kompleks karena harus mengatur proses transaksi dan penguncian database dengan benar.

### C. Taktik 3 – Pembaruan Status Permohonan Secara Otomatis (Usability)

**Permasalahan:**

Mahasiswa menginginkan informasi apakah permohonan peminjaman laboratorium diterima atau ditolak tanpa harus bertanya langsung kepada laboran.

**Taktik yang digunakan: Automatic Status Update dan Periodic Polling**

**Cara Kerja:**

Ketika laboran memberikan keputusan terhadap permohonan peminjaman, sistem secara otomatis memperbarui status permohonan menjadi menunggu, diterima, atau ditolak sesuai kondisi pengajuan. Halaman mahasiswa melakukan pemeriksaan status secara berkala setiap 30 detik. Dengan demikian, mahasiswa dapat mengetahui perubahan status tanpa harus menghubungi laboran secara langsung.

**Harga yang Dibayar (Trade-off):**

Pemeriksaan status secara berkala menghasilkan permintaan tambahan ke server dan database. Hal ini dapat meningkatkan penggunaan sumber daya server, terutama ketika banyak mahasiswa membuka halaman status secara bersamaan.

## 3.2 Ringkasan Penerapan Taktik

| Skenario | Karakteristik | Taktik | Target |
|---|---|---|---|
| Skenario 1 | Performance | Database Indexing dan Query Optimization | Halaman tampil dalam 2 detik |
| Skenario 2 | Reliability | Transaction Management dan Concurrency Control | 0 jadwal bentrok |
| Skenario 3 | Usability | Automatic Status Update dan Periodic Polling | Status terlihat dalam 1 menit |

Berdasarkan ketiga taktik tersebut, sistem diharapkan mampu meningkatkan kecepatan pencarian ketersediaan laboratorium, mencegah terjadinya jadwal peminjaman yang bertabrakan, serta memudahkan mahasiswa dalam mengetahui status permohonan peminjaman secara mandiri.
