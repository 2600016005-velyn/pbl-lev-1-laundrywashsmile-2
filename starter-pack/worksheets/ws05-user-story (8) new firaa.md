# **WORKBOOK: LEMBAR KERJA MAHASISWA WS05**

## **Formulasi Kebutuhan Fungsional: User Story & Acceptance Criteria**

Mata Kuliah: **Konsep Sistem Informasi (KSI)**  
Kerangka Kerja: **Project-Based Learning (PBL) Level 1**  
Fase Learning Spine: **Fase 3 — Define (Minggu 3)**  
Sub-CPMK / SFIA: **S-01.1 (Intermediate - Problem Framing) & S-03.1 (Intermediate - Pemetaan SI)** | **SFIA BUSA L1, REQM L2**  
Keterkaitan Deliverable: **Bahan Utama Deliverable D2 (System & Solution Design - TPL-02)**

### **1\. Identifikasi Kelompok & Rotasi Kepemimpinan**

- **Nama Kelompok:** Lauvi (Kelas A)
- **Objek UMKM Mitra:** Wash Smile Laundry
- **Phase Lead 3 (Define):** Difa Lilensia 2600016041 (Mahasiswa C)
- **Anggota Tim:**

1\. Felyna Irma Najwa (2600016005)

2\. Fira Safitri (2600016042)

3\. Aulia Safitri (2600016030)

4\. Ni'mah Laeli Sundari (2600016004)

### **2\. Landasan Konseptual: Analisis Sistem "What" vs "How"**

