## A3. Batasan Sistem

**Penanggung Jawab: Muh. Fahmi Ashar**

Batasan sistem berikut disusun berdasarkan ruang lingkup layanan peminjaman ruang laboratorium di Fakultas Ilmu Komputer Universitas Muslim Indonesia (FIKOM UMI), serta kebutuhan yang diperoleh melalui proses wawancara dan analisis layanan. Batasan ini mencakup aspek teknologi, bisnis, dan operasional yang menjadi dasar dalam menentukan rancangan arsitektur sistem.

| Kategori | No | Batasan | Dampak pada Arsitektur | Sumber |
|---|---|---|---|---|
| Teknologi | T1 | Sistem hanya berfokus pada layanan peminjaman ruang laboratorium dan tidak mencakup peminjaman perangkat komputer maupun alat praktikum secara terpisah. | Struktur database dan fitur sistem difokuskan pada pengelolaan ruangan, data pengguna, jadwal, dan transaksi peminjaman. | Ruang Lingkup Sistem |
| Teknologi | T2 | Informasi ketersediaan ruangan harus disesuaikan dengan jadwal perkuliahan, praktikum, dan peminjaman yang telah tercatat. | Sistem membutuhkan pengelolaan jadwal terpusat serta validasi waktu untuk mencegah bentrokan penggunaan ruangan. | Analisis Kebutuhan |
| Teknologi | T3 | Pengajuan dan pemantauan status peminjaman dilakukan melalui sistem yang membutuhkan koneksi jaringan. | Sistem memerlukan layanan berbasis jaringan agar pengguna dan pengelola dapat mengakses informasi peminjaman. | Asumsi Teknis |
| Bisnis | B1 | Penggunaan ruang laboratorium diprioritaskan untuk kegiatan akademik yang telah terjadwal, seperti perkuliahan dan praktikum. | Sistem harus mempertimbangkan jadwal akademik sebelum menerima permohonan peminjaman ruangan lainnya. | Hasil Wawancara |
| Bisnis | B2 | Setiap permohonan peminjaman harus melalui proses pemeriksaan dan persetujuan oleh admin laboratorium atau pihak yang memiliki kewenangan. | Sistem membutuhkan fitur verifikasi permohonan dengan status menunggu, disetujui, atau ditolak. | Hasil Wawancara |
| Bisnis | B3 | Peminjaman ruangan harus memiliki informasi tujuan penggunaan, identitas peminjam, tanggal, waktu, dan ruangan yang digunakan. | Sistem memerlukan formulir pengajuan dengan data yang wajib diisi dan divalidasi sebelum permohonan dikirimkan. | Analisis Kebutuhan |
| Operasional | O1 | Admin Laboratorium bertanggung jawab terhadap pengelolaan data ruangan, pemeriksaan permohonan, dan administrasi peminjaman. | Sistem memerlukan pembagian hak akses berdasarkan peran pengguna untuk menjaga keamanan dan keteraturan pengelolaan data. | Hasil Wawancara |
| Operasional | O2 | Asisten Laboratorium membantu memantau pelaksanaan peminjaman serta mencatat penggunaan dan kondisi ruangan setelah digunakan. | Sistem membutuhkan fitur pencatatan aktivitas penggunaan ruangan dan dokumentasi kondisi ruangan. | Hasil Wawancara |
| Operasional | O3 | Riwayat peminjaman perlu disimpan sebagai dokumentasi penggunaan fasilitas laboratorium dan bahan evaluasi pengelola. | Sistem memerlukan penyimpanan data riwayat peminjaman yang dapat ditampilkan berdasarkan pengguna, ruangan, dan periode waktu. | Analisis Kebutuhan |

Berdasarkan batasan tersebut, pengembangan subsistem Laboratory Management diarahkan untuk menghasilkan layanan peminjaman ruang laboratorium yang terstruktur, mudah digunakan, dan sesuai dengan kebutuhan pengguna maupun pengelola laboratorium. Batasan ini juga menjadi pedoman agar pengembangan sistem tetap berfokus pada proses peminjaman ruangan tanpa mencakup pengelolaan inventaris atau perangkat laboratorium secara terpisah.
