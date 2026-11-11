# BAB II SKENARIO
- **Nama:** Muh Ammar Samkhan
- **Stambuk (NIM):** 13020240112
- **Bagian Tugas:** U1 – Konteks dan ASR
---

## 2.1 Identifikasi Kebutuhan Kualitas Sistem

Kualitas sistem merupakan aspek penting dalam perancangan arsitektur karena menentukan kemampuan sistem dalam memenuhi kebutuhan pengguna. Pada Layanan Peminjaman Ruang Laboratorium FIKOM UMI, terdapat tiga kualitas utama yang menjadi prioritas, yaitu kinerja (*performance*), keandalan (*reliability*), dan kemudahan penggunaan (*usability*).

Ketiga kualitas tersebut dipilih karena masalah utama pada layanan ini adalah mahasiswa belum dapat mengetahui ketersediaan laboratorium secara mandiri dan masih bergantung pada laboran, serta adanya risiko jadwal penggunaan yang bertabrakan. Setiap kualitas dipetakan ke satu kebutuhan ASR pada BAB I.

## 2.2 Perancangan Quality Attribute Scenarios

*Quality Attribute Scenario* digunakan untuk menggambarkan respons sistem terhadap kondisi tertentu secara terukur [1]. Berikut tiga skenario yang dirancang, masing-masing untuk satu karakteristik pendorong.

### A. Skenario 1 – Kinerja Pengecekan Ketersediaan Ruangan (ASR-1)

| Komponen | Deskripsi |
|---|---|
| Source | Mahasiswa FIKOM |
| Stimulus | 300 mahasiswa membuka halaman ketersediaan laboratorium di waktu yang sama |
| Environment | Sistem beroperasi normal pada jam sibuk, misalnya awal semester |
| Artifact | Layanan Ketersediaan dan Basis Data Jadwal |
| Response | Sistem menampilkan daftar ruangan yang kosong dan yang sedang digunakan beserta jadwalnya |
| Response Measure | Hasil tampil dalam 2 detik |

Skenario ini menjawab masalah utama secara langsung: mahasiswa dapat melihat ketersediaan ruangan sendiri tanpa bertanya kepada laboran.

### B. Skenario 2 – Keandalan Jadwal Peminjaman (ASR-2)

| Komponen | Deskripsi |
|---|---|
| Source | Mahasiswa FIKOM |
| Stimulus | 100 mahasiswa mengajukan peminjaman untuk ruangan dan jam yang sama pada waktu yang bersamaan |
| Environment | Sistem beroperasi normal, ruangan masih kosong pada jam yang diminta |
| Artifact | Layanan Peminjaman dan Basis Data Jadwal |
| Response | Sistem hanya meloloskan satu permohonan, sedangkan permohonan lain ditolak dengan pemberitahuan bahwa ruangan sudah terisi |
| Response Measure | Hanya 1 orang yang mendapat ruangan, 99 lainnya diberi tahu bahwa ruangan sudah terisi, dan jadwal bentrok berjumlah 0 |

Skenario ini menjawab risiko jadwal bertabrakan yang disampaikan asisten laboratorium.

### C. Skenario 3 – Kemudahan Mengetahui Status Permohonan (ASR-3)

| Komponen | Deskripsi |
|---|---|
| Source | Laboran (memberi keputusan) dan mahasiswa (melihat status) |
| Stimulus | Laboran menyetujui atau menolak permohonan peminjaman |
| Environment | Sistem beroperasi normal |
| Artifact | Layanan Status dan antarmuka mahasiswa |
| Response | Sistem memperbarui status permohonan (menunggu, diterima, atau ditolak) dan menampilkannya kepada mahasiswa tanpa mahasiswa menghubungi laboran |
| Response Measure | Status baru terlihat oleh mahasiswa dalam 1 menit |

Skenario ini menjawab status keputusan yang selama ini disampaikan langsung atau melalui pesan.

## 2.3 Pengukuran dan Target Kualitas Sistem

Berdasarkan skenario yang telah dibuat, target kualitas sistem dirangkum sebagai berikut:

| Kualitas | Target yang Diusulkan | Cara Pengukuran |
|---|---|---|
| Performance | Saat 300 mahasiswa mengakses bersamaan, halaman ketersediaan tampil dalam 2 detik | Uji beban dengan 300 pengguna simulasi, lalu ukur waktu respons halaman ketersediaan (minimal 95% permintaan memenuhi target) |
| Reliability | Dari 100 permintaan pada ruangan dan jam yang sama, hanya 1 diterima dan 0 jadwal bentrok | Uji permintaan bersamaan pada satu slot, lalu periksa jumlah peminjaman yang tersimpan di Basis Data Jadwal |
| Usability | Status permohonan terlihat dalam 1 menit setelah keputusan laboran | Ukur selisih waktu antara keputusan laboran dan status tampil di halaman mahasiswa |
