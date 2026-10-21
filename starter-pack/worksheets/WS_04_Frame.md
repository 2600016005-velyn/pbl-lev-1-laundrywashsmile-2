# WS04: Problem Identification & Scope

**Mata Kuliah**: Konsep Sistem Informasi (KSI)

**Kerangka Kerja**: Project-Based Learning (PBL) Level 1

**Fase Learning Spine**: **Fase 2 — Frame (Problem Discovery & Scope) Minggu / Alokasi Waktu**: Minggu 2 / 14 Jam Belajar

**Sub-CPMK / SFIA**: S-01.1 (Introduce - Problem Framing) | SFIA BUSA L1 (_Business Analysis_), IRMG L1

#### Penanggung Jawab Fase: Phase Lead 2 (Frame — Mahasiswa B)

**Keterkaitan Deliverable**: Sumber Utama Penyusunan **Deliverable D1 (Problem Brief - TPL-01)**

## Identifikasi Tim & Objek Proyek

| **Elemen Informasi**          | **Rincian Identitas Kelompok & Mitra** |
| ----------------------------- | -------------------------------------- |
| **Nama Kelompok / Kelas**     | \[ Lauvi / A \]                        |
| **Phase Lead 2 (Frame - M2)** | \[ Fira Safitra (2600016042) \]        |
| **Nama UMKM Mitra Lapangan**  | \[ Wash Smile Laundry \]               |
| **Pemilik / Kontak Mitra**    | \[ Nandya Aripta Sukma Yanti \]        |

## Matriks Problem Framing & Analisis Akar Masalah (Root Cause Analysis)

Gunakan temuan kuantitatif dari WS03 untuk memisahkan antara **Gejala Permukaan (_Symptoms_)** dan **Akar Masalah Utama (_Root Cause_)** operasional bisnis mitra:

| **No** | **Kategori Observasi**      | **Gejala Permukaan (_Symptoms_)**                                                    | **Akar Masalah Operasional (_Root Cause_)**                                                             | **Bukti Kuantitatif (_Baseline Data_)** |
| ------ | --------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| **1**  | **Proses Transaksi Kasir**  | Transaksi masih dicatat manual pada buku laporan.                                    | Kasir belum menggunakan aplikasi kasir digital, sehingga semua transaksi masih ditulis tangan.          | Rata-rata waktu transaksi = 60 detik.   |
| **2**  | **Pengelolaan Stok Barang** | Pasokan stok tertunda karena bergantung pada mengiriman dari pemilik usaha.          | Tidak adanya SOP pengadaan barang mandiri oleh staff/ tim.                                              | Selisih stok 3% (**tidak menentu).**    |
| **3**  | **Rekapitulasi Keuangan**   | Masih mencatat secara manual mengunakan cacatan nota untuk pemasukkan sehari – hari. | Setiap pemasukkan masih melakukan catatan dibuku kas atau cataan nota yang membutuhkan waktu yang lama. | Durasi rekap harian = **10–30 menit**.  |

## Perumusan Problem Statement Kontekstual

##### Berdasarkan analisis di atas, rumuskan **Problem Statement** utama dalam 1–2 paragraf terstruktur

_Petunjuk_: Hindari mendefinisikan masalah sebagai _"Mitra belum memiliki aplikasi Python/komputer"_. Definisikan dari hambatan bisnis nyata mitra!

**Rumusan Problem Statement Kelompok:**

**_"_**_Pencatatan transaksi dan inventaris yang masih dilakukan secara manual menggunakan buku kertas nota di \[wash smile laundry\] (kondisi As-Is, setiap transaksi dicatat secara tertulis pada buku laporan penerimaan persis di meja kasir) menyebabkan bottleneck operasional berupa waktu transaksi kasir yang lambat (60 detik/pelanggan), keterlambatan pemesanan ulang stok akibat selisih stok 3% per bulan (tidak menentu), serta waktu rekapitulasi harian pemilik usaha yang memakan waktu hingga 10-30 menit setiap harinya. Kondisi ini menghambat efisiensi operasional dan potensi pertumbuhan omzet mitra."_

## Menetapkan Batasan Sistem (System Boundary / Scope Alignment)

Untuk mencegah terjadinya pembengkakan fitur (_Scope Creep_) yang membahayakan penyelesaian proyek dalam 1 semester, tentukan secara tegas apa yang **Masuk Cakupan (_In-Scope_)** dan apa yang **Di Luar Cakupan (_Out-of-Scope_)**:

None

```
┌───────────────────────────────────────────┐
│
│
│
│
│
│
│
SYSTEM BOUNDARY (BATASAN SISTEM)
[ IN-SCOPE: Fitur yang Akan Dibangun ]
```

