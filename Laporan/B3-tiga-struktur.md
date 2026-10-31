# B3. Tiga Struktur Arsitektur

**Penanggung jawab: Rendi Pratama**

## 1. Tujuan dan dasar rancangan

Bagian ini menggambarkan usulan arsitektur untuk subsistem *Laboratory Management*, khususnya layanan peminjaman ruang laboratorium di Fakultas Ilmu Komputer Universitas Muslim Indonesia (FIKOM UMI). Pembahasan menggunakan tiga kategori struktur: struktur modul, struktur komponen dan konektor (*component-and-connector*/C&C), serta struktur alokasi. Struktur modul menunjukkan unit perangkat lunak dan ketergantungannya; C&C menunjukkan komponen runtime dan komunikasinya; struktur alokasi menunjukkan hubungan perangkat lunak dengan lingkungan operasional [1, §2.2].

Rancangan ini **selesai sebagai usulan konseptual untuk B3**, tetapi bukan keputusan arsitektur yang telah disahkan atau diimplementasikan. A1, A5, dan B5 belum tersedia di repo. Karena itu, nama komponen, alur, kanal pemberitahuan, dan penempatan infrastruktur di bawah ini perlu diperlakukan sebagai rancangan usulan yang dapat diputuskan atau disesuaikan di A5/B5.

Rancangan diturunkan dari kebutuhan yang sudah dicatat:

- **ASR-1:** mencegah jadwal ganda dan memberi tahu pihak terdampak paling lama lima menit setelah perubahan disahkan; nol jadwal ganda pada 30 pengajuan bersamaan adalah target usulan.
- **ASR-2:** admin dapat mengubah konfigurasi laboratorium dan alur persetujuan tanpa perubahan kode; penerapan paling lama satu jam kerja adalah target usulan.
- **ASR-3:** penggunaan dan perubahan status dicatat, jejak perubahan dipertahankan, dan akses dibatasi menurut kewenangan.
- **ASR-4:** target ketersediaan layanan minimal 99% dari jam kerja per bulan.
- **Batasan A3:** fokus layanan adalah peminjaman ruang laboratorium; data jadwal menjadi acuan; pengguna mengakses layanan melalui jaringan; dan kewenangan operasional dibedakan berdasarkan peran.

Semua angka di atas merupakan **target usulan dalam A4, B2, dan B4**, bukan hasil implementasi atau pengukuran.

## 2. Struktur modul

Struktur modul membagi tanggung jawab perangkat lunak dan menunjukkan ketergantungan antarmodul. Komponen di bawah adalah unit logis untuk analisis, bukan nama paket atau layanan yang sudah dibuat dalam kode.

| Modul | Tanggung jawab | Kebutuhan yang didukung |
|---|---|---|
| Antarmuka pengguna | Menampilkan jadwal, ketersediaan, status, dan riwayat; menerima permohonan; menyediakan fungsi bagi admin/petugas. | Kasus penggunaan BAB I; kebutuhan stakeholder A2 |
| Layanan aplikasi | Mengatur alur permohonan, pemeriksaan kewenangan, persetujuan, pencatatan, dan respons ke antarmuka. | Pemisahan alur dan validasi lintas fungsi |
| Identitas dan hak akses | Mengenali pengguna serta memeriksa kewenangan sebelum operasi dijalankan. | ASR-3; A3-O1 |
| Pengajuan peminjaman | Memvalidasi kelengkapan permohonan dan meneruskan permohonan untuk diproses. | Kasus penggunaan BAB I; B2 A3 |
| Jadwal dan ketersediaan | Membaca jadwal, memeriksa bentrokan, dan menjaga konsistensi penetapan ruang dan waktu. | ASR-1; A3-T2 dan A3-B3 |
| Alur persetujuan dan konfigurasi | Mengelola tahapan dan pihak yang menyetujui, jenis keperluan, serta konfigurasi ruang sebagai data. | ASR-2; A3-B2 |
| Pencatatan penggunaan dan audit | Mencatat peminjam, tujuan, waktu mulai/selesai, kondisi ruang, dan jejak perubahan. | ASR-3; A3-O2 dan A3-O3 |
| Notifikasi | Meneruskan pemberitahuan perubahan yang telah disahkan dan mencatat status pengirimannya. | ASR-1 |
| Akses data | Menyimpan dan mengambil data pengguna, ruang, jadwal, permohonan, persetujuan, penggunaan, konfigurasi, dan audit. | ASR-1, ASR-2, ASR-3, ASR-4 |

Ketergantungan yang diusulkan: antarmuka menggunakan layanan aplikasi; layanan aplikasi menggunakan modul identitas, pengajuan, jadwal, persetujuan, pencatatan, dan notifikasi; modul-modul tersebut menggunakan akses data. Pemeriksaan kewenangan dan bentrokan jadwal dilakukan pada layanan terkait, bukan hanya di antarmuka, supaya semua jalur permintaan tunduk pada aturan yang sama.

