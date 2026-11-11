# D3 — Dokumentasi Prototipe & Hasil Uji

**Project**: Digital Problem Framing Mini Project — [ laundry wash smile]
**Tim**: [felyna irma najwa, Aulia safitri, Ni'mah laeli sundari, Fira safitri, Difa lilensia] | **Tanggal**: [11/11/2026] | **Versi**: [v1.0]
**Template**: TPL-03

> **Petunjuk**: Hapus teks dalam `[...]` dan huruf miring setelah diisi.
> Worksheet terkait: WS07, WS09, WS10

---

## 1. Ringkasan Solusi

- **Masalah yang diselesaikan**: [ proyek yang dikerjakan pada penelitian ini adalah pembuatan Website Sistem Reminder Pakaian Yang tidak di ambil Pada Laundry. Website ini dibuat untuk membantu pihak laundry dalam menangani permasalahan pelanggan yang tidak mengambil pakaian bisa dari 1 bulan ]
- **Bentuk prototipe**: [ Customer Datang - Menimbang & Menyortir Pakaian - Melakukan Pembayaran di Kasir - Memilih Mesin & Program Cuci - Proses Cuci + Kering ( ± 1 Jam 10 Menit) - Melipat Pakaian - Customer Puas & Pergi ]
- **Alur utama (input → proses → output)**:
 Nama pelanggan : aulia
 No. HP: 082323209094
 Pilih Paket: 1.Cuci-Strika (4500) 2.Strika (3500) 3.Cuci Kering (3000) 4. Express (7000)
 Masukkan kode layanan (1-4): 1
 Berat (Kg): 8 Kg
 Total tagihan: Rp 36,000
 Uang Tunai Pembayaran: 36000

===========================================================
               NOTA TRANSAKSI WASH SMILE LAUNDRY
============================================================

 NO. Nota   : TRX20261111080027
 Pelanggan  : aulia (082323209094)
 Layanan    : Cuci Strika Reguler 
 Berat      : 8.0 Kg 
 Total      : Rp. 36,000
 Bayar      : Rp. 36,000
 Kembalian  : Rp. 0
 Status     : Dalam proses Pencucian
 
 =============================================================
       
       Terima Kasih atas Kepercayaan Anda di Wash smile!
       
## 2. Desain Singkat

### Flowchart / Pseudocode

*[Gambarkan flowchart di sini atau lampirkan gambar di folder `assets/`]*
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

### Struktur Menu Program

```
1. Menu Utama
   ├── 1.1 [Menu A]
   ├── 1.2 [Menu B]
   ├── 1.3 [Menu C]
   └── 0. Keluar
```

## 3. Kode Program

- **Lokasi kode**: `src/main.py`
- **Python version**: 3.10+
- **Library yang digunakan**: [hanya dari Whitelist Library]

### Penjelasan Struktur Kode

| Fungsi/Bagian | Fungsi |
|---|---|
| `main()`     | [ nama fungsi utama.]           |
| `[import]`   | [ memanggil library]            |
| `[def]`      | [ membuat fungsi ]              |
| `[if]`       | [ jika.]                        |
| `[elif]`     | [ jika kondisi lain]            |
| `[else]`     | [ jika tidak ]                  |
| `[return]`   | [ Menghentikan fungsi ]         |
| `[try]`      | [ Mencoba menjalankan kode ]    |
| `[except]`   | [ menangani kesalahan ]         |
| `[print()]`  | [ menampilkan hasil ]           |
| `[input()]`  | [ memasukkan data ]             |
| `[float ()]` | [ memasukkan ke angka desimal ] |
| `[global]`   | [ menggunakan variable global ] |
| `[with]`     | [ mengelola file ]              |
| `[or]`       | [ atau  ]                       |
| `[=]`        | [ memberikan nilai ]            |
| `[==]`       | [ membandingkan kesamaan ]      |
| `[+==]`      | [menmabhakan nilai ]            |
| `[#]`        | [ komentar ]                    |



## 4. Log Hasil Uji

| # | Kasus Uji | Input | Output Diharapkan | Output Aktual | Status | Perbaikan |
|---|---|---|---|---|---|---|
| 1 | [nama kasus] | [input] | [output] | [aktual] | ⬜ Lulus / ⬜ Gagal | [jika gagal] |
| 2 | | | | | | |
| 3 | | | | | | |
| 4 | *(tambah minimal 3 kasus uji)* | | | | | |
| 5 | | | | | | |

## 5. Catatan Code Walkthrough

- **Nama pengembang yang menjelaskan**: [...]
- **Bagian yang dibantu AI**: [sebutkan bagian mana]
- **Penjelasan manual (apa yang dipahami)**: [...]

## 6. Keterbatasan & Pengembangan Lanjut

- **Keterbatasan prototipe**: [apa yang belum bisa dilakukan]
- **Pengembangan semester berikutnya**: [fitur yang mungkin ditambahkan]

---

**Status**: ⬜ Draf → ⬜ Uji Coba → ⬜ Walkthrough → ⬜ Final (Gate 2)
