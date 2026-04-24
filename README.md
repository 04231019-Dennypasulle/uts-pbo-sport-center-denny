# 🏟️ ITK-Sport Center — Sistem Reservasi Lapangan Kampus

![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge\&logo=kotlin\&logoColor=white) ![OOP](https://img.shields.io/badge/Paradigma-OOP-blue?style=for-the-badge) ![Status](https://img.shields.io/badge/Status-Selesai-success?style=for-the-badge) ![ITK](https://img.shields.io/badge/Institut-Teknologi%20Kalimantan-orange?style=for-the-badge)

Ujian Tengah Semester — Pemrograman Berorientasi Objek (TE2514027)
Semester Genap 2025/2026 · Program Studi Teknik Elektro

---

## 👤 Identitas

| Keterangan | Detail                           |
| ---------- | -------------------------------- |
| Nama       | Denny Pasulle                    |
| NIM        | 19                               |
| Kelas      | A                                |
| Tema       | Tema ke-11 — Sport Center Kampus |
| Dosen      | Himawan Wicaksono, S.ST., M.T.   |

---

## 📋 Deskripsi Proyek

Sistem ini merupakan simulasi reservasi lapangan berbasis console menggunakan Kotlin dengan konsep OOP.
Fitur utama meliputi:

* Booking lapangan
* Validasi saldo
* Validasi jadwal bentrok
* Manajemen data secara aman (enkapsulasi)

---

## 💻 Source Code (Kotlin)

```kotlin
// =======================
// CLASS MEMBER
// =======================
class Member(
    val id: String,
    val nama: String,
    saldoAwal: Int
) {
    var saldo: Int = saldoAwal
        private set

    fun topUp(jumlah: Int) {
        if (jumlah > 0) {
            saldo += jumlah
            println("[TOP UP] Saldo berhasil ditambah. Saldo sekarang: Rp$saldo")
        } else {
            println("[ERROR] Jumlah top up tidak valid")
        }
    }

    fun potongSaldo(jumlah: Int): Boolean {
        return if (jumlah <= saldo) {
            saldo -= jumlah
            true
        } else {
            false
        }
    }
}

// =======================
// CLASS LAPANGAN
// =======================
class Lapangan(
    val nama: String,
    val hargaPerJam: Int
) {
    private val jadwalTerbooking = mutableListOf<String>()

    fun cekKetersediaan(jam: String): Boolean {
        return !jadwalTerbooking.contains(jam)
    }

    fun tambahJadwal(jam: String) {
        jadwalTerbooking.add(jam)
    }

    fun tampilkanJadwal() {
        println("Jadwal terbooking di $nama: $jadwalTerbooking")
    }
}

// =======================
// CLASS RESEPSIONIS
// =======================
class Resepsionis(val nama: String) {

    fun prosesBooking(member: Member, lapangan: Lapangan, jam: String) {
        println("\n[PROSES BOOKING]")
        println("Member: ${member.nama}")
        println("Lapangan: ${lapangan.nama}")
        println("Jam: $jam")

        // Validasi 1: Cek jadwal
        if (!lapangan.cekKetersediaan(jam)) {
            println("[GAGAL] Jadwal sudah penuh / bentrok!")
            return
        }

        // Validasi 2: Cek saldo
        if (!member.potongSaldo(lapangan.hargaPerJam)) {
            println("[GAGAL] Saldo tidak mencukupi!")
            return
        }

        // Jika lolos semua validasi
        lapangan.tambahJadwal(jam)
        println("[SUKSES] Booking berhasil!")
        println("Sisa saldo: Rp${member.saldo}")
    }
}

// =======================
// MAIN FUNCTION
// =======================
fun main() {

    val member = Member("M001", "Denny", 50000)
    val lapangan = Lapangan("Futsal A", 100000)
    val resepsionis = Resepsionis("Admin")

    println("=== SIMULASI SPORT CENTER ===")

    resepsionis.prosesBooking(member, lapangan, "10:00")
    member.topUp(100000)
    resepsionis.prosesBooking(member, lapangan, "10:00")
    resepsionis.prosesBooking(member, lapangan, "10:00")

    lapangan.tampilkanJadwal()
}
```

---

## 🎮 Skenario Program

* ❌ Gagal: saldo tidak mencukupi
* ➕ Top up saldo
* ✅ Sukses: booking berhasil
* ❌ Gagal: jadwal bentrok

---

## ⚙️ Aturan Bisnis

* Tidak bisa booking jika jadwal bentrok
* Tidak bisa booking jika saldo kurang
* Saldo otomatis berkurang saat booking berhasil

---

## 📁 Struktur Repository

```
UTS-PBO-Sport-Center/
├── Main.kt
├── diagram/
└── README.md
```

---

## 💡 Kesimpulan

Program ini berhasil menerapkan konsep enkapsulasi dengan membatasi akses langsung ke data dan memastikan semua perubahan dilakukan melalui method yang tervalidasi.

---

## ☕ Penutup

Dibuat dengan logika, kopi, dan deadline ☕🔥
Institut Teknologi Kalimantan · 2026
