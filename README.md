# Mini Project 1: Automasi Pengambilan dan Pembersihan Data Cryptocurrency

Proyek ini bertujuan untuk melakukan ekstraksi data pasar cryptocurrency terkini dari CoinGecko API, melakukan proses pembersihan data (*data cleaning*), dan menyimpan hasilnya ke dalam format CSV yang siap digunakan untuk analisis lebih lanjut atau visualisasi data.

## 🚀 Fitur Utama
1. **Pengambilan Data Otomatis via API**
   - Mengambil data Top Cryptocurrency (berdasarkan kapitalisasi pasar / *market cap*) dari [CoinGecko API](https://www.coingecko.com/en/api).
   - Menggunakan pendekatan *Object-Oriented Programming* (OOP) dengan membuat class `KlienKripto` untuk mengatur pengambilan data dengan berbagai parameter halaman (termasuk pengulangan jika terjadi *timeout*).
2. **Pembersihan Data (*Data Cleaning*)**
   - **Identifikasi Tipe Data:** Melakukan inspeksi tipe data yang ditarik dari JSON secara langsung sebelum dilakukan pemrosesan lebih lanjut.
   - **Penanganan Data Duplikat:** Mengidentifikasi data duplikat menggunakan `.duplicated()` dan menghapusnya menggunakan `.drop_duplicates()` berdasarkan kolom acuan yang pasti unik, yaitu `ID_Koin`.
   - **Penanganan Nilai Kosong (*Missing Values*):** Memastikan kolom `Kapitalisasi_Pasar` memiliki nilai. Jika terdapat data kosong (NaN), secara otomatis akan diisi dengan angka `0` dengan bantuan fungsi moduler `bersihkan_kapitalisasi`.
   - **Konversi Tipe Data (*Type Casting*):** 
     - Mengubah format waktu pada kolom `Terakhir_Diperbarui` yang aslinya bertipe teks (string) menjadi tipe `datetime` melalui fungsi kustom `ubah_ke_tanggal`.
     - Memastikan perhitungan aman dengan mengubah `Harga_USD` dan `Kapitalisasi_Pasar` ke tipe numerik (`float64`).
3. **Penyimpanan Data**
   - Data bersih diekspor dan disimpan ke dalam file `.csv`.

## 📂 Struktur Repositori
- `demo_mp.ipynb`: *Jupyter Notebook* utama yang berisi semua langkah (langkah pengujian API, OOP, pembersihan data, dan ekspor).
- `dataset_kripto.csv`: Hasil dataset final sebanyak 150 baris koin yang telah bersih dan bertipe data yang benar.
- `.env`: File konfigurasi rahasia (*tidak di-push ke repository ini*) untuk mengamankan API key.

## 📊 Temuan Data (*Data Findings*)
Saat mengeksekusi kode *notebook*, berikut adalah ringkasan proses yang terjadi pada data tersebut:
- **Jumlah Awal Data:** API dipanggil sebanyak 3 halaman x 50 koin, sehingga diperoleh **150 baris data**.
- **Data Duplikat:** Terdeteksi beberapa baris duplikat (bergantung pada respons API secara *real-time*). Baris duplikat ini berhasil **dibuang sepenuhnya**.
- **Dataset Akhir:** Menghasilkan data siap analisis, kolom-kolom disesuaikan agar tidak mengandung `null` di tempat yang vital.
- **Tipe Data Akhir (Siap Analisis):**
  - `ID_Koin`, `Nama`, `Simbol` -> `object` (Teks)
  - `Harga_USD`, `Kapitalisasi_Pasar` -> `float64` (Angka desimal)
  - `Terakhir_Diperbarui` -> `datetime64[ns]` (Format waktu/tanggal)

## 🛠️ Cara Penggunaan / Instalasi
1. Clone repositori ini ke komputer lokal Anda.
2. Anda membutuhkan CoinGecko API Key. Buat file `.env` di folder utama dan tambahkan API Key tersebut dengan format:
   ```env
   COIN_API_KEY=API_KEY_ANDA_DISINI
   ```
3. Pastikan Anda telah menginstal pustaka yang dibutuhkan:
   ```bash
   pip install requests pandas python-dotenv
   ```
4. Buka `demo_mp.ipynb` menggunakan Jupyter Notebook atau VS Code, lalu jalankan semua sel (`Run All`).

## 📚 Kesimpulan
Mini Project ini mendemonstrasikan bagaimana kita tidak hanya "sekadar menarik data", tetapi juga secara teliti membersihkan data kotor, membuang informasi berlebih/duplikat, dan memberikan struktur (tipe data) yang benar. Struktur ini mempermudah Data Analyst untuk langsung menggunakan `dataset_kripto.csv` ke dalam *Dashboard* tanpa perlu mengkhawatirkan data anomali.
