# **WORKBOOK: LEMBAR KERJA MAHASISWA WS06**

## **Success Metrics (BPI/DMAIC) & Pemetaan Komponen SI Awal**

Mata Kuliah: **Konsep Sistem Informasi (KSI)**  
Kerangka Kerja: **Project-Based Learning (PBL) Level 1**  
Fase Learning Spine: **Fase 3 — Define (Minggu 4)**  
Sub-CPMK / SFIA: **S-01.1 (Intermediate - Problem Framing) & S-03.1 (Intermediate - Pemetaan SI)** | **SFIA BUSA L1, METR L2**  
Keterkaitan Deliverable: **Bahan Utama Deliverable D1 Final (TPL-01) & D2 Draf (TPL-02)**

### **1\. Identifikasi Kelompok & Rotasi Kepemimpinan**

- **Nama Kelompok:** Lauvi (Kelas A)
- **Objek UMKM Mitra:** Wash Smile Laundry
- **Phase Lead 3 (Define):** Difa Lilensia — 2600016041 (Mahasiswa C)
- **Anggota Tim:** 1\. Felyna Irma Najwa (2600016005) 2. Fira Safitri (2600016042) 3. Aulia Safitri (2600016030) 4. Ni'mah Laeli Sundari (2600016004)

### **2\. Landasan Konseptual: Metrik BPI & Pemetaan 5 Pilar SI**

- **Business Process Improvement (BPI)** mengukur keberhasilan perbaikan proses bisnis melalui dua dimensi utama (Rainer et al., 2014):
  - **Efisiensi (_Efficiency_)**: Mengukur penghematan sumber daya (_doing things well_), seperti efisiensi waktu siklus transaksi atau reduksi biaya operasional.
  - **Efektivitas (_Effectiveness_)**: Mengukur pencapaian kualitas/tujuan (_doing the right things_), seperti akurasi data stok, penurunan angka selisih kasir, dan kepuasan pelanggan.
- **Model 5 Pilar SI O'Brien**: Solusi sistem informasi dipetakan ke dalam pilar _People, Hardware, Software, Data,_ dan _Network_ (Marakas & O'Brien, 2013).

### **3\. Workspace A: Matrik Metrik Keberhasilan Bisnis (DMAIC Six Sigma)**

| **Dimensi Metrik**     | **Parameter Kinerja**                                           | **Kondisi Baseline (As-Is)** | **Target Solusi (To-Be)**                  | **Metode Pengukuran**                                |
| ---------------------- | --------------------------------------------------------------- | ---------------------------- | ------------------------------------------ | ---------------------------------------------------- |
| Efisiensi (Waktu)      | Durasi pelayanan transaksi per pelanggan                        | 60 – 90 detik / pelanggan    | < 30 detik / pelanggan                     | Stopwatch sampel 10 transaksi kasir                  |
| ---                    | ---                                                             | ---                          | ---                                        | ---                                                  |
| Efisiensi (Waktu)      | Durasi rekapitulasi harian pemilik                              | 10 – 30 menit / malam        | < 5 menit / malam                          | Uji coba langsung eksekusi fitur rekapitulasi harian |
| ---                    | ---                                                             | ---                          | ---                                        | ---                                                  |
| Efektivitas (Akurasi)  | Tingkat selisih pencatatan stok bahan baku (deterjen & pewangi) | Selisih 3% / bulan           | Selisih &lt; 1% / bulan (Akurasi &gt; 99%) | Stock opname bulanan (fisik vs log sistem)           |
| ---                    | ---                                                             | ---                          | ---                                        | ---                                                  |
| Efektivitas (Kualitas) | Frekuensi kesalahan hitung nota & uang kembalian                | 3 – 5 kali / minggu          | 0 kali / minggu (100% akurat)              | Audit sampel lembar nota transaksi harian            |
| ---                    | ---                                                             | ---                          | ---                                        | ---                                                  |

### **4\. Workspace B: Pemetaan Arsitektur 5 Pilar SI Solusi Awal**

┌────────────────────────────────────────────┐

│ PETA 5 PILAR SISTEM INFORMASI │

├────────────────────────────────────────────┤

│ 1. PEOPLE RESOURCES (Pengguna & Spesialis) │

│ • Pengguna Akhir: Staf Kasir / Operasional Shift (input cuci, timbang, print nota)│

│ • Pengelola Data: Pemilik Usaha (Ibu Nandya - audit rekap, restock deterjen) │

├────────────────────────────────────────────┤

│ 2. HARDWARE RESOURCES (Perangkat Mesin & Media) │

│ • Perangkat Fisik Input: Keyboard, Mouse PC Kasir & Timbangan Digital Laundry │

│ • Perangkat Fisik Output: Layar Monitor PC Kasir & Printer Struk Thermal 58mm │

├────────────────────────────────────────────┤

│ 3. SOFTWARE RESOURCES (Aplikasi & Prosedur Operational) │

│ • Aplikasi Program: Program Kasir & Manajemen Laundry Berbasis Python (CLI) │

│ • Prosedur Pengguna: SOP Input Kasir, Batas Beban 8 Kg & Rekap Tutup Shift │

├────────────────────────────────────────────┤

│ 4. DATA RESOURCES (Struktur Data & Basis Data) │

│ • Data Transaksi: File CSV Transaksi (id_trx, tanggal, nama, kg, tarif, bayar) │

│ • Data Produk/Stok: File CSV Stok (id_bahan, nama, sisa_ml) & Layanan Laundry │

├────────────────────────────────────────────┤

│ 5. NETWORK RESOURCES (Jaringan Communication & Media) │

│ • Konektivitas: Standalone Offline Kasir & Opsi Backup Google Drive / WA │

└────────────────────────────────────────────┘



### **5\. Workspace C: Lembar Persetujuan Formal Mitra (Sign-Off)**

Dengan ini, pemilik / manajer UMKM mitra menyatakan setuju atas rumusan kebutuhan fungsional, target metrik keberhasilan, dan batas cakupan sistem yang dirancang oleh tim mahasiswa.

- **Nama UMKM Mitra:** Wash Smile Laundry
- **Nama Pemilik / Pengelola:** Nandya Aripta Sukma Yanti
- **Tanggal Persetujuan:** 28 Oktober 2026

**Tanda Tangan Persetujuan Mitra**:

**\[ Cap & Tanda Tangan: Nandya Aripta Sukma Yanti — Telah Disetujui Secara Resmi \]**

### **6\. Verifikasi Integritas AI (TPL-07) & Pengesahan**

- **Penggunaan AI Co-pilot:  
  **Apakah tim menggunakan AI untuk membantu merumuskan metrik BPI / diagram 5 pilar SI? \[ X \] Ya \[ \] Tidak  
  (Catatan: Bantuan AI Co-pilot digunakan untuk pemetaan taksonomi 5 Pilar Sistem Informasi O'Brien dan benchmarking metrik DMAIC efisiensi-efektivitas. Seluruh angka baseline dan target diselaraskan dengan hasil observasi empiris di Wash Smile Laundry. Formulir TPL-07 dilampirkan).

**Tanda Tangan Tim & Pengesahan Dosen**:

- **Phase Lead 3:** Difa Lilensia — 2600016041 (Tanggal: 29 Oktober 2026) \[ Disetujui \]
- **Dosen Coach:** Imam Azhari, S.Si., M.Cs. (Tanggal: 30 Oktober 2026) \[ X \] Approved