# B1. Identifikasi dan Klasifikasi Karakteristik

**Penanggung Jawab:**  Muh. Fahmi Ashar

## 1. Identifikasi Kandidat Karakteristik

Karakteristik arsitektur merupakan ciri atau kebutuhan penting yang memengaruhi rancangan, pengembangan, dan pengoperasian sistem [1]. Pada sistem peminjaman ruang laboratorium FIKOM UMI, karakteristik digunakan untuk memastikan proses pengecekan ketersediaan ruangan, pengajuan peminjaman, verifikasi, persetujuan, dan pencatatan penggunaan berjalan dengan baik.

**Kategori karakteristik yang digunakan:**

- **Operasional:** Berkaitan dengan perilaku sistem ketika digunakan.
- **Struktural:** Berkaitan dengan susunan komponen dan hubungan antarkomponen.
- **Lintas sektor:** Berkaitan dengan kebutuhan yang memengaruhi berbagai bagian atau fungsi organisasi.

**Sifat karakteristik dibedakan menjadi:**

- **Eksplisit:** Dinyatakan secara langsung dalam kebutuhan, batasan (A3), atau ASR (A4).
- **Implisit:** Tidak dinyatakan secara langsung, tetapi dapat disimpulkan dari kebutuhan organisasi.

### Tabel Identifikasi Kandidat Karakteristik

| No. | Karakteristik | Kategori | Sifat | Alasan |
|---|---|---|---|---|
| 1 | Keamanan (Security) | Lintas sektor | Eksplisit | Hak akses berbeda untuk tiap peran (O1), dan riwayat penggunaan harus tercatat serta tidak dapat diubah tanpa jejak (O3, ASR-3). |
| 2 | Keandalan dan Integritas Data (Reliability and Data Integrity) | Operasional | Eksplisit | Bentrok jadwal harus dicegah (B3), dan jadwal pernah berubah mendadak tanpa informasi tepat waktu sehingga data jadwal harus konsisten dan perubahan diberitahukan (ASR-1). |
| 3 | Kemudahan Pemeliharaan (Maintainability) | Struktural | Eksplisit | Penyetuju dan tahapan persetujuan ditetapkan pihak berwenang dan dapat berubah (B2), serta admin mengelola data ruangan (O1). Aturan harus berupa data, bukan kode program (ASR-2). |
| 4 | Ketersediaan (Availability) | Operasional | Eksplisit | Pengecekan ketersediaan dan pengajuan memerlukan jaringan (T3) dan bergantung pada data jadwal (T2). Jika layanan tidak dapat diakses, pencatatan di luar sistem berisiko memicu bentrok (ASR-4). |
| 5 | Auditabilitas (Auditability) | Lintas sektor | Eksplisit | Riwayat pengajuan, persetujuan, dan penggunaan ruangan disimpan sebagai dokumentasi dan bahan evaluasi (O3). Sudah tercakup pada ASR-3. |
| 6 | Kinerja (Performance) | Operasional | Implisit | Pengguna mengharapkan respons yang wajar, tetapi jadwal kuliah dan praktikum di laboratorium sudah teratur sehingga beban bersamaan kecil. Tidak ada ASR kinerja pada A4. |
| 7 | Kemudahan Penggunaan (Usability) | Lintas sektor | Implisit | Pengguna terdiri atas mahasiswa, dosen, asisten, dan admin dengan kemampuan teknis beragam, sehingga antarmuka diharapkan mudah dipahami. |
| 8 | Skalabilitas (Scalability) | Operasional | Implisit | Sistem perlu menyesuaikan diri apabila jumlah ruangan dan transaksi bertambah, tetapi cakupan layanan terbatas pada ruang laboratorium (T1). |
| 9 | Interoperabilitas (Interoperability) | Struktural | Implisit | Sistem berpotensi dikembangkan agar terhubung dengan layanan akademik atau sistem informasi kampus lainnya. |

## 2. Tiga Ciri Karakteristik Arsitektur sebagai Alat Uji

Sebuah karakteristik layak menjadi pendorong arsitektur jika memenuhi ketiga ciri berikut [1]:

1. **Menentukan pertimbangan rancangan di luar domain bisnis:** Karakteristik bukan fungsi bisnis (seperti mengajukan atau menyetujui peminjaman), tetapi syarat bagaimana fungsi tersebut harus dijalankan.
2. **Memengaruhi aspek struktural rancangan:** Karakteristik memengaruhi pemilihan pola arsitektur, pembagian komponen, atau penyimpanan data.
3. **Penting bagi keberhasilan sistem:** Jika karakteristik tidak terpenuhi, layanan gagal mencapai tujuannya.

### Tabel Pengujian Karakteristik

