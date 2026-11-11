# Lampiran 1. Architecture Decision Records

ADR-001 dan ADR-002 berasal dari Tugas Kelompok 1 (`Laporan/A5-keputusan-arsitektur.md`). ADR-003 dan ADR-004 adalah ADR baru pada UTS (subbab 5.5).

## ADR-001: Gaya Arsitektur

| Bagian | Isi |
|---|---|
| **Title** | Menggunakan *modular monolith* dengan pendekatan *client-server* berbasis REST API. |
| **Status** | Diterima (Oktober 2026), dilanjutkan pada UTS sebagai gaya Client-Server dengan pola Layered (BAB III). |
| **Context** | Sistem memerlukan pemisahan antarmuka dan logika peminjaman, dengan skala internal kampus. |
| **Decision** | Satu aplikasi yang dibagi menjadi modul/lapisan, diakses melalui REST API. |
| **Consequences** | Skalabilitas dilakukan untuk aplikasi secara keseluruhan, bukan per modul. |

## ADR-002: Basis Data

| Bagian | Isi |
|---|---|
| **Title** | Menggunakan basis data relasional (RDBMS). |
| **Status** | Diterima (Oktober 2026). |
| **Context** | Isu paling kritis adalah mencegah dua peminjaman pada slot yang sama. |
| **Decision** | Memakai RDBMS yang mendukung transaksi ACID dan penguncian baris. |
| **Consequences** | Skema harus dinormalisasi dengan relasi ketat antara ruangan, slot jadwal, dan permohonan. Menjadi dasar ADR-003. |

## ADR-003: Penyimpanan Slot melalui Repository dengan Penguncian per Slot

| Bagian | Isi |
|---|---|
| **Title** | Pemeriksaan dan penyimpanan slot hanya melalui `JadwalRepository.simpanJikaKosong` dengan *pessimistic locking* per slot. |
| **Status** | Diterima (November 2026) |
| **Context** | Informasi ketersediaan (masalah utama) hanya berguna jika benar, dan Asisten Laboratorium (R2) menyebut jadwal bertabrakan sebagai kendala. ASR-2 menuntut hanya 1 dari 100 pengajuan serentak yang diterima. Taktik 2 memerlukan satu tempat penguncian, dan pola Repository menyediakan satu pintu akses data. *Optimistic locking* ditolak karena menghasilkan 99 kegagalan dan pengulangan. |
| **Decision** | Layanan Peminjaman menyimpan peminjaman hanya melalui `simpanJikaKosong`, yang mengunci baris slot dengan `SELECT … FOR UPDATE`, memeriksa ketersediaan, lalu *commit* atau *rollback* (Gambar 4.4). Batasan unik (ruang, tanggal, jam mulai) menjadi pengaman kedua. |
| **Consequences** | (+) Jadwal ganda dicegah di tingkat basis data dan mudah diuji. (−) Permintaan pada slot yang sama antre saat puncak (R1, TP1). (−) Terikat pada satu basis data. |

## ADR-004: Status Permohonan dengan Pola State dan Polling 30 Detik

| Bagian | Isi |
|---|---|
| **Title** | Status permohonan dikelola pola State di Layanan Status dan dibaca Antarmuka Mahasiswa dengan polling 30 detik, bukan WebSocket. |
| **Status** | Diterima (November 2026) |
| **Context** | R1 ingin mengetahui keputusan permohonannya (Bukti 3), dan ASR-3 menuntut status terlihat ≤ 1 menit. Taktik 3 membutuhkan status yang konsisten, dan pola State menjamin hanya permohonan Menunggu yang dapat diputuskan. WebSocket lebih cepat, tetapi kalah pada perbandingan berbobot (subbab 5.2) karena butuh koneksi terbuka per pengguna. |
| **Decision** | Status hanya berubah melalui `Permohonan.setujui()` dan `tolak()` yang diteruskan ke kelas status (Gambar 4.3). Antarmuka Mahasiswa memanggil Controller / API setiap 30 detik. |
| **Consequences** | (+) Sederhana dan memenuhi ASR-3 dengan selisih aman. (+) Label status selalu seragam. (−) Tambahan ±10 permintaan/detik pada 300 pengguna. (−) Status tidak *real-time*; interval polling adalah SP1. |
