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
| **Title** | Pemeriksaan dan penyimpanan slot hanya melalui `JadwalRepository.simpanJikaKosong`, dalam satu transaksi dengan *pessimistic locking* per slot. |
| **Status** | Diterima (November 2026) |
| **Context** | Masalah utama adalah mahasiswa tidak dapat mengetahui ketersediaan laboratorium secara mandiri (subbab 1.2). Informasi ketersediaan hanya berguna jika benar, padahal Asisten Laboratorium (R2) menyebut jadwal bertabrakan sebagai kendala. ASR-2 menuntut hanya 1 dari 100 pengajuan serentak yang mendapat slot. Taktik 2 (*Transaction Management dan Concurrency Control*) membutuhkan satu tempat untuk menjalankan penguncian, dan pola Repository menyediakan satu pintu akses data tersebut. Alternatif *optimistic locking* (memeriksa versi data saat menyimpan, lalu mengulang jika gagal) akan menghasilkan 99 kegagalan dan pengulangan untuk 100 permintaan pada satu slot. |
| **Decision** | Layanan Peminjaman hanya menyimpan peminjaman melalui `JadwalRepository.simpanJikaKosong`. Metode ini membuka transaksi, mengunci baris slot (ruang, tanggal, jam) dengan `SELECT … FOR UPDATE`, memeriksa ketersediaan, lalu melakukan *commit* atau *rollback* (Gambar 4.4). Basis Data Jadwal juga diberi batasan unik pada (ruang, tanggal, jam mulai) sebagai pengaman kedua. Batas tunggu kunci 3 detik (usulan). |
| **Consequences** | (+) Jadwal ganda dicegah di tingkat basis data, dan tidak ada jalur penyimpanan yang melewati penguncian.<br>(+) Mudah diuji dengan memeriksa jadwal yang tumpang tindih setelah uji serentak.<br>(−) Permintaan pada slot yang sama harus antre, sehingga waktu respons naik saat puncak (R1, TP1).<br>(−) Rancangan terikat pada satu basis data. Jika kelak dipecah menjadi *microservices*, mekanisme ini harus dirancang ulang. |

## ADR-004: Status Permohonan dengan Pola State dan Polling 30 Detik

| Bagian | Isi |
|---|---|
| **Title** | Status permohonan dikelola dengan pola State di Layanan Status, dan Antarmuka Mahasiswa membacanya dengan polling setiap 30 detik, bukan WebSocket. |
| **Status** | Diterima (November 2026) |
| **Context** | R1 ingin mengetahui apakah permohonannya diterima atau ditolak (Bukti 3), dan ASR-3 menuntut status terlihat ≤ 1 menit setelah laboran memutuskan. Taktik 3 (*Automatic Status Update dan Periodic Polling*) membutuhkan status yang selalu konsisten, dan pola State menjamin hanya permohonan berstatus Menunggu yang dapat diputuskan. WebSocket atau *Server-Sent Events* dapat mengirim status seketika, tetapi membutuhkan koneksi terbuka untuk setiap pengguna dan konfigurasi server tambahan. Pada perbandingan berbobot (subbab 5.2), keunggulan itu tidak sebanding dengan kerumitannya. |
| **Decision** | Perubahan status hanya melalui `Permohonan.setujui()` dan `Permohonan.tolak()`, yang diteruskan ke `StatusMenunggu`, `StatusDiterima`, atau `StatusDitolak` (Gambar 4.3). Antarmuka Mahasiswa memanggil Controller / API setiap 30 detik untuk membaca label status dari Layanan Status. |
| **Consequences** | (+) Sederhana: memakai REST API yang sudah ada dan sesuai gaya Client-Server.<br>(+) ASR-3 terpenuhi dengan selisih aman (keterlambatan maksimal ±30 detik dari batas 60 detik).<br>(+) Label status yang dilihat mahasiswa selalu seragam.<br>(−) Menambah sekitar 10 permintaan/detik pada 300 pengguna aktif, termasuk permintaan yang tidak membawa perubahan.<br>(−) Status tidak *real-time*. Interval polling adalah *sensitivity point* SP1, sehingga setiap perubahan nilainya harus diuji ulang terhadap ASR-3. |
