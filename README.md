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
// MAIN FUNCTION (SIMULASI)
// =======================
fun main() {

    // Inisialisasi objek
    val member = Member("M001", "Denny", 50000)
    val lapangan = Lapangan("Futsal A", 100000)
    val resepsionis = Resepsionis("Admin")

    println("=== SIMULASI SISTEM SPORT CENTER ===")

    // =======================
    // SIMULASI GAGAL (SALDO KURANG)
    // =======================
    resepsionis.prosesBooking(member, lapangan, "10:00")

    // =======================
    // TOP UP SALDO
    // =======================
    member.topUp(100000)

    // =======================
    // SIMULASI SUKSES
    // =======================
    resepsionis.prosesBooking(member, lapangan, "10:00")

    // =======================
    // SIMULASI GAGAL (JADWAL BENTROK)
    // =======================
    resepsionis.prosesBooking(member, lapangan, "10:00")

    // =======================
    // TAMPILKAN JADWAL
    // =======================
    lapangan.tampilkanJadwal()
}
