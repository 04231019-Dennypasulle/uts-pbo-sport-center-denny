![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white) ![OOP](https://img.shields.io/badge/Paradigma-OOP-blue?style=for-the-badge) ![Status](https://img.shields.io/badge/Status-Selesai-success?style=for-the-badge) ![ITK](https://img.shields.io/badge/Institut-Teknologi%20Kalimantan-orange?style=for-the-badge)

# Ujian Tengah Semester — Pemrograman Berorientasi Objek (TE2514027)
### Semester Genap 2025/2026 · Program Studi Teknik Elektro

---

## 👤 Identitas

| Keterangan | Detail |
| :--- | :--- |
| **Nama** | Denny Pasulle |
| **NIM** | 04231019 |
| **Kelas** | A |
| **Tema** | Tema ke-11 — Sport Center Kampus (Reservasi Lapangan) |
| **Dosen** | Himawan Wicaksono, S.ST., M.T. |

---

## 📋 Deskripsi Proyek

**Sport Center ITK** adalah simulasi sistem reservasi lapangan olahraga berbasis konsol yang dibangun menggunakan bahasa pemrograman **Kotlin** dengan menerapkan paradigma **Pemrograman Berorientasi Objek (OOP)** secara ketat. Sistem ini mensimulasikan alur kerja nyata di sebuah fasilitas olahraga — mulai dari pengecekan ketersediaan jadwal, verifikasi saldo member, hingga proses *booking* yang aman dan terintegrasi.

Proyek ini dirancang untuk membuktikan bahwa konsep **enkapsulasi** mampu mengamankan data-data sensitif. Data seperti uang (saldo) member dan jadwal lapangan yang sudah terpesan benar-benar tidak bisa dimanipulasi secara langsung dari luar kelas. Setiap perubahan harus melewati metode resmi dari fungsi resepsionis yang sudah dilengkapi validasi berlapis.

---

## 🏗️ Struktur Kelas

Sistem ini terdiri dari tiga kelas utama yang saling berinteraksi secara independen namun terintegrasi.

```text
┌─────────────────────────────────────────────────────────┐
│                      Resepsionis                        │
│  + nama: String                                         │
│  ─────────────────────────────────────────────────────  │
│  + prosesBooking(m: Member, l: Lapangan, jam: String)   │
└──────────────┬──────────────────────┬───────────────────┘
               │ memproses            │ memvalidasi
               ▼                      ▼
┌──────────────────────┐   ┌──────────────────────────────┐
│        Member        │   │           Lapangan           │
│  + id: String        │   │  + nama: String              │
│  + nama: String      │   │  + hargaPerJam: Int          │
│  - saldo: Int ←privat│   │  - jadwalTerbooking ←privat  │
│  ────────────────    │   │  ──────────────────────────  │
│  + topUp(): Unit     │   │  + cekKetersediaan(): Boolean│
│  + potongSaldo():    │   │  + tambahJadwal(): Unit      │
│    Boolean           │   │  + tampilkanJadwal(): Unit   │
└──────────────────────┘   └──────────────────────────────┘
🔐 Konsep Enkapsulasi yang Diterapkan
Enkapsulasi adalah inti keamanan dari proyek ini. Berikut implementasi konkretnya di dalam kode:

Data Hiding pada Keuangan: Atribut saldo di kelas Member menggunakan modifier private set. Ini berarti nilai saldo bisa dibaca untuk ditampilkan di layar utama, tetapi tidak bisa diubah langsung menggunakan tanda sama dengan (=).

Data Hiding pada Jadwal: List jadwalTerbooking di kelas Lapangan diatur sebagai private val. Jadwal tidak bisa dihapus atau ditimpa dari luar kelas.

Custom Setter & Validasi: Satu-satunya jalur resmi untuk memodifikasi data tersebut adalah melalui method. Metode topUp() menolak nominal nol atau negatif, sedangkan metode potongSaldo() akan mengembalikan nilai false jika uang tidak cukup, mencegah terjadinya saldo minus.

Kotlin
// Contoh perlindungan enkapsulasi pada kelas Member
var saldo: Int = saldoAwal
    private set  // ← Nilai tidak bisa diubah langsung dari fungsi main!

fun potongSaldo(jumlah: Int): Boolean {
    return if (jumlah <= saldo) {
        saldo -= jumlah // ← Hanya bisa dikurangi dari dalam kelas
        true
    } else {
        false
    }
}
🧪 Skenario Simulasi
Program membuktikan ketangguhan sistem melalui empat tahapan skenario yang dijalankan berurutan di dalam fun main().

Skenario 1 — GAGAL (Saldo Tidak Mencukupi): Denny mencoba mem- booking lapangan Futsal A seharga Rp100.000, tetapi saldonya hanya Rp50.000. Sistem langsung memblokir transaksi tanpa menyimpan jadwal.

Skenario 2 — TOP UP (Validasi Saldo): Denny melakukan Top Up sebesar Rp100.000. Sistem memvalidasi input dan berhasil memperbarui saldo menjadi Rp150.000 melalui jalur resmi.

Skenario 3 — SUKSES (Transaksi Valid): Dengan saldo yang kini mencukupi dan lapangan masih kosong di jam 10:00, transaksi dinyatakan sukses. Saldo dipotong secara akurat dan jam ditambahkan ke dalam daftar jadwalTerbooking.

Skenario 4 — GAGAL (Jadwal Bentrok): Seseorang mencoba kembali mem- booking lapangan Futsal A di jam 10:00. Meskipun saldonya cukup, sistem langsung menolaknya karena cekKetersediaan mendeteksi bahwa jam tersebut sudah terisi.

🚀 Cara Menjalankan Program
Program ini sangat ringan dan bisa dijalankan tanpa instalasi environment yang rumit. Gunakan salah satu dari dua cara berikut:

Menggunakan Kotlin Playground (Rekomendasi): Buka play.kotlinlang.org, salin seluruh isi file Main.kt, tempel di dalam editor web tersebut, lalu klik tombol Run.

Menggunakan IntelliJ IDEA: Buka folder proyek ini di IntelliJ, pastikan compiler Kotlin sudah aktif, lalu klik tombol Run (segitiga hijau) di sebelah kiri blok fun main().

📁 Struktur Repository
Plaintext
uts-pbo-sport-center-denny/
├── Main.kt                    ← Seluruh source code program Kotlin
├── Laporan_UTS_PBO_Denny.pdf  ← Laporan analisis SDLC & Pemodelan
└── README.md                  ← Dokumentasi proyek yang sedang dibaca ini
📌 Aturan Bisnis (Business Rules)
Sistem Sport Center ini mengunci logika aplikasinya (hardcode) pada kelas Resepsionis dengan urutan aturan bisnis yang mutlak dan tidak bisa diintervensi:

Cek Jadwal Terlebih Dahulu: Sistem wajib mengecek apakah jadwal di jam tersebut kosong. Jika sudah ada yang booking, proses langsung dihentikan sebelum mengecek uang member.

Cek Kecukupan Dana: Transaksi hanya dilanjutkan jika fungsi potongSaldo() pada entitas member mengembalikan status true (dana tersedia).

Auto-Update Integritas: Jika dan hanya jika kedua kondisi di atas lolos (Jadwal kosong + Uang cukup), maka sistem akan secara otomatis mengurangi saldo member dan memblokir jam lapangan tersebut secara bersamaan.