```mermaid
flowchart LR
  UI[Antarmuka pengguna] --> APP[Layanan aplikasi]
  APP --> ID[Identitas dan hak akses]
  APP --> REQ[Pengajuan peminjaman]
  APP --> SCH[Jadwal dan ketersediaan]
  APP --> APR[Alur persetujuan dan konfigurasi]
  APP --> AUDIT[Pencatatan penggunaan dan audit]
  APP --> NOTIF[Notifikasi]
  ID --> DATA[Akses data]
  REQ --> DATA
  SCH --> DATA
  APR --> DATA
  AUDIT --> DATA
  NOTIF --> DATA
```

**Gambar B3-1.** Struktur modul konseptual. Panah menunjukkan ketergantungan antarmodul, bukan urutan pesan saat runtime.

## 3. Struktur komponen dan konektor saat runtime

Struktur C&C menggambarkan komponen yang berinteraksi ketika layanan digunakan. Usulan ini memakai pola klien–server: pengguna mengakses klien web, layanan aplikasi memeriksa dan mengatur proses, sedangkan penyimpanan jadwal menjadi acuan bersama. Protokol HTTPS dan transaksi ditunjukkan sebagai kebutuhan komunikasi konseptual; teknologi dan mekanisme rinci belum dipilih. Akses persisten melalui modul/komponen akses data pada Gambar B3-1 dan B3-2, bukan melalui ketergantungan langsung setiap layanan pada basis data.

```mermaid
flowchart LR
  U[Mahasiswa / Dosen / Petugas] -->|permintaan HTTPS| WEB[Klien web]
  WEB -->|respons HTTPS| U
  WEB -->|permintaan layanan| API[Layanan aplikasi]
  API -->|periksa identitas dan kewenangan| AUTH[Layanan identitas dan hak akses]
  AUTH -->|hasil pemeriksaan| API
  API -->|permohonan| REQ[Layanan pengajuan]
  REQ --> SCHED[Layanan jadwal]
  API -->|keputusan persetujuan| APPROVE[Layanan persetujuan dan konfigurasi]
  APPROVE -->|keputusan yang disahkan| SCHED
  SCHED -->|cek bentrokan dan simpan melalui| REPO[Layanan akses data]
  REPO -->|baca/tulis| DB[(Basis data terpusat)]
  APPROVE -->|baca/tulis konfigurasi dan keputusan melalui| REPO
  API -->|catatan kegiatan| AUDIT[Layanan pencatatan dan audit]
  AUDIT -->|tulis jejak audit melalui| REPO
  SCHED -->|perubahan jadwal| AUDIT
  APPROVE -->|keputusan persetujuan| AUDIT
  SCHED -->|perubahan yang sudah disahkan| QUEUE[Antrean pemberitahuan]
  QUEUE --> NOTIFY[Layanan notifikasi]
  NOTIFY -->|status pengiriman melalui| REPO
  NOTIFY -->|kirim melalui kanal yang dipilih| CHANNEL[Gerbang kanal pemberitahuan]
  CHANNEL -->|pemberitahuan kepada pihak terdampak| U
```

**Gambar B3-2.** Komponen dan konektor runtime yang diusulkan. Gerbang kanal pemberitahuan adalah placeholder; A2–A4 belum menetapkan apakah pemberitahuan dikirim melalui email, SMS, atau kanal lain.

Alur penting yang ditunjukkan:

1. Pengguna meminta informasi jadwal atau mengirim permohonan melalui klien web.
2. Layanan aplikasi memeriksa identitas dan kewenangan. Permohonan diteruskan ke layanan jadwal untuk memeriksa bentrokan sebelum jadwal ditetapkan.
3. Pihak berwenang menyetujui/menolak permohonan atau mengesahkan perubahan. Keputusan dan penggunaan ruang dicatat agar dapat ditelusuri.
4. Setelah perubahan jadwal disahkan dan disimpan, peristiwa perubahan diteruskan melalui antrean ke layanan notifikasi, lalu dikirim ke pihak terdampak melalui kanal yang nantinya dipilih.

Pemeriksaan dan penyimpanan jadwal harus menangani permohonan bersamaan agar tidak menghasilkan jadwal ganda. Mekanisme spesifik—misalnya batasan transaksi atau penguncian data—belum ditetapkan dan harus diputuskan di A5 serta diuji sesuai B2. Antrean memisahkan pengiriman notifikasi dari transaksi utama, tetapi perlu pemantauan dan percobaan ulang; detail jaminan pesan tidak hilang juga harus diputuskan sebelum implementasi.

## 4. Struktur alokasi

Struktur alokasi menghubungkan komponen perangkat lunak dengan perangkat dan lingkungan operasionalnya. Diagram ini menunjukkan **penempatan konseptual**, bukan spesifikasi hosting yang sudah dipilih. Jenis host, penyedia, kanal notifikasi, dan mekanisme cadangan masih terbuka.