Dalam tahap _Systems Analysis_, fokus utama tim adalah menentukan **APA (_What_)** yang dibutuhkan pengguna bisnis untuk memecahkan masalahnya, **BUKAN BAGAIMANA (_How_)** sistem dibangun secara teknis (Marakas & O'Brien, 2013).

- **User Story** merepresentasikan kebutuhan fungsional dari sudut pandang pengguna bisnis dengan pola:  
  \$\$\\text{"Sebagai \[Peran Pengguna\], Saya ingin \[Kemampuan/Fitur\], Sehingga \[Manfaat Bisnis Nyata\]"}\$\$
- **Acceptance Criteria (Given-When-Then)** mendefinisikan batas kondisi kapan sebuah fitur dinyatakan selesai dan memenuhi syarat penerimaan pengguna (Rainer et al., 2021).

### **3\. Workspace A: Formulasi User Story Fungsional**

Petakan minimal **3 User Story Utama** yang langsung menjawab akar masalah pada D1 / WS04:

#### **User Story 1 pembukuan dan pembayaran**

- **Sebagai (As a):** staff Shift Wash Smile Laundry
- **Saya ingin (I want to):** mencatat transaksi penerimaan laundry kiloan dan satuan secara digital, memvalidasi batas kapasitas mesin cuci (maksimal 8 kg per mesin sesuai aturan 1 mesin 1 pelanggan), serta menghitung otomatis total tagihan tarif layanan dan uang kembalian secara presisi
- **Sehingga (So that):** waktu pelayanan di meja kasir berkurang drastis dari 60–90 detik menjadi < 30 detik per pelanggan, serta mengeliminasi risiko kesalahan perhitungan tarif maupun uang kembalian fisik.

#### **User Story 2 stok barang**

- **Sebagai (As a):** staff laundry
- **Saya ingin (I want to):** memantau persediaan stok bahan baku (deterjen cair dan pewangi laundry) yang terpotong otomatis secara real-time berdasarkan beban berat cucian setiap transaksi berhasil, serta menerima notifikasi peringatan jika stok menipis di bawah ambang batas minimum (reorder point)
- **Sehingga (So that):** operasional pencucian tidak pernah terhenti akibat kehabisan bahan baku mendadak, pengadaan stok mandiri lebih terkontrol, dan selisih pencatatan stok bulanan dapat ditekan dari 3% menjadi di bawah 1%.

#### **User Story 3 pengambilan pakaian**

- **Sebagai (As a):** staff Usaha Wash Smile Laundry (Ibu Nandya Aripta Sukma Yanti)
- **Saya ingin (I want to):** melihat dan mencetak ringkasan laporan rekapitulasi harian (total omzet uang masuk, rincian pembayaran tunai vs QRIS, total akumulasi berat cucian kg, dan jumlah transaksi yang diproses per shift) secara otomatis melalui sistem
- **Sehingga (So that):** pemilik dan staf tidak perlu lagi merekap tumpukan nota kertas fisik dan menghitung buku kas secara manual selama 10–30 menit setiap malam saat penutupan toko.

### **4\. Workspace B: Acceptance Criteria Berbasis Skenario (Given-When-Then)**

Susun kriteria penerimaan terstruktur untuk **User Story 1** (mencakup Skenario Sukses dan Skenario Penanganan Eror):

#### **Skenario 1A: Transaksi Penjualan Berhasil (Happy Path)**

- **Diberikan (Given):** Kasir berada pada layar menu transaksi utama aplikasi CLI Wash Smile Laundry, stok deterjen dan pewangi tersedia mencukupi (deterjen > 5.000 ml), dan tarif layanan Reguler Cuci-Setrika adalah Rp 4.500/kg.
- **Ketika (When):** Kasir menginput nama pelanggan "Fira", nomor HP "081234567890", memilih jenis layanan "1. Cuci Setrika Reguler", memasukkan berat cucian "4.5" kg (sesuai batas kapasitas mesin <= 8 kg), serta memasukkan nominal pembayaran tunai Rp 25.000 (total tagihan Rp 20.250).
- **Maka (Then):** Sistem memvalidasi transaksi berhasil, menampilkan struk bukti pembayaran digital di layar dengan nomor ID Transaksi (misal: TRX-001), rincian tagihan Rp 20.250, uang bayar Rp 25.000, uang kembalian Rp 4.750, memotong stok deterjen otomatis sebanyak 450 ml (100 ml/kg), dan menyimpan rekaman transaksi ke file data transaksi.csv.

#### **Skenario 1B: Penanganan Pembayaran Kurang / Overload Beban Mesin (Exception Path)**

- **Diberikan (Given):** kasir memproses transaksi laundry kiloan dengan total tagihan yang dihitung sistem sebesar Rp 36.000 (untuk paket cucian reguler 8.0 kg) pada sistem kasir Wash Smile Laundry.
- **Ketika (When):** Kasir memasukkan nominal pembayaran tunai sebesar Rp 30.000 (atau jika kasir menginput berat beban cucian melebihi batas maksimal 8.0 kg dalam satu mesin tanpa split nota).
- **Maka (Then):** Sistem menolak proses penyimpanan transaksi, menampilkan pesan peringatan eror: "ERROR: Nominal pembayaran kurang Rp 6.000! Transaksi dibatalkan / silakan input ulang nominal yang valid", data transaksi tidak disimpan ke file database, dan persediaan stok deterjen tidak berkurang.

### **5\. Workspace C: Catatan Validasi Kebutuhan dengan Mitra (Field Confirmation)**

- **Tanggal Validasi:** 21 Oktober 2026
- **Narahubung Mitra:** Nandya Aripta Sukma Yanti (Pemilik Wash Smile Laundry)
- **Hasil Konfirmasi User Story:  
  **\[ X \] Seluruh User Story disetujui mitra  
  \[ √ \] Terdapat penyesuaian/revisi kebutuhan:  
  Catatan Validasi Lapangan: Pemilik menyetujui seluruh kebutuhan fungsional (pencatatan transaksi kasir, pembatasan beban 8 kg per mesin cuci, pemotongan stok deterjen otomatis, dan laporan rekap omzet harian). Mitra menekankan bahwa pembayaran harus di awal (kasir tidak memproses cucian jika belum lunas tunai/QRIS).

### **6\. Verifikasi Integritas AI (TPL-07) & Pengesahan**

- **Penggunaan AI Co-pilot:  
  **Apakah tim menggunakan AI untuk membantu merumuskan skenario Given-When-Then? \[ X \] Ya \[ \] Tidak  
  (Catatan: Tim memanfaatkan AI Co-pilot untuk membantu merumuskan skenario Given-When-Then terstruktur dan baku sesuai standar SFIA REQM L2, yang kemudian diverifikasi dan diselaraskan secara empiris dengan alur kerja nyata di outlet Wash Smile Laundry. Formulir TPL-07 disertakan sebagai lampiran).

**Tanda Tangan Tim & Pengesahan Dosen**:

- **Phase Lead 3:** Difa Lilensia — 2600016041 (Tanggal: 23 Oktober 2026) \[ Disetujui \]
- **Dosen Coach:** Imam Azhari, S.Si., M.Cs. (Tanggal: 24 Oktober 2026) \[ X \] Approved