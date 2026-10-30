## A3. Batasan Sistem

**Penanggung Jawab: Muh. Fahmi Ashar**

Batasan sistem berikut disusun berdasarkan ruang lingkup layanan peminjaman ruang laboratorium di Fakultas Ilmu Komputer Universitas Muslim Indonesia (FIKOM UMI). Batasan ini digunakan untuk menentukan ruang lingkup pengembangan sistem dari aspek teknologi, bisnis, dan operasional. Beberapa batasan masih berupa asumsi sehingga perlu dikonfirmasi melalui wawancara dengan pihak pengelola laboratorium.

| Kategori | No | Batasan | Dampak pada Arsitektur | Sumber |
|---|---|---|---|---|
| Teknologi | T1 | Sistem berfokus pada pengelolaan peminjaman ruang laboratorium dan tidak mencakup peminjaman perangkat komputer atau alat praktikum secara terpisah. | Struktur database dan fitur sistem difokuskan pada data ruangan, jadwal, pengguna, dan transaksi peminjaman. | Ruang Lingkup Sistem |
| Teknologi | T2 | Informasi ketersediaan ruangan bergantung pada data jadwal perkuliahan, praktikum, dan peminjaman yang tercatat dalam sistem. | Sistem memerlukan pengelolaan data jadwal yang terstruktur agar dapat menghindari bentrokan penggunaan ruangan. | Asumsi |
| Teknologi | T3 | Sistem membutuhkan koneksi jaringan untuk mengakses informasi ketersediaan ruangan, mengajukan peminjaman, dan memantau status permohonan. | Sistem dirancang dengan layanan yang dapat diakses melalui jaringan dan membutuhkan pengelolaan data secara terpusat. | Asumsi |
| Bisnis | B1 | Penggunaan ruang laboratorium diprioritaskan untuk kegiatan akademik yang telah terjadwal, seperti perkuliahan dan praktikum. | Sistem harus mempertimbangkan jadwal akademik sebelum menerima permohonan peminjaman tambahan. | Ketentuan Layanan / Perlu Konfirmasi |
| Bisnis | B2 | Setiap permohonan peminjaman harus melalui proses verifikasi dan persetujuan oleh admin laboratorium atau pihak yang berwenang. | Sistem memerlukan fitur pengelolaan status permohonan, seperti menunggu, disetujui, atau ditolak. | Ruang Lingkup Sistem |
| Bisnis | B3 | Peminjaman ruangan hanya dapat dilakukan sesuai ketersediaan jadwal dan ketentuan penggunaan laboratorium yang berlaku. | Sistem perlu melakukan pemeriksaan jadwal dan validasi permohonan untuk mencegah bentrokan waktu penggunaan. | Asumsi |
| Operasional | O1 | Pengelolaan permohonan, jadwal, dan data ruangan dilakukan oleh admin laboratorium sesuai kewenangannya. | Sistem memerlukan pembagian hak akses berdasarkan peran pengguna agar pengelolaan data lebih terkontrol. | Ruang Lingkup Sistem |
| Operasional | O2 | Asisten laboratorium membantu memantau pelaksanaan peminjaman, mencatat waktu penggunaan, serta memeriksa kondisi ruangan setelah digunakan. | Sistem perlu menyediakan fitur pencatatan aktivitas penggunaan dan kondisi ruangan. | Ruang Lingkup Sistem |
| Operasional | O3 | Riwayat peminjaman perlu disimpan sebagai dokumentasi penggunaan ruang laboratorium dan dapat digunakan untuk kebutuhan evaluasi. | Sistem memerlukan penyimpanan riwayat transaksi peminjaman yang dapat ditampilkan kembali berdasarkan ruangan, pengguna, dan periode waktu. | Ruang Lingkup Sistem |

Batasan tersebut menjadi dasar dalam menentukan kebutuhan dan rancangan arsitektur subsistem Laboratory Management. Dengan adanya batasan sistem, pengembangan dapat lebih terarah pada kebutuhan utama layanan peminjaman ruang laboratorium tanpa mencakup fitur di luar ruang lingkup yang telah ditentukan.