```mermaid
flowchart TB
  subgraph CLIENT[Perangkat pengguna]
    BROWSER[Peramban web]
  end
  subgraph APPHOST[Host aplikasi - lingkungan belum ditetapkan]
    WEBAPP[Komponen klien web]
    API[Layanan aplikasi]
    REPO[Layanan akses data]
    QUEUE[Antrean pemberitahuan]
    WORKER[Layanan/pemroses notifikasi]
  end
  subgraph DATAHOST[Host/layanan penyimpanan - belum ditetapkan]
    DB[(Basis data terpusat)]
    BACKUP[Salinan cadangan]
  end
  GATEWAY[Gerbang kanal pemberitahuan - pilihan belum ditetapkan]
  USER[Mahasiswa / Dosen / Petugas]
  BROWSER -->|jaringan kampus atau internet, HTTPS| WEBAPP
  WEBAPP -->|HTTPS| API
  API --> REPO
  REPO -->|koneksi layanan| DB
  API -->|peristiwa perubahan| QUEUE
  QUEUE --> WORKER
  WORKER -->|koneksi ke kanal| GATEWAY
  GATEWAY -->|pemberitahuan| USER
  DB -.->|cadangan berkala; kebijakan belum ditetapkan| BACKUP
```

**Gambar B3-3.** Alokasi konseptual klien, layanan aplikasi, pemroses notifikasi, penyimpanan, cadangan, dan gerbang pemberitahuan.

Basis data terpusat dimaksudkan menjadi acuan jadwal. Pemisahan antrean/pemroses notifikasi memberi ruang untuk menangani pengiriman tanpa menahan respons permohonan. Akan tetapi, satu host aplikasi dan satu basis data pada gambar tidak menjamin target ASR-4 sebesar 99%. Redundansi, pemulihan gangguan, keamanan jaringan, retensi cadangan, dan tanggung jawab operasional perlu dipilih dan diuji sebelum target ketersediaan dapat dinilai.

## 5. Keterkaitan struktur dengan atribut kualitas

| Atribut/kebutuhan | Elemen rancangan yang mendukung | Hal yang perlu diputuskan atau dibuktikan |
|---|---|---|
| Konsistensi jadwal (ASR-1) | Pemeriksaan bentrokan pada layanan jadwal dan penyimpanan bersama. | Pilih mekanisme transaksi untuk permohonan bersamaan; uji 30 pengajuan dan pastikan tidak ada jadwal ganda. |
| Pemberitahuan perubahan (ASR-1) | Antrean dan layanan notifikasi yang terpisah dari proses persetujuan. | Pilih kanal, mekanisme pemulihan/pengiriman ulang, dan ukur batas lima menit serta tingkat keberhasilan pada B2. |
| Perubahan aturan (ASR-2) | Modul alur persetujuan dan konfigurasi memisahkan aturan dari kode alur utama. | Buktikan admin dapat mengubah aturan tanpa perubahan kode dan aturan baru berlaku sesuai target B2. |
| Keamanan dan auditabilitas (ASR-3) | Pemeriksaan kewenangan di layanan dan modul jejak audit. | Uji akses per peran, kelengkapan catatan, dan pencegahan perubahan tanpa jejak. |
| Ketersediaan (ASR-4) | Alokasi layanan dan data terpusat; kebutuhan cadangan ditampilkan. | Tetapkan strategi redundansi/pemulihan dan ukur waktu aktif terhadap jam kerja. |
| Kinerja (B1) | Layanan aplikasi dan akses data menjadi jalur utama permintaan. | B1 memilih kinerja sebagai pendorong, tetapi A4/B2 belum menetapkan target waktu respons; tentukan ukuran dan uji sebelum menyatakan rancangan memenuhi kinerja. |

## 6. Trade-off rancangan awal

- **Pemisahan modul** membantu memisahkan aturan persetujuan, pemeriksaan jadwal, audit, dan notifikasi. Dampaknya, batas tanggung jawab serta kontrak antarmodul perlu didefinisikan dengan jelas.
- **Layanan aplikasi terpusat** memberi satu jalur validasi dan menyederhanakan konsistensi jadwal. Dampaknya, kapasitas serta ketersediaan host aplikasi dan basis data menjadi penting.
- **Antrean pemberitahuan** memungkinkan pengiriman berjalan terpisah dari transaksi permohonan. Dampaknya, sistem perlu memantau antrean, mencoba ulang pesan gagal, dan mencegah atau menangani pesan ganda.
- **Basis data terpusat** menyediakan acuan jadwal bersama. Dampaknya, ketersediaan dan pemulihan basis data perlu dirancang untuk memenuhi ASR-4.

Trade-off ini adalah masukan untuk B5, bukan keputusan final. A5 perlu menetapkan pilihan dan alasannya berdasarkan ASR, batasan, biaya, dan kemampuan operasional yang tersedia.

## 7. Referensi

[1] P. C. Clements, *Comparing the SEI’s Views and Beyond Approach for Documenting Software Architectures with ANSI-IEEE 1471-2000*, CMU/SEI-2005-TN-017, Software Engineering Institute, Carnegie Mellon University, 2005, §2.2. [PDF resmi SEI](https://www.sei.cmu.edu/documents/2072/2005_004_001_14498.pdf).
