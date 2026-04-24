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

**Sport Center ITK** adalah simulasi sistem pemesanan lapangan olahraga berbasis konsol yang dikembangkan menggunakan bahasa **Kotlin**. Proyek ini bertujuan untuk mengelola jadwal penggunaan lapangan secara adil dan aman dengan menerapkan konsep **Pemrograman Berorientasi Objek (OOP)**.

Sistem ini menjamin integritas data melalui validasi berlapis: pengecekan ketersediaan jadwal lapangan dan kecukupan saldo member sebelum sebuah transaksi reservasi dianggap sah.

---

## 🏗️ Struktur Kelas

Sistem terdiri dari entitas utama yang saling berinteraksi untuk memastikan aturan bisnis terpenuhi.

```text
┌─────────────────────────────────────────────────────────┐
│                        Resepsionis                      │
│  + namaResepsionis: String                              │
│  ─────────────────────────────────────────────────────  │
│  + prosesBooking(m: Member, l: Lapangan, jam: Int): Unit│
│  + batalkanBooking(l: Lapangan): Unit                    │
└──────────────┬──────────────────────┬───────────────────┘
               │ mengelola            │ memvalidasi
               ▼                      ▼
┌──────────────────────┐    ┌──────────────────────┐
│        Member        │    │       Lapangan       │
│  + nama: String      │    │  + namaLapangan: String│
│  - saldo: Int  ←priv │    │  - isTersedia: Boolean │
│  ────────────────    │    │  - hargaSewa: Int    │
│  + isiSaldo(): Unit  │    └──────────────────────┘
│  + bayar(): Unit     │
└──────────────────────┘
