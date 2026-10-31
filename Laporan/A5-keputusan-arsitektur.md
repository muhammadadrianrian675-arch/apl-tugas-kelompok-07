# A5. Keputusan Arsitektur (Architecture Decision Records)

## ADR-001: Pola Arsitektur (Architecture Style)
*   **Konteks:** Sistem membutuhkan pengelolaan logika pengajuan dan jadwal, serta pemisahan antara UI dan logika bisnis.
*   **Keputusan:** Menggunakan **Modular Monolith** dengan pendekatan *Client-Server* berbasis *RESTful API*.
*   **Alasan:** Untuk skala sistem internal kampus (peminjaman lab/ruangan), arsitektur *Microservices* terlalu kompleks dan *overkill*. *Modular monolith* memudahkan pemeliharaan kode (memisahkan modul *User*, *Room*, *Booking*, dan *Report*) dengan biaya infrastruktur yang jauh lebih rendah.
*   **Konsekuensi:** Skalabilitas dilakukan pada tingkat aplikasi secara keseluruhan, bukan per modul.

## ADR-002: Pemilihan Basis Data (Database)
*   **Konteks:** Sistem menangani penjadwalan ruangan. Isu paling kritis adalah mencegah bentrokan jadwal (*double-booking*) pada waktu yang sama.
*   **Keputusan:** Menggunakan **Relational Database Management System (RDBMS)** seperti MySQL atau PostgreSQL.
*   **Alasan:** RDBMS mendukung transaksi ACID (*Atomicity, Consistency, Isolation, Durability*) dan penguncian baris (*row-level locking*). Ini menjamin konsistensi data yang mutlak diperlukan saat dua pemohon mencoba meminjam ruangan yang sama di detik yang sama.
*   **Konsekuensi:** Skema basis data harus dirancang secara dinormalisasi dengan relasi yang ketat antara tabel `Users`, `Rooms`, dan `Bookings`.