| No. | Karakteristik | (1) Di luar domain bisnis | (2) Memengaruhi struktur | (3) Penting bagi keberhasilan | Hasil |
|---|---|---|---|---|---|
| 1 | Keamanan | Ya | Ya (otentikasi, peran, dan log di semua alur) | Ya | Pendorong |
| 2 | Keandalan dan Integritas Data | Ya | Ya (satu sumber data jadwal dan pemeriksaan bentrok atomik) | Ya | Pendorong |
| 3 | Kemudahan Pemeliharaan | Ya | Ya (modul alur persetujuan terpisah dan aturan sebagai data) | Ya | Pendorong |
| 4 | Ketersediaan | Ya | Sebagian (cukup dengan pemusatan data, cadangan, dan pemantauan) | Ya | Pendukung |
| 5 | Auditabilitas | Ya | Ya | Ya | Digabung ke Keamanan (ASR-3) |
| 6 | Kinerja | Ya | Tidak (beban kecil) | Sedang | Bukan pendorong |
| 7 | Kemudahan Penggunaan | Ya | Tidak (urusan antarmuka) | Ya | Pendukung |
| 8 | Skalabilitas | Ya | Tidak | Rendah | Bukan pendorong |
| 9 | Interoperabilitas | Ya | Sebagian | Rendah | Bukan pendorong |

## 3. Pemilihan Tiga Karakteristik Pendorong

Berdasarkan pengujian di atas dan kesesuaian dengan ASR pada A4, tiga karakteristik pendorong adalah **Keamanan, Keandalan dan Integritas Data, serta Kemudahan Pemeliharaan**.

### 3.1 Keamanan (Security) — ASR-3

Keamanan dipilih karena sistem mencatat penggunaan ruangan dan persetujuan yang menyangkut aset fakultas, serta memiliki beberapa peran dengan hak akses berbeda.

- **Alasan:** Riwayat dipakai sebagai dokumentasi dan bahan evaluasi (O3), sehingga satu catatan yang berubah tanpa jejak sudah merusak tujuannya.
- **Pengaruh terhadap arsitektur:** Menentukan otentikasi, otorisasi berdasarkan peran, dan log yang ada di semua alur sejak awal karena sulit ditambahkan belakangan.
- **Cara pengujian:** Uji hak akses tiap peran, percobaan akses oleh peran tanpa hak, dan pencocokan sampel catatan dengan log audit.

### 3.2 Keandalan dan Integritas Data (Reliability and Data Integrity) — ASR-1

Karakteristik ini dipilih karena kegagalan yang paling merugikan adalah dua kegiatan mendapat laboratorium yang sama pada jam yang sama, atau perubahan jadwal yang tidak sampai ke pihak terdampak.

- **Alasan:** Jadwal praktikum pernah diundur karena laboratorium dipakai kegiatan lain, dan informasinya hanya disampaikan melalui grup chat.
- **Pengaruh terhadap arsitektur:** Menentukan satu sumber data jadwal, pemeriksaan bentrok yang tidak dapat dilewati, aturan prioritas antarkegiatan, dan notifikasi yang terpisah dari alur utama.
- **Cara pengujian:** Uji pengajuan serentak pada ruang dan waktu yang sama, kueri tumpang tindih jadwal, dan pengukuran waktu notifikasi dari log.

### 3.3 Kemudahan Pemeliharaan (Maintainability) — ASR-2

Kemudahan pemeliharaan dipilih karena kebijakan penyetuju dan tahapan persetujuan dapat berubah tanpa melibatkan pengembang.

- **Alasan:** Jika aturan persetujuan ditulis di dalam kode, setiap perubahan kebijakan membutuhkan pengembang.
- **Pengaruh terhadap arsitektur:** Menentukan alur persetujuan sebagai modul terpisah dan aturan yang disimpan sebagai data.
- **Cara pengujian:** Latihan perubahan oleh admin (tambah laboratorium, ganti penyetuju, ubah tahapan) dan pemeriksaan bahwa tidak ada perubahan kode.

### 3.4 Karakteristik yang Tidak Dipilih

Ketersediaan (ASR-4) tetap dipertahankan sebagai kebutuhan pendukung karena targetnya dapat dipenuhi dengan pemusatan data dan pemantauan tanpa struktur khusus.

Kinerja tidak dipilih karena jadwal kuliah dan praktikum sudah teratur sehingga beban bersamaan kecil, dan kegiatan insidental ditangani melalui perubahan jadwal pada ASR-1.

## 4. Referensi

[1] M. Richards and N. Ford, *Fundamentals of Software Architecture: An Engineering Approach*. O'Reilly Media, 2020, Chapter 4.
