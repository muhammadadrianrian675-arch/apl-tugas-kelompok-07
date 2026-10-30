## A4. Kebutuhan Signifikan (ASR)

**Penanggung jawab: Muh. Ammar Samkhan**

ASR berikut disusun untuk layanan peminjaman ruang laboratorium di Fakultas Ilmu Komputer Universitas Muslim Indonesia (FIKOM UMI), berdasarkan batasan sistem pada A3 dan pengalaman penulis sebagai pengguna layanan.

| Kode | Kebutuhan (stimulus, kondisi, respons) | Karakteristik | Alasan signifikan secara arsitektural |
| --- | --- | --- | --- |
| ASR-1 | Saat dua pengajuan atau lebih masuk bersamaan untuk lab dan jam yang sama, atau saat ada kegiatan berprioritas lebih tinggi yang memerlukan lab yang sudah terjadwal, sistem hanya menetapkan satu jadwal pada jam tersebut, menandai kegiatan yang terdampak, dan memberi notifikasi kepada pihak terkait paling lama 5 menit setelah perubahan disahkan. Target: tidak ada jadwal ganda pada 30 pengajuan bersamaan (usulan). | Keandalan, konsistensi data | Berdasarkan pengalaman penulis, jadwal praktikum pernah diundur karena lab dipakai untuk tes seleksi kepolisian. Perubahan diumumkan lewat grup chat, biasanya sehari sebelumnya dan kadang pada hari pelaksanaan, sehingga tidak ada jaminan informasi sampai tepat waktu. Karena kegiatan akademik terjadwal diprioritaskan (B1) dan bentrok harus dicegah (B3), sistem memerlukan satu sumber data jadwal sebagai acuan, aturan prioritas antar-kegiatan, pemeriksaan bentrok yang mencegah dua pengajuan lolos sekaligus, dan fitur notifikasi yang terpisah dari alur utama. |
| ASR-2 | Saat admin menambah lab, jenis keperluan, atau mengubah penyetuju dan tahapan persetujuan, aturan baru berlaku paling lama 1 jam kerja tanpa mengubah kode program (usulan). | Konfigurabilitas, modifiabilitas | Setiap permohonan harus disetujui oleh admin laboratorium atau pihak yang berwenang (B2), dan permohonan, jadwal, serta data ruangan dikelola admin (O1). Jika aturan persetujuan ditulis langsung di kode program, setiap perubahan kebijakan memerlukan pengembang. Karena itu alur persetujuan dibuat sebagai modul terpisah dan aturannya disimpan sebagai data. |
| ASR-3 | Saat lab mulai dan selesai dipakai, sistem mencatat waktu mulai dan selesai, peminjam, tujuan, serta kondisi ruangan setelah dipakai. Target: semua sesi peminjaman tercatat, tidak ada catatan yang bisa diubah tanpa jejak, dan status hanya dapat diubah oleh petugas berwenang (usulan). | Keamanan (akuntabilitas, integritas) | Asisten lab bertugas mencatat waktu penggunaan dan memeriksa kondisi ruangan (O2), dan riwayat harus disimpan sebagai dokumentasi dan bahan evaluasi (O3). Riwayat juga perlu dapat ditampilkan kembali berdasarkan ruangan, pengguna, dan periode waktu, sehingga data pencatatan harus tertata sejak awal. Hak akses berbeda untuk tiap peran (O1), dan catatan perubahan (log) harus ada di semua alur sejak awal karena sulit ditambahkan belakangan. Karena T1 membatasi layanan pada peminjaman ruang, pencatatan difokuskan pada ruangan, bukan alat. |
| ASR-4 | Saat peminjam atau admin mengakses sistem lewat jaringan pada jam kerja, informasi ketersediaan lab, pengajuan peminjaman, dan status permohonan dapat dibuka dan dipakai. Target: layanan dapat diakses minimal 99% dari jam kerja dalam sebulan (usulan). | Ketersediaan layanan | Melihat ketersediaan ruangan, mengajukan peminjaman, dan memantau status permohonan semuanya memerlukan koneksi jaringan (T3), dan informasi ketersediaan bergantung pada data jadwal yang tercatat di sistem (T2). Jika layanan tidak dapat diakses, pengecekan jadwal dan pengajuan terhenti, dan pencatatan di luar sistem berisiko memicu bentrok. Karena itu data dikelola terpusat dan sistem dirancang agar tetap dapat diakses lewat jaringan, termasuk rencana pemulihan saat terjadi gangguan. |

### Keterkaitan dengan bagian lain

| ASR | Batasan terkait (A3) | Stakeholder terkait (A2) |
| --- | --- | --- |
| ASR-1 | T2, B1, B3 | Mahasiswa, Dosen, Asisten Laboratorium, Admin Laboratorium |
| ASR-2 | B2, O1 | Admin Laboratorium, Kepala Laboratorium / Pengelola Berwenang |
| ASR-3 | O1, O2, O3 | Asisten Laboratorium, Admin Laboratorium, Kepala Laboratorium / Pengelola Berwenang |
| ASR-4 | T2, T3 | Mahasiswa, Dosen, Admin Laboratorium |
