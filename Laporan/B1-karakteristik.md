# B1. Identifikasi dan Klasifikasi Karakteristik

**Penanggung Jawab: Muh. Fahmi Ashar**

## 1. Identifikasi Kandidat Karakteristik

Karakteristik arsitektur merupakan ciri atau kebutuhan penting yang memengaruhi rancangan, pengembangan, dan pengoperasian sistem. Pada sistem peminjaman ruang laboratorium, karakteristik digunakan untuk memastikan proses pengecekan ketersediaan ruangan, pengajuan peminjaman, verifikasi, persetujuan, dan pencatatan penggunaan berjalan dengan baik.

Kategori karakteristik yang digunakan:

- **Operasional:** berkaitan dengan perilaku sistem ketika digunakan.
- **Struktural:** berkaitan dengan susunan komponen dan hubungan antarkomponen.
- **Lintas sektor:** berkaitan dengan kebutuhan yang memengaruhi berbagai bagian atau fungsi organisasi.

Sifat karakteristik dibedakan menjadi:

- **Eksplisit:** dinyatakan secara langsung dalam kebutuhan atau kebijakan sistem.
- **Implisit:** tidak dinyatakan secara langsung, tetapi dapat disimpulkan dari kebutuhan organisasi.

| No. | Karakteristik | Kategori | Sifat | Alasan |
|---|---|---|---|---|
| 1 | Kinerja (Performance) | Operasional | Eksplisit | Sistem harus mampu menampilkan informasi ketersediaan ruangan dan memproses pengajuan peminjaman dalam waktu yang dapat diterima. |
| 2 | Keamanan (Security) | Lintas sektor | Eksplisit | Sistem harus melindungi data pengguna dan membatasi akses berdasarkan peran, seperti mahasiswa, dosen, asisten laboratorium, dan admin. |
| 3 | Ketersediaan (Availability) | Operasional | Eksplisit | Sistem diharapkan dapat diakses ketika pengguna membutuhkan informasi ruangan atau ingin mengajukan peminjaman. |
| 4 | Kemudahan Penggunaan (Usability) | Operasional | Eksplisit | Antarmuka harus mudah dipahami agar pengguna dapat melakukan pengajuan dan memeriksa status peminjaman dengan mudah. |
| 5 | Keandalan (Reliability) | Operasional | Implisit | Sistem harus beroperasi secara konsisten dan menyimpan data peminjaman dengan benar agar tidak terjadi kehilangan informasi. |
| 6 | Integritas Data (Data Integrity) | Lintas sektor | Eksplisit | Data jadwal dan peminjaman harus akurat serta mencegah terjadinya pemesanan ruangan pada waktu yang sama. |
| 7 | Kemudahan Pemeliharaan (Maintainability) | Struktural | Implisit | Sistem perlu dirancang agar mudah diperbaiki dan dikembangkan ketika terdapat perubahan kebutuhan laboratorium. |
| 8 | Skalabilitas (Scalability) | Struktural | Implisit | Sistem perlu mampu menyesuaikan diri apabila jumlah pengguna, ruangan, dan transaksi peminjaman bertambah. |
| 9 | Auditabilitas (Auditability) | Lintas sektor | Eksplisit | Riwayat pengajuan, persetujuan, dan penggunaan ruangan perlu disimpan agar dapat diperiksa kembali oleh pihak pengelola. |
| 10 | Interoperabilitas (Interoperability) | Struktural | Implisit | Sistem berpotensi dikembangkan agar dapat terhubung dengan layanan akademik atau sistem informasi kampus lainnya. |

## 2. Tiga Ciri Karakteristik Arsitektur sebagai Alat Uji

Karakteristik arsitektur diuji menggunakan tiga ciri berikut:

1. **Dampak terhadap keputusan arsitektur:** karakteristik memengaruhi pemilihan teknologi, pola arsitektur, atau komponen sistem.
2. **Dapat diuji atau diukur:** karakteristik dapat dinilai menggunakan indikator atau kriteria penerimaan.
3. **Dampak lintas komponen:** karakteristik memengaruhi beberapa bagian sistem atau keputusan jangka panjang.

