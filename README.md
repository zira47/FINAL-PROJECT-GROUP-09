# FINAL-PROJECT-GROUP-09

# Program Manajemen Data Karyawan dan Perhitungan Gaji Otomatis sebagai Solusi Transparansi Gaji Karyawan

Program ini ditulis dalam bahasa C untuk mengelola data karyawan dan menghitung gaji bersih berdasarkan aturan PPh 21 progresif sesuai dengan peraturan perpajakan di Indonesia.

---

## Deskripsi

Program ini mensimulasikan sistem penggajian di mana pengguna dapat menambahkan data karyawan, menghitung pajak penghasilan secara otomatis, dan melihat statistik gaji seluruh karyawan. Perhitungan pajak mengikuti tarif PPh 21 progresif berdasarkan Penghasilan Kena Pajak (PKP) tahunan.

---

## Fitur

| Fitur | Deskripsi |
|---|---|
| Tambah Karyawan | Input data karyawan baru dan perhitungan gaji otomatis |
| Tampilkan Karyawan | Menampilkan detail lengkap seluruh karyawan |
| Cari Karyawan | Pencarian karyawan berdasarkan ID (dengan linear search) |
| Statistik Gaji | Menampilkan gaji tertinggi, terendah, rata-rata, dan total pajak |
| Hitung PPh 21 | Perhitungan pajak progresif 5 lapisan sesuai dengan aturan perpajakan Indonesia |

---

## Struktur Program

Program ini menggunakan beberapa konsep dalam bahasa C:

### Tipe Data
- **`enum Jabatan`** — merepresentasikan jabatan: `STAF`, `MANAJER`, `MAGANG`
- **`enum StatusPerkawinan`** — status pajak: `TK` (Tidak Kawin) / `K` (Kawin)
- **`union InfoGaji`** — berbagi satu lokasi memori antara `gajiPerBulan` dan `bonus`
- **`struct Karyawan`** — menyatukan seluruh data satu karyawan dalam satu tipe

### Fungsi Utama

| Fungsi | Kegunaan |
|---|---|
| `tambahKaryawan()` | Input dan menyimpan data karyawan baru |
| `hitungGaji()` | Menghitung gaji kotor, PTKP, PKP, pajak, dan gaji bersih |
| `getPTKP()` | Menghitung nilai PTKP sesuai status perkawinan dan tanggungan |
| `hitungPPh21()` | Menghitung pajak progresif berdasarkan PKP tahunan |
| `tampilkanKaryawan()` | Menampilkan seluruh data dan rincian perhitungan pajak |
| `cariKaryawan()` | Mencari data karyawan berdasarkan ID |
| `statistik()` | Merangkum statistik gaji seluruh karyawan |

---

## Logika Perhitungan Gaji

### 1. Gaji Kotor Per Bulan
```
Lembur = (Jam - 40) × (Tarif × 1.5)   ← hanya jika jam > 40
Gaji Kotor = (Jam × Tarif) + Lembur
```

### 2. PTKP (Penghasilan Tidak Kena Pajak) — Per Tahun
| Status | PTKP Dasar |
|---|---|
| Tidak Kawin (TK) | Rp 54.000.000 |
| Kawin (K) | Rp 58.500.000 |

Setiap tanggungan PTKP akan ditambah Rp 4.500.000* dengan maksimal 3 tanggungan.

### 3. PKP (Penghasilan Kena Pajak)
```
PKP = (Gaji Kotor × 12) − PTKP
```

### 4. PPh 21 Progresif (Per Tahun)
| Lapisan | Rentang PKP | Tarif |
|---|---|---|
| 1 | s.d. Rp 60 juta | 5% |
| 2 | Rp 60 juta – Rp 250 juta | 15% |
| 3 | Rp 250 juta – Rp 500 juta | 25% |
| 4 | Rp 500 juta – Rp 5 miliar | 30% |
| 5 | Di atas Rp 5 miliar | 35% |

### 5. Gaji Bersih Per Bulan
```
Pajak/Bulan  = PPh 21 Tahunan ÷ 12
Gaji Bersih  = Gaji Kotor/Bulan − Pajak/Bulan
```

---

## 🖥️ Contoh Penggunaan

```
===== SISTEM MANAJEMEN GAJI (PPh 21) =====
1. Tambah Karyawan
2. Tampilkan Karyawan
3. Cari Karyawan
4. Statistik Gaji
5. Keluar
Pilih Menu: 1

ID Karyawan: 101
Nama Karyawan: Budi
Jam Kerja (per bulan): 180
Tarif Per Jam (Rp): 50000

Jabatan
0. Staf
1. Manajer
2. Magang
Pilih Jabatan: 0

Status Perkawinan
0. Tidak Kawin (TK)
1. Kawin (K)
Pilih Status: 1

Jumlah Tanggungan (0-3): 2
Karyawan Berhasil Ditambahkan
```

---

## Batasan-Batasan Dalam Program

- Maksimal 100 karyawan per sesi (`#define MAKS 100`)
- Tanggungan secara otomatis dibatasi antara 0–3
- Data tidak tersimpan ke file; semua hilang saat program ditutup

---

## Konsep pemrograman C yang Digunakan

- `struct`, `enum`, `union`
- Alokasi memori dinamis (`malloc`, `free`)
- Pointer dan pass-by-reference
- Loop `do-while` dan `switch-case`
- Fungsi modular dengan parameter pointer

---
