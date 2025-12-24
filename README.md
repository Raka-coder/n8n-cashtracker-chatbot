# 💰 Telegram Finance Bot with n8n & Google Sheets

Workflow otomasi **n8n** sederhana untuk mencatat pemasukan dan pengeluaran pribadi langsung dari Telegram ke Google Sheets. Bot ini juga dapat memberikan laporan rekapitulasi saldo secara *real-time*.

---

## 📋 Fitur Utama
- **Pencatatan Cepat:** Input transaksi semudah kirim chat (`/input`).
- **Laporan Otomatis:** Menghitung total pemasukan, pengeluaran, dan sisa saldo (`/laporan`).
- **Database Cloud:** Semua data tersimpan aman di Google Sheets.
- **Multi-User Friendly:** Mencatat nama user yang melakukan input (cocok untuk grup keluarga/tim kecil).

---

## 🛠️ Prasyarat
Sebelum menjalankan workflow ini, pastikan Anda memiliki:
1. **n8n** (Versi Desktop, Cloud, atau Self-Hosted).
2. **Akun Telegram** & **Bot Token** (dibuat melalui [@BotFather](https://t.me/BotFather)).
3. **Akun Google** (untuk Google Sheets & Google Cloud Console).

---

## ⚙️ Persiapan Database (Google Sheets)
1. Buat file Google Sheets baru.  
2. Pada **baris pertama (Row 1)**, buat kolom dengan nama persis seperti berikut (huruf kecil semua):

| A          | B      | C        | D           | E     |
|------------|--------|----------|-------------|-------|
| **tanggal** | **jenis** | **nominal** | **keterangan** | **user** |

> **Penting:** Pastikan akun Service Account (email bot Google Cloud) sudah ditambahkan sebagai **Editor** di file Google Sheets ini.

---

## 🚀 Cara Instalasi
1. **Import Workflow**
   - Download file `.json` dari repositori ini.
   - Buka n8n → *Add Workflow* → *Import from File*.
   - Paste kode JSON ke kanvas editor.

2. **Konfigurasi Kredensial**
   - **Telegram Trigger & Telegram Node:** Tambahkan kredensial `Telegram API` menggunakan Token dari BotFather.
   - **Google Sheets Node:** Tambahkan kredensial `Google Sheets OAuth2 API` atau `Service Account`.

3. **Update Node ID**
   - Buka node **"Simpan ke Sheet"** dan **"Baca Semua Data"**.
   - Masukkan **Spreadsheet ID** milik Anda (ID dapat ditemukan di URL Google Sheets).
   - Pastikan **Sheet Name** sesuai (default: `Sheet1`).

4. **Aktifkan Workflow**
   - Klik tombol **Save**.
   - Klik tombol **Publish** (atau aktifkan toggle di pojok kanan atas) agar bot berjalan di background.

---

## 📖 Cara Penggunaan Telegram Finance Bot

Bot ini memungkinkan pencatatan transaksi keuangan pribadi langsung dari Telegram ke Google Sheets menggunakan workflow n8n.

🔧 Persiapan Awal

Pastikan workflow n8n sudah aktif.

Bot Telegram sudah dikonfigurasi dengan token dari BotFather.

Spreadsheet Google Sheets sudah siap dengan kolom: tanggal, jenis, nominal, keterangan, user.

## 📝 Perintah Bot

1. Memulai Bot

Ketik:
```
/start
```
Bot akan membalas dengan panduan format pengisian.

2. Input Transaksi

Gunakan format:
```
/input [Jenis] [Nominal] [Keterangan]
```
Jenis: Masuk/Pemasukan atau Keluar/Pengeluaran.

Nominal: Angka tanpa titik/koma.

Keterangan: Deskripsi singkat transaksi.

Contoh Pemasukan:
```
/input Masuk 5000000 Gaji Bulanan
```
Contoh Pengeluaran:
```
/input Keluar 25000 Makan Siang
```
3. Cek Laporan

Untuk melihat ringkasan keuangan bulan ini:
```
/laporan
```
Bot akan membalas dengan total pemasukan, pengeluaran, dan saldo saat ini.

## 🧠 Logika Workflow

Trigger: Menerima pesan masuk dari Telegram.

Switch Node:
```
/start → Kirim pesan sambutan.

/input → Parse teks → Simpan ke Google Sheets.

/laporan → Ambil data dari Sheets → Hitung agregat → Kirim hasil.
```
## 📌 Catatan

Pastikan kredensial Google Sheets dan Telegram sudah dikonfigurasi di n8n.

Spreadsheet ID dan nama sheet harus sesuai dengan yang digunakan di workflow.

Workflow harus dalam keadaan aktif agar bot merespons perintah.
