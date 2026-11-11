# Tugas Kelompok 7 – Arsitektur Perangkat Lunak (2 KKA 512)

Repositori Kelompok 07 Bagian III. Berisi **Tugas Proyek UTS** (folder `uts/`) dan Tugas Kelompok 1 (folder `Laporan/`).

| Keterangan | Isi |
|---|---|
| Kelompok | Bagian III – Kelompok 07 |
| Subsistem | Layanan Pendukung Kampus |
| Layanan inti | Peminjaman Ruang Laboratorium FIKOM UMI |
| Perwakilan kelompok | Muhammad Adrian, 13020240262 |

## Anggota

| No | Stambuk | Nama | Akun GitHub | UTS | Tugas Kelompok 1 |
|---|---|---|---|---|---|
| 1 | 13020240184 | Rendi Pratama | @RenDY-16 | U6, U7, Penutup, Pustaka, Lampiran, Sampul, Daftar Isi, PDF akhir | BAB I, B3, BAB IV |
| 2 | 13020240333 | Muh. Fahmi Ashar | @Fhmii-png | U3 | A2, A3, B1 |
| 3 | 13020240112 | Muh. Ammar Samkhan | @Ammar1234567-gif | U1, U2 | A4, B2, B4 |
| 4 | 13020240262 | Muhammad Adrian | @muhammadadnanrian675-arch | U4, U5 | A1, A5, B5, Pustaka |

## Tugas Proyek UTS – Perancangan Arsitektur Layanan Smart Campus UMI

Batas pengumpulan: **Kamis, 12 November 2026, pukul 07.00 WITA**.

### Peta berkas dan penanggung jawab

Status: Belum / Draf / Selesai. Perbarui tabel ini setiap ada perubahan.

| Kode | Bab | Berkas | Penanggung jawab | Status |
|---|---|---|---|---|
| U1 | BAB I Pendahuluan | uts/U1-Konteks-dan-ASR.md | Muh. Ammar Samkhan | Draf |
| U2 | BAB II Skenario | uts/U2-Skenario-Atribut-Kualitas.md | Muh. Ammar Samkhan | Draf |
| U3 | BAB III Taktik dan Pola | uts/U3-Taktik.md | Muh. Fahmi Ashar | Draf |
| U4 | BAB III Taktik dan Pola | uts/U4-Pola.md | Muhammad Adrian | Draf |
| U5 | BAB IV Desain | uts/U5-Desain dan diagram.md | Muhammad Adrian | Draf |
| U6 | BAB V Evaluasi dan ADR | uts/U6-Evaluasi.md | Rendi Pratama | Selesai |
| U7 | BAB V Evaluasi dan ADR | uts/U7-ADR.md | Rendi Pratama | Selesai |
| – | BAB VI Penutup | uts/BAB6-Penutup.md | Rendi Pratama | Draf |
| – | Daftar pustaka (IEEE, 6 referensi) | uts/daftar-pustaka.md | Rendi Pratama | Draf |
| – | Lampiran 1: ADR-001 s.d. ADR-004 | lampiran/L1-ADR.md | Rendi Pratama | Draf |
| – | Lampiran 2: Pembagian tugas dan bukti kontribusi | lampiran/L2-pembagian-tugas.md | Rendi Pratama | Draf |
| – | Sampul dan daftar isi | uts/UTS_III_Kelompok07.pdf | Rendi Pratama | Draf |
| – | PDF akhir dan berkas tautan LMS | uts/UTS_III_Kelompok07.pdf, uts/UTS_III_Kelompok07.txt | Rendi Pratama | Draf (menunggu gambar U5) |

### Yang masih harus diselesaikan

1. Gambar U5 (`gambar-5.1.png` s.d. `gambar-5.4.png`) di-commit ke `uts/` agar diagram tampil.
2. Penomoran bab mengikuti soal: U3–U4 = BAB III (3.x), U5 = BAB IV (4.x, Gambar 4.x), U6–U7 = BAB V.
3. Sitasi [5] Gamma dkk. (State) dan [6] Fowler (Repository) ditambahkan di U4.
4. Sebutan R2 diseragamkan menjadi "Asisten Laboratorium (R2)" di U2 dan U3.
5. Akun commit pada Lampiran 2 dikonfirmasi oleh tiap anggota.
6. Foto bukti wawancara U1 disimpan sebagai file di repo (misalnya `bukti-data/`) agar dapat dimasukkan ke PDF.

### Laporan PDF akhir

`uts/UTS_III_Kelompok07.pdf` (maksimal 12 halaman isi). Tautan dikirim ke LMS Kalam UMI dalam berkas `UTS_III_Kelompok07.txt`.

## Tugas Kelompok 1 (selesai)

| Kode | Berkas | Penanggung jawab | Status |
|---|---|---|---|
| BAB I | Laporan/BAB1-pendahuluan.md | Rendi Pratama | Selesai |
| A1 | Laporan/A1-konteks-arsitektur.md | Muhammad Adrian | Selesai |
| A2 | Laporan/A2-Stakeholder.md | Muh. Fahmi Ashar | Selesai |
| A3 | Laporan/A3-batasan.md | Muh. Fahmi Ashar | Selesai |
| A4 | Laporan/A4-asr.md | Muh. Ammar Samkhan | Selesai |
| A5 | Laporan/A5-keputusan-arsitektur.md dan adr/ | Muhammad Adrian | Selesai |
| B1 | Laporan/B1-karakteristik.md | Muh. Fahmi Ashar | Selesai |
| B2 | Laporan/B2-atribut-terukur.md | Muh. Ammar Samkhan | Selesai |
| B3 | Laporan/B3-tiga-struktur.md dan diagram/ | Rendi Pratama | Selesai |
| B4 | Laporan/B4-iso-25010.md | Muh. Ammar Samkhan | Selesai |
| B5 | Laporan/B5-trade-off.md | Muhammad Adrian | Selesai |
| BAB IV | Laporan/BAB4-penutup.md | Rendi Pratama | Selesai |
| Pustaka | Laporan/daftar-pustaka.md | Muhammad Adrian | Selesai |

Laporan PDF: `hasil/TugasKel1_III_Kelompok07.pdf`

## Aturan kerja singkat

1. Setiap anggota commit dengan akun GitHub sendiri.
2. Kerjakan bagian milik sendiri. Untuk bagian orang lain, sepakati dulu dan beri pesan commit yang jelas.
3. Pesan commit diawali kode bagian, contoh: [U6] tambah analisis ATAM.
4. Jalankan git pull sebelum mulai bekerja. Jangan force push. Jangan gabung commit (squash).
5. Jangan unggah data pribadi orang lain (nama responden, nomor telepon, tangkapan layar berisi identitas). Sebut responden sebagai R1, R2, dan seterusnya.
6. Gambar dan foto bukti disimpan di repo (uts/ atau bukti-data/), bukan hanya diunggah lewat editor web GitHub.
7. Isi lampiran/C-pembagian-tugas.md dengan tautan commit masing-masing.
8. Batas UTS: versi terakhir di repositori pada **12 Nov 2026 pukul 07.00 WITA** yang dinilai.
