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
uts-pbo-sport-center-denny/
├── Main.kt                    ← Seluruh source code program Kotlin
├── Laporan_UTS_PBO_Denny.pdf  ← Laporan analisis SDLC & Pemodelan
└── README.md                  ← Dokumentasi proyek yang sedang dibaca ini
