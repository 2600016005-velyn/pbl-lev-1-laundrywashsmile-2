# D2 — System & Solution Design

**Project**: Digital Problem Framing Mini Project — [Washsmile Laundry]
**Tim**: [Aulia Safitri (2600016030), Difa Lilensia (2600016041), Fira Safitri (2600016042), Ni'mah Laeli Sundari (2600016004), Felyna Irma Najwa (2600016005)] | **Tanggal**: [10-11-2026] | **Versi**: [v1.0]
**Template**: TPL-02

> **Petunjuk**: Hapus teks dalam `[...]` setelah diisi.
> Worksheet terkait: WS05, WS06, WS07

---

## 1. Daftar Kebutuhan (User Story)

| # | User Story | Prioritas |
|---|---|---|
| 1 | Sebagai [staff laundry  ], saya ingin [mencatat transaksi penerimaan laundry kiloan dan satuan secara digital, memvalidasi batas kapasitas mesin cuci (maksimal 8 kg per mesin sesuai aturan 1 mesin 1 pelanggan), serta menghitung otomatis total tagihan tarif layanan dan uang kembalian secara presisi.]

 sehingga [waktu pelayanan di meja kasir berkurang drastis dari 60–90 detik menjadi < 30 detik per pelanggan, serta mengeliminasi risiko kesalahan perhitungan tarif maupun uang kembalian fisik. ] | [sedang] |
| 2 | | |
| 3 | | |
| 4 | *(tambah jika perlu)* | |

## 2. Kriteria Penerimaan

| # | Kriteria Penerimaan (terukur & dapat diuji) |
|---|---|
| 1 | [Kondisi yang dapat diperiksa, mis. "sistem menampilkan total dalam < 30 detik"] |
| 2 | |
| 3 | |

## 3. Success Metrics

| Metrik | Baseline (Sekarang) | Target | Cara Mengukur |
|---|---|---|---|
| [mis. waktu pencatatan] | [60-90] | [<30] | [Stock opname bulanan (fisik vs log sistem)] |
| [mis. keakuratan data] | [10-30] | [<5] | [Uji coba langsung eksekusi fitur rekapitulasi harian] |

## 4. Desain Solusi

### 4.1 Konsep Solusi (ringkasan)

_[Pembuatan Website Sistem Reminder Pakaian Yang tidak diambil Pada Laundry.Website ini dibuat untuk membantu pihak laundry.- Data pelanggan seperti nama dan nomor WhatsApp yang diinput oleh admin dianggap valid dan aktif.Pelanggan memiliki dan menggunakan aplikasi WhatsApp yang aktif untuk menerima pesan reminder.Admin laundry secara rutin menginput data transaksi laundry dan mengupdate status pengambilan pakaian ke dalam website.Koneksi internet dan layanan WhatsApp Gateway tersedia dan berfungsi dengan baik saat proses pengiriman reminder berlangsung.]_

### 4.2 Peta Komponen (IPO)

```
Input  ──▶  Proses  ──▶  Output
  │                           │
  └───── Data/Penyimpanan ────┘
```

- **Input**: [apa data yang masuk]
- **Proses**: [apa yang dilakukan sistem]
- **Output**: [apa hasil yang keluar]
- **Data/Penyimpanan**: [di mana data disimpan, mis. file CSV]

### 4.3 Flowchart & Pseudocode

_[Tempel flowchart di `assets/` dan tulis pseudocode di bawah]_

```
[PSEUDOCODE]
```

## 5. Hasil Validasi Pemilik Usaha

- **Tanggal validasi**: [21-10-2026 ]
- **Feedback pemilik**: [Pemilik menyetujui seluruh kebutuhan fungsional (pencatatan transaksi kasir, pembatasan beban 8 kg per mesin cuci, pemotongan stok deterjen otomatis, dan laporan rekap omzet harian). Mitra menekankan bahwa pembayaran harus di awal (kasir tidak memproses cucian jika belum lunas tunai/QRIS).]
- **Perubahan setelah validasi**: [...]

---

**Status**: ⬜ Draf → ⬜ Review Tim → ⬜ Validasi Pemilik → ⬜ Final (GATE 1)