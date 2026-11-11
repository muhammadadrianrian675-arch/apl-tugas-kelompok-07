# BAB VI PENUTUP

## 6.1 Kesimpulan

1. Masalah utama Layanan Peminjaman Ruang Laboratorium FIKOM UMI adalah mahasiswa belum dapat mengetahui ketersediaan laboratorium secara mandiri dan harus bertanya langsung kepada laboran. Masalah ini didukung oleh wawancara mahasiswa (R1) dan asisten laboratorium (R2).
2. Masalah tersebut dijawab oleh tiga karakteristik pendorong, yaitu Performance, Reliability, dan Usability. Ketiganya dirumuskan sebagai skenario terukur: ketersediaan tampil ≤ 2 detik untuk 300 pengguna, hanya 1 dari 100 pengajuan serentak yang diterima, dan status terlihat ≤ 1 menit.
3. Rancangan memakai gaya Client-Server dengan pola Layered, Repository, dan State. Taktik indeks basis data, transaksi dengan penguncian per slot, dan polling 30 detik ditempatkan pada lapisan yang sesuai.
4. Evaluasi berbobot memilih rancangan ini dibanding *microservices* (4,60 vs 3,30). Analisis ATAM menemukan dua risiko utama: antrean penguncian saat puncak pengajuan dan server tunggal sebagai titik kegagalan. Keputusan penting dicatat dalam ADR-003 dan ADR-004.
5. Masalah utama teratasi pada tingkat rancangan, tetapi belum terbukti karena seluruh target masih berupa usulan.

## 6.2 Saran

1. Menguji target secara nyata: uji beban 300 pengguna untuk S1 dan uji 100 pengajuan serentak untuk S2 sebelum layanan digunakan.
2. Menyiapkan cadangan basis data dan pemantauan *uptime* untuk mengurangi risiko server tunggal.
3. Menambahkan komponen pengelolaan aturan penggunaan dan kebijakan Kepala Laboratorium (KF-4 dan KF-5) pada iterasi berikutnya.
4. Menetapkan batas waktu bagi permohonan berstatus Menunggu agar slot yang belum diputuskan tidak tertahan terlalu lama.
