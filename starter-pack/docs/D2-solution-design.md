# D2 — System & Solution Design

**Project**: Digital Problem Framing Mini Project — [washsmile laundry]
**Tim**: [Aulia Safitri (2600016030), Difa Lilensia (2600016041), Fira Safitri (2600016042), Ni'mah Laeli Sundari (2600016004), Felyna Irma Najwa (2600016005)] | **Tanggal**: [11-11-2026] | **Versi**: [v1.0]
**Template**: TPL-02

> **Petunjuk**: Hapus teks dalam `[...]` setelah diisi.
> Worksheet terkait: WS05, WS06, WS07

---

## 1. Daftar Kebutuhan (User Story)

| # | User Story | Prioritas |
|---|---|---|
| 1 | Sebagai [Kasir], saya ingin [mencatat transaksi penerimaan laundry kiloan dan satuan secara digital, memvalidasi batas kapasitas mesin cuci (maksimal 8 kg per mesin sesuai aturan 1 mesin 1 pelanggan), serta menghitung otomatis total tagihan tarif layanan dan uang kembalian secara presisi] 
sehingga [waktu pelayanan di meja kasir berkurang drastis dari 60–90 detik menjadi < 30 detik per pelanggan, serta mengeliminasi risiko kesalahan perhitungan tarif maupun uang kembalian fisik.] | [Tinggi] |
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
| [Durasi pelayanan
transaksi per pelanggan] | [60-90 detik] | [<30 detik] | [Stopwatch sampel 10 transaksi kasir] |
| [Durasi rekapitulasi harian pemilik] | [10-30 menit] | [<5 menit] | [Uji coba langsung eksekusi fitur rekapitulasi harian] |

## 4. Desain Solusi

### 4.1 Konsep Solusi (ringkasan)

_[Satu paragraf bagaimana prototipe menjawab masalah dari D1]_
Dalam proyek ini kita menggunakan sistem nota secara digital dengan menggunakan kode program kasir & manajemen laundry berbasis python (CLI)

### 4.2 Peta Komponen (IPO)

```
Input  ──▶  Proses  ──▶  Output
  │                           │
  └───── Data/Penyimpanan ────┘
```

- **Input**: [ID Transaksi (auto-generate TRX-XXX), Nama Pelanggan, Nomor HP/WhatsApp, Pilihan Kode Layanan (1: Cuci Setrika Reguler Rp 4.500/kg; 2: Setrika Saja Rp 3.500/kg; 3: Cuci Kering Rp 3.000/kg; 4: Express Cuci Setrika Rp 7.000/kg), Berat Cucian (kg), Nominal Uang Pembayaran Tunai (Rp).]
- **Proses**: [(1) Validasi berat cucian: jika berat_kg > 8.0 kg, berikan peringatan aturan 1 mesin 1 pelanggan (maks 8 kg) dan sarankan split 2 nota; (2) Hitung subtotal = berat_kg * tarif_layanan; (3) Cek nominal pembayaran: validasi uang_bayar >= subtotal; hitung uang_kembali = uang_bayar - subtotal; (4) Hitung konsumsi bahan baku: deterjen_terpakai = berat_kg * 100 ml, pewangi_terpakai = berat_kg * 50 ml; (5) Potong sisa stok pada data persediaan; (6) Generate record transaksi baru dengan timestamp.]
- **Output**: [Struk Nota Digital pada layar terminal kasir (menampilkan ID Transaksi, Tanggal/Jam, Nama Pelanggan, Jenis Layanan, Berat Cucian, Total Tagihan, Uang Bayar, Kembalian, Status "Dalam Proses Pencucian"), serta notifikasi peringatan jika sisa stok deterjen/pewangi mendekati batas minimum.]
- **Data/Penyimpanan**: [Menambahkan baris rekaman baru ke file data transaksi.csv (Append mode), dan memperbarui sisa volume deterjen dan pewangi pada file stok_bahan.csv (Overwrite mode).]

### 4.3 Flowchart & Pseudocode

_[Tempel flowchart di `assets/` dan tulis pseudocode di bawah]_

```
[PSEUDOCODE]
import datetime
import os
import csv
import re

# --- Inisialisasi State dan Konstanta ---
MAX_KAPASITAS_MESIN = 8.0
stok_deterjen_ml = 5000  # contoh stok awal
stok_pewangi_ml = 3000   # contoh stok awal
tgl_trx = datetime.date.today().strftime("%Y-%m-%d")

def Inisialisasi_Basis_Data():
    # Membuat file database CSV jika belum ada
    if not os.path.exists('transaksi.csv'):
        with open('transaksi.csv', mode='w', newline='') as file:
            writer = csv.writer(file)
            writer.writerow(['id_trx', 'tgl_trx', 'nama_pelanggan', 'no_hp', 'nama_layanan', 'berat_kg', 'total_bayar', 'uang_tunai', 'kembalian', 'status_cucian'])

    if not os.path.exists('stok.csv'):
        with open('stok.csv', mode='w', newline='') as file:
            writer = csv.writer(file)
            writer.writerow(['stok_deterjen_ml', 'stok_pewangi_ml'])
            writer.writerow([stok_deterjen_ml, stok_pewangi_ml])
    print("Basis data berhasil diinisialisasi.\n")

def Generate_ID_Transaksi():
    now = datetime.datetime.now()
    return f"TRX{now.strftime('%Y%m%d%H%M%S')}"

def Simpan_Transaksi_CSV(id_trx, tgl_trx, nama_pelanggan, no_hp, nama_layanan, berat_kg, total_bayar, uang_tunai, kembalian, status_cucian):
    with open('transaksi.csv', mode='a', newline='') as file:
        writer = csv.writer(file)
        writer.writerow([id_trx, tgl_trx, nama_pelanggan, no_hp, nama_layanan, berat_kg, total_bayar, uang_tunai, kembalian, status_cucian])

def Update_Stok_CSV(deterjen, pewangi):
    with open('stok.csv', mode='w', newline='') as file:
        writer = csv.writer(file)
        writer.writerow(['stok_deterjen_ml', 'stok_pewangi_ml'])
        writer.writerow([deterjen, pewangi])

def bersihkan_input_uang(teks_input):
    """Membersihkan karakter non-angka seperti Rp, titik pemisah ribuan, atau koma"""
    # Hapus teks 'Rp', 'rp', spasi, titik (biasanya pemisah ribuan di ID), dan koma
    teks_bersih = re.sub(r'[Rr][Pp]\.?|\s+', '', teks_input)
    # Hapus pemisah ribuan berupa titik atau koma
    teks_bersih = teks_bersih.replace(',', '').replace('.', '')
    return teks_bersih

# --- Alur Program Utama ---
def main():
    global stok_deterjen_ml, stok_pewangi_ml

    Inisialisasi_Basis_Data()

    print("=== INPUT TRANSAKSI BARU WASH SMILE LAUNDRY ===")
    nama_pelanggan = input("Nama Pelanggan: ")
    no_hp = input("No. HP: ")

    print("\nPilih Paket: 1.Cuci-Setrika (4500) | 2.Setrika (3500) | 3.Cuci Kering (3000) | 4.Express (7000)")
    kode_layanan = input("Masukkan kode layanan (1-4): ")

    if kode_layanan == '1':
        nama_layanan = "Cuci Setrika Reguler"
        tarif_per_kg = 4500
    elif kode_layanan == '2':
        nama_layanan = "Setrika Saja"
        tarif_per_kg = 3500
    elif kode_layanan == '3':
        nama_layanan = "Cuci Kering"
        tarif_per_kg = 3000
    elif kode_layanan == '4':
        nama_layanan = "Express Cuci Setrika"
        tarif_per_kg = 7000
    else:
        print("ERROR: Kode layanan tidak valid!")
        return

    try:
        berat_kg = float(input("Berat (kg): "))
    except ValueError:
        print("ERROR: Input berat harus berupa angka!")
        return

    if berat_kg <= 0:
        print("ERROR: Berat pakaian harus lebih besar dari 0 kg!")
        return

    if berat_kg > MAX_KAPASITAS_MESIN:
        print("\nPERINGATAN: Beban cucian melebihi kapasitas maksimal mesin (8.0 kg)!")
        print("Sesuai SOP 1 Mesin 1 Pelanggan, cucian disarankan dipisah menjadi 2 mesin.\n")

    deterjen_butuh = berat_kg * 100   # 100 ml per kg
    pewangi_butuh  = berat_kg * 50    # 50 ml per kg

    if (stok_deterjen_ml < deterjen_butuh) or (stok_pewangi_ml < pewangi_butuh):
        print("PERINGATAN: Persediaan bahan baku menipis! Harap segera lakukan restock.\n")

    subtotal = berat_kg * tarif_per_kg
    total_bayar = subtotal
    print(f"Total Tagihan: Rp {total_bayar:,.0f}")

    raw_uang_tunai = input("Uang Tunai Pembayaran: ")
    cleaned_uang_tunai = bersihkan_input_uang(raw_uang_tunai)

    try:
        uang_tunai = float(cleaned_uang_tunai)
    except ValueError:
        print("ERROR: Input pembayaran harus berupa angka! (Contoh: 36000 atau Rp 36.000)")
        return

    if uang_tunai >= total_bayar:
        kembalian = uang_tunai - total_bayar
        stok_deterjen_ml -= deterjen_butuh
        stok_pewangi_ml -= pewangi_butuh
        status_cucian = "Dalam Proses Pencucian"
        id_trx = Generate_ID_Transaksi()

        Simpan_Transaksi_CSV(id_trx, tgl_trx, nama_pelanggan, no_hp, nama_layanan, berat_kg, total_bayar, uang_tunai, kembalian, status_cucian)
        Update_Stok_CSV(stok_deterjen_ml, stok_pewangi_ml)

        print("\n==================================================")
        print("        NOTA TRANSAKSI WASH SMILE LAUNDRY        ")
        print("==================================================")
        print(f"No. Nota   : {id_trx}")
        print(f"Pelanggan  : {nama_pelanggan} ({no_hp})")
        print(f"Layanan    : {nama_layanan}")
        print(f"Berat      : {berat_kg} kg")
        print(f"Total      : Rp {total_bayar:,.0f}")
        print(f"Bayar      : Rp {uang_tunai:,.0f}")
        print(f"Kembalian  : Rp {kembalian:,.0f}")
        print(f"Status     : {status_cucian}")
        print("==================================================")
        print("Terima Kasih atas Kepercayaan Anda di Wash Smile! ")
    else:
        print(f"ERROR: Uang tunai pembayaran kurang Rp {total_bayar - uang_tunai:,.0f}")
        print("Transaksi dibatalkan. Data tidak disimpan.")

if __name__ == '__main__':
    main()
```

## 5. Hasil Validasi Pemilik Usaha

- **Tanggal validasi**: [21-10-2026]
- **Feedback pemilik**: [: Pemilik menyetujui seluruh kebutuhan fungsional (pencatatan transaksi kasir, pembatasan beban 8 kg per mesin cuci, pemotongan stok deterjen otomatis, dan laporan rekap omzet harian). Mitra menekankan bahwa pembayaran harus di awal (kasir tidak memproses cucian jika belum lunas tunai/QRIS).]
- **Perubahan setelah validasi**: [...]

---

**Status**: ⬜ Draf → ⬜ Review Tim → ⬜ Validasi Pemilik → ⬜ Final (GATE 1)