1. Pencatatan transaksi kasir berbasis konsol (CLI).
2. Pengurangan stok otomatis setiap transaksi berhasil.
3. Pencetakan ringkasan rekapitulasi harian untuk pemilik.

```
│
│
│
│
│
│
│
│─────────────────────────────────────────── │
│ │
│ [ OUT-OF-SCOPE: Di Luar Cakupan Proyek ] │
│ 1. Integrasi gateway pembayaran e-wallet / QRIS otomatis. │
│ 2. Fitur penggajian karyawan / manajemen HRD. │
│ 3. Pemesanan stok otomatis ke supplier luar. │
└────────────────────────────────────────────┘
```

**Tabel Penegasan Cakupan Proyek (_Scope Alignment Table_)**

| **No** | **Modul / Fitur Sistem**          | **Status Cakupan (_In-Scope /_**<br><br>**_Out-of-Scope_)** | **Alasan Pertimbangan Kelayakan (O'Brien)**                                                                           |
| ------ | --------------------------------- | ----------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **1**  | Input Transaksi & Kalkulasi Total | **IN-SCOPE**                                                | Kelayakan Operasional: Mempercepat proses pelayanan transaksi kasir, serta meminimalkan kesalahan perhitungan manual. |
| **2**  | Update Stok Otomatis              | **IN-SCOPE**                                                | Kelayakan Teknis: Dapat menyediakan barang dan saldo TAB yang harus disediakan terus menerus.                         |
| **3**  | Laporan Rekap Harian (Laba/Rugi)  | **IN-SCOPE**                                                | Kelayakan Ekonomi:Dibutuhkan untuk mengetahui berapa krisisnya dan stok barang setiap perbulannya.                    |

| **No** | **Modul / Fitur Sistem**            | **Status Cakupan (_In-Scope /_**<br><br>**_Out-of-Scope_)** | **Alasan Pertimbangan Kelayakan (O'Brien)**                     |
| ------ | ----------------------------------- | ----------------------------------------------------------- | --------------------------------------------------------------- |
| **4**  | Pembayaran Online / Payment Gateway | **OUT-OF-SCOPE**                                            | Pembayaran diawal bisa dilakukan dengan metode QRIS atau tunai. |
| **5**  | Multi-Branch / Banyak Cabang        | **OUT-OF-SCOPE**                                            | Mitra saat ini hanya memiliki 1 lokasi usaha operasional.       |

## Target Metrik Keberhasilan Solusi (To-Be Targets)

##### Tentukan target kuantitatif perbaikan yang ingin dicapai melalui solusi sistem informasi To-Be

| **Indikator Kinerja**               | **Kondisi As-Is (Baseline)** | **Target To-Be (Expected)** | **Estimasi Persentase Peningkatan**      |
| ----------------------------------- | ---------------------------- | --------------------------- | ---------------------------------------- |
| **Waktu Pelayanan Transaksi Kasir** | 60 detik / pelanggan         | **< 30 detik / pelanggan**  | Peningkatan efisiensi<br><br>**50%**     |
| **Durasi Rekapitulasi Harian**      | 10-30 menit / hari           | **< 5 menit / hari**        | Penghematan waktu<br><br>**83.3%**       |
| **Akurasi Pencatatan Stok**         | Selisih 3% / bulan           | **Akurasi > 80%**           | Penurunan tingkat kesalahan selisih stok |

## Refleksi & Lembar Pengesahan Phase Lead

### Pertanyaan Refleksi Tim

- - 1. _Bagaimana tim memastikan bahwa batasan proyek yang ditetapkan realistis untuk diselesaikan dalam 16 minggu?_

##### **Jawab**: \[ kami akan semaksimal mungkin untuk menyelesaikannya dalam waktu 16 minggu dan menghasilkan yang terbaik dalam projek ini dan menjaga kerja sama antara mitra kami \]

- - 1. _Apakah pemilik usaha mitra telah menyetujui batasan sistem yang diusulkan oleh kelompok?_ - **Jawab**: \[ Mitra kami telah menyetujui sistem yang kami buat dengan mengunakan masalah traksaksi yang masih manual pada buku laporan yang akan kami bawah sampai akhir. \]

### Tanda Tangan Pengesahan Phase Lead 2

![](data:image/png;base64,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)

None

```
Disusun oleh Phase Lead 2 (Frame): [ Fira Safitri — 2600016042] Tanggal Penyusunan: [ 16 Oktober 2026 ]
Tanda Tangan Phase Lead 2:
Diverifikasi oleh Dosen Pengampu / Coach:
Tanggal: [ Tanggal ] | Status Checkpoint: [ APPROVED / REVISION NEEDED ] Catatan Dosen:
```