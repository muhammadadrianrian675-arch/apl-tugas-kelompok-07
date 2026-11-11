BAB IV POLA
Nama: Muhammad Adrian
NIM: 13020240262

Bagian: U4 – Pola
4.1 Gaya dan Pola yang Digunakan
Taktik pada BAB III menjelaskan langkah teknis untuk memenuhi karakteristik kualitas. Pola (pattern) melengkapinya dengan menentukan bagaimana struktur sistem disusun agar taktik tersebut dapat diterapkan dengan rapi. Pola adalah solusi yang sudah teruji untuk masalah desain yang sering berulang.
Layanan Peminjaman Ruang Laboratorium FIKOM UMI menggunakan gaya arsitektur Client-Server berbasis web: mahasiswa, laboran, dan Kepala Laboratorium mengakses layanan melalui peramban (klien), sedangkan server memproses permintaan dan menyimpan data. Di dalam gaya tersebut dipilih tiga pola dari tiga kategori yang berbeda, yaitu:
Pola	Kategori	Masalah pada layanan yang dijawab	Mendukung
Layered	Pola arsitektur (struktur sistem)	Antarmuka, aturan peminjaman, dan data tercampur sehingga sulit diubah dan diuji	Taktik 1, 2, dan 3
Repository	Pola akses data	Query dan penguncian data tersebar sehingga sulit dioptimalkan dan rawan bentrok	Taktik 1 dan 2 (Skenario 1 dan 2)
State	Pola desain perilaku (behavioral)	Aturan perubahan status permohonan tersebar dan rawan tidak konsisten	Taktik 3 (Skenario 3)

4.2 Pola 1 – Layered (Arsitektur Berlapis)
Aspek	Penjelasan
Kategori	Pola arsitektur (struktural).
Alasan dipilih	Layanan memiliki tiga tanggung jawab yang berbeda: menampilkan halaman kepada pengguna, menjalankan aturan peminjaman (memeriksa slot dan memutuskan permohonan), dan menyimpan jadwal. Taktik pada BAB III juga berada di tempat yang berbeda: indeks pada basis data (Taktik 1), transaksi pada logika peminjaman (Taktik 2), dan polling pada antarmuka (Taktik 3). Pembagian lapisan memberi setiap taktik tempat yang jelas sehingga perubahan di satu tempat tidak merusak yang lain.
Penerapan pada layanan	Layanan dibagi menjadi empat lapisan:
•	Presentasi: Antarmuka Mahasiswa, Antarmuka Laboran/Kepala Laboratorium, dan Controller.
•	Aplikasi: Layanan Ketersediaan, Layanan Peminjaman, dan Layanan Status.
•	Akses Data: JadwalRepository dan PermohonanRepository.
•	Penyimpanan: Basis Data Jadwal.
Setiap lapisan hanya memanggil lapisan tepat di bawahnya.
Kelebihan	•	Tampilan dapat diubah tanpa mengubah aturan peminjaman.
•	Logika pencegahan bentrok berada di satu lapisan sehingga konsisten (mendukung K2 Reliability).
•	Tiap lapisan dapat diuji terpisah, misalnya uji beban 300 pengguna pada Layanan Ketersediaan (K1 Performance).
Kekurangan	•	Permintaan melewati beberapa lapisan sehingga menambah waktu respons sedikit; harus dijaga agar tetap dalam 2 detik (ASR-1).
•	Fitur sederhana, seperti menampilkan aturan penggunaan, tetap harus melewati semua lapisan sehingga kode lebih banyak.

4.3 Pola 2 – Repository
Aspek	Penjelasan
Kategori	Pola akses data (data access).
Alasan dipilih	Taktik 1 (indeks dan optimasi query) dan Taktik 2 (transaksi dan penguncian) sama-sama bergantung pada cara layanan mengakses basis data. Jika perintah SQL tersebar di banyak layanan, query sulit dioptimalkan dan ada risiko satu jalur menyimpan peminjaman tanpa melalui penguncian. Repository memusatkan semua akses data pada satu pintu.
Penerapan pada layanan	•	JadwalRepository: cariByTanggal mengambil hanya data ruangan dan jadwal yang dibutuhkan melalui query berindeks; simpanJikaKosong memeriksa dan menyimpan slot dalam satu transaksi dengan penguncian.
•	PermohonanRepository: menyimpan permohonan, mencari permohonan berdasarkan NIM, dan memperbarui status.
•	Implementasi (JadwalRepositoryDB dan PermohonanRepositoryDB) berisi perintah SQL; layanan hanya mengenal antarmukanya.
Kelebihan	•	Indeks dan query dikelola di satu tempat sehingga mudah dioptimalkan (Taktik 1).
•	Penyimpanan slot selalu lewat satu pintu sehingga tidak ada jalur yang melewati penguncian; ini mendukung target 0 jadwal bentrok (Taktik 2).
•	Layanan dapat diuji dengan repository tiruan tanpa basis data, dan basis data dapat diganti tanpa mengubah layanan.
Kekurangan	•	Menambah antarmuka dan kelas baru sehingga pekerjaan awal lebih banyak.
•	Abstraksi dapat menyembunyikan biaya query, sehingga pengembang tetap harus memeriksa kinerja query secara berkala.
•	Jika kebutuhan query makin beragam, jumlah metode repository bisa membengkak.