| No. | Karakteristik | Dampak pada Arsitektur | Dapat Diuji | Dampak Lintas Komponen |
|---|---|---|---|---|
| 1 | Kinerja | Ya | Ya, melalui pengukuran waktu respons sistem. | Ya |
| 2 | Keamanan | Ya | Ya, melalui pengujian hak akses dan autentikasi. | Ya |
| 3 | Ketersediaan | Ya | Ya, melalui pengukuran waktu aktif sistem. | Ya |
| 4 | Kemudahan Penggunaan | Ya | Ya, melalui pengujian langsung oleh pengguna. | Dapat bervariasi |
| 5 | Keandalan | Ya | Ya, melalui pengujian penyimpanan dan pemulihan data. | Ya |
| 6 | Integritas Data | Ya | Ya, melalui pengujian validasi dan bentrok jadwal. | Ya |
| 7 | Kemudahan Pemeliharaan | Ya | Ya, melalui pengujian perubahan dan perbaikan sistem. | Ya |
| 8 | Skalabilitas | Ya | Ya, melalui pengujian peningkatan jumlah pengguna. | Ya |
| 9 | Auditabilitas | Ya | Ya, melalui pemeriksaan riwayat aktivitas peminjaman. | Ya |
| 10 | Interoperabilitas | Ya | Ya, melalui pengujian pertukaran data antarsistem. | Ya |

## 3. Pemilihan Tiga Karakteristik Pendorong

Berdasarkan kebutuhan sistem peminjaman ruang laboratorium, terdapat tiga karakteristik utama yang menjadi pendorong keputusan arsitektur, yaitu keamanan, kinerja, dan integritas data.

### 3.1 Keamanan (Security)

Keamanan dipilih karena sistem menyimpan data pengguna dan informasi peminjaman ruangan yang hanya boleh diakses oleh pihak sesuai kewenangannya.

- **Alasan:** sistem memiliki beberapa jenis pengguna dengan hak akses yang berbeda. Data pengajuan dan persetujuan peminjaman harus terlindungi dari akses yang tidak sah.
- **Pengaruh terhadap arsitektur:** menentukan penerapan autentikasi, otorisasi berdasarkan peran pengguna, serta perlindungan data.
- **Cara pengujian:** melakukan pengujian login, hak akses setiap pengguna, dan pembatasan akses terhadap fitur tertentu.

### 3.2 Kinerja (Performance)

Kinerja dipilih karena sistem harus memberikan respons yang baik ketika pengguna memeriksa ketersediaan ruangan, mengajukan peminjaman, dan melihat status permohonan.

- **Alasan:** proses pencarian jadwal dan pengajuan yang lambat dapat menghambat aktivitas mahasiswa, dosen, maupun pengelola laboratorium.
- **Pengaruh terhadap arsitektur:** memengaruhi pemilihan teknologi, pengelolaan basis data, dan proses pengambilan informasi jadwal peminjaman.
- **Cara pengujian:** mengukur waktu respons ketika pengguna membuka informasi ruangan, memeriksa jadwal, dan mengirim pengajuan peminjaman.

### 3.3 Integritas Data (Data Integrity)

Integritas data dipilih karena informasi jadwal dan transaksi peminjaman harus selalu akurat dan konsisten.

- **Alasan:** kesalahan penyimpanan atau perubahan data dapat menyebabkan jadwal peminjaman bertabrakan dan ruangan digunakan oleh lebih dari satu pihak pada waktu yang sama.
- **Pengaruh terhadap arsitektur:** memengaruhi rancangan basis data, validasi jadwal, pengelolaan transaksi, dan aturan penyimpanan data peminjaman.
- **Cara pengujian:** melakukan pengujian pengajuan pada ruangan dan waktu yang sama, validasi data peminjaman, serta pemeriksaan konsistensi riwayat transaksi.
