# BAB V EVALUASI DAN ADR

**Nama:** Rendi Pratama  
**NIM:** 13020240184  
**Bagian:** U7 – ADR

## 5.5 Architecture Decision Records

Keputusan arsitektur dicatat dengan format Nygard [4]: Title, Status, Context, Decision, dan Consequences. ADR-001 dan ADR-002 berasal dari Tugas Kelompok 1. Dua ADR baru berikut diturunkan dari taktik (BAB III), pola (BAB IV), dan hasil evaluasi (subbab 5.2–5.3).

### ADR-003: Penyimpanan Slot Melalui Repository dengan Transaksi dan Penguncian per Slot

- **Title:** Pemeriksaan dan penyimpanan slot dilakukan hanya melalui `JadwalRepository.simpanJikaKosong`, dalam satu transaksi dengan *pessimistic locking* per slot.
- **Status:** Diterima (November 2026).
- **Context:** Masalah utama layanan adalah mahasiswa tidak dapat mengetahui ketersediaan laboratorium secara mandiri (BAB I). Informasi ketersediaan hanya berguna jika benar, sedangkan R2 menyebut jadwal bertabrakan sebagai kendala. ASR-2 menuntut hanya 1 dari 100 pengajuan serentak yang mendapat slot. Taktik 2 (*Transaction Management dan Concurrency Control*) memerlukan satu tempat untuk menjalankan penguncian, dan pola Repository (BAB IV) menyediakan satu pintu akses data itu. Pilihan lain adalah *optimistic locking* (memeriksa versi data saat menyimpan, lalu mengulang jika gagal). Pada 100 permintaan untuk satu slot, cara ini menghasilkan 99 kegagalan dan pengulangan.
- **Decision:** Layanan Peminjaman hanya menyimpan peminjaman melalui `JadwalRepository.simpanJikaKosong`. Metode ini membuka transaksi, mengunci baris slot (ruang, tanggal, jam) dengan `SELECT … FOR UPDATE`, memeriksa ketersediaan, lalu menyimpan (*commit*) atau membatalkan (*rollback*). Basis Data Jadwal juga diberi batasan unik pada (ruang, tanggal, jam mulai) sebagai pengaman kedua. Batas tunggu kunci 3 detik (usulan).
- **Consequences:**
  - (+) Jadwal ganda dicegah di tingkat basis data. Tidak ada jalur penyimpanan yang melewati penguncian, karena semua jalur lewat repository.
  - (+) Mudah diuji: hasil uji serentak dapat diperiksa langsung dengan kueri jadwal yang tumpang tindih.
  - (−) Permintaan pada slot yang sama harus antre, sehingga waktu respons naik saat puncak (R1, TP1).
  - (−) Rancangan terikat pada satu basis data. Jika kelak dipecah menjadi *microservices*, mekanisme ini harus dirancang ulang.

### ADR-004: Status Permohonan dengan Pola State dan Polling 30 Detik

- **Title:** Status permohonan dikelola dengan pola State di Layanan Status, dan Antarmuka Mahasiswa membacanya dengan polling setiap 30 detik, bukan WebSocket.
- **Status:** Diterima (November 2026).
- **Context:** R1 ingin mengetahui apakah permohonannya diterima atau ditolak (Bukti 3), dan ASR-3 menuntut status terlihat ≤ 1 menit setelah laboran memutuskan. Taktik 3 (*Automatic Status Update dan Periodic Polling*) membutuhkan status yang selalu konsisten. Pola State (BAB IV) menjamin hanya permohonan berstatus Menunggu yang dapat diputuskan. Pilihan lain adalah WebSocket atau *Server-Sent Events* yang mengirim status seketika, tetapi keduanya membutuhkan koneksi terbuka untuk setiap pengguna dan konfigurasi server tambahan. Pada perbandingan berbobot (subbab 5.2), keunggulan kecepatan itu tidak sebanding dengan kerumitannya.
- **Decision:** Perubahan status hanya melalui `Permohonan.setujui()` dan `Permohonan.tolak()`, yang diteruskan ke kelas `StatusMenunggu`, `StatusDiterima`, atau `StatusDitolak`. Antarmuka Mahasiswa memanggil Controller / API setiap 30 detik untuk membaca label status dari Layanan Status.
- **Consequences:**
  - (+) Sederhana: memakai REST API yang sudah ada dan sesuai gaya Client-Server.
  - (+) Target ASR-3 terpenuhi dengan selisih aman (keterlambatan maksimal ±30 detik dari batas 60 detik).
  - (+) Label status yang dilihat mahasiswa selalu seragam karena berasal dari satu kelas status.
  - (−) Menambah sekitar 10 permintaan/detik pada 300 pengguna aktif, termasuk permintaan yang tidak membawa perubahan.
  - (−) Status tidak *real-time*. Interval polling adalah *sensitivity point* SP1, sehingga setiap perubahan nilainya harus diuji ulang terhadap ASR-3.

## Referensi

[4] M. Nygard, "Documenting Architecture Decisions," Cognitect Blog, Nov. 2011.