4.4 Pola 3 – State
Aspek	Penjelasan
Kategori	Pola desain perilaku (behavioral design pattern).
Alasan dipilih	Permohonan peminjaman memiliki tiga status (menunggu, diterima, ditolak) dengan aturan perubahan yang jelas: hanya permohonan berstatus menunggu yang dapat diputuskan laboran. Jika aturan ini ditulis dengan percabangan if-else di banyak tempat, status bisa tidak konsisten (K2) dan pesan yang diterima mahasiswa bisa keliru (K3). Pola State menjadikan setiap status sebagai kelas sendiri yang mengetahui aturannya.
Penerapan pada layanan	•	Permohonan meneruskan perintah setujui(), tolak(), dan label() ke objek StatusPermohonan.
•	StatusMenunggu: setujui mengubah status menjadi Diterima; tolak mengubah menjadi Ditolak dan melepas slot ruangan.
•	StatusDiterima dan StatusDitolak menolak perubahan lebih lanjut.
•	Layanan Status membaca label status untuk ditampilkan pada halaman mahasiswa yang diperbarui setiap 30 detik (Taktik 3).
Kelebihan	•	Aturan perubahan status terkumpul di kelas statusnya sehingga mudah diperiksa.
•	Menambah status baru, misalnya Dibatalkan, cukup dengan menambah satu kelas.
•	Label status yang ditampilkan kepada mahasiswa selalu seragam.
Kekurangan	•	Menambah jumlah kelas: tiga kelas kecil hanya untuk tiga status.
•	Alur perubahan status tersebar di beberapa kelas sehingga harus dibaca dari beberapa tempat.
•	Untuk jumlah status yang sedikit, pola ini bisa terasa berlebihan.

4.5 Perbedaan Gaya dan Pola
Gaya arsitektur dan pola sering tertukar karena keduanya sama-sama menjelaskan struktur. Perbedaan utamanya terletak pada cakupan dan tujuannya: gaya menentukan jenis komponen dan cara berhubungan untuk seluruh sistem, sedangkan pola menyelesaikan satu masalah desain yang berulang pada bagian tertentu sistem.
Aspek	Gaya (Client-Server)	Pola (Repository dan State)
Cakupan	Seluruh sistem	Satu bagian atau satu masalah tertentu
Fungsi	Menetapkan aturan umum: klien meminta, server memproses dan menjawab	Memberi solusi konkret untuk masalah berulang beserta kelebihan dan kekurangannya
Contoh pada layanan	Peramban mahasiswa meminta halaman ketersediaan, server menjawab dengan data jadwal	Repository memusatkan akses jadwal; State mengatur perubahan status permohonan

Pada layanan ini, gaya Client-Server saja tidak menjelaskan cara mencegah dua mahasiswa memesan slot yang sama. Masalah tersebut baru terjawab oleh pola Repository yang dikombinasikan dengan Taktik 2 (transaksi dan penguncian). Dengan demikian, gaya memberi kerangka umum, dan pola mengisi kerangka itu dengan solusi untuk masalah spesifik.
4.6 Ringkasan Penerapan Pola
Pola	Taktik/Skenario	Kelebihan utama	Kekurangan utama
Layered	Taktik 1, 2, 3	Tanggung jawab terpisah; mudah diubah dan diuji	Waktu respons bertambah sedikit; kode lebih banyak
Repository	Taktik 1 dan 2 (Skenario 1 dan 2)	Query terpusat; satu pintu penyimpanan slot	Kelas dan antarmuka bertambah; biaya query tersembunyi
State	Taktik 3 (Skenario 3)	Aturan status terkumpul; mudah menambah status	Jumlah kelas bertambah; alur tersebar
