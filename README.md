# Catatan Keuangan - Dompet Digital

Aplikasi manajemen keuangan pribadi berbasis Flutter yang dirancang dengan antarmuka modern, interaksi responsif, dan penyimpanan lokal yang aman menggunakan Hive.

---

## 📱 Rincian Aplikasi & Fitur Utama

### 1. Ringkasan & Transaksi Utama (Dashboard/Home)
* **Pencatatan Cepat**: Menambah, mengedit, dan menghapus transaksi (Pemasukan & Pengeluaran) secara instan.
* **Format Mata Uang Rupiah**: Input otomatis diformat dengan pemisah ribuan (titik) menggunakan formatter khusus.
* **Filter Dinamis**: Menyaring transaksi berdasarkan akun, kategori, tipe transaksi, dan rentang tanggal kustom.
* **Pengelompokan Berdasarkan Tanggal**: Daftar transaksi diurutkan secara kronologis dan dikelompokkan per hari untuk kemudahan pemantauan.

### 2. Grafik & Analisis Keuangan
* Visualisasi persentase pengeluaran per kategori menggunakan diagram lingkaran (pie chart) interaktif untuk mempermudah analisis alokasi dana.

### 3. Manajemen Kategori & Pengurutan Dinamis
* **Drag-and-Drop Reordering**: Mengubah urutan kategori secara interaktif dengan menekan dan menggeser ikon pegangan (*drag handle*) di sebelah kiri ikon kategori.
* **Sinkronisasi Otomatis**: Urutan kustom kategori langsung tercermin saat memilih kategori pada form tambah transaksi.

### 4. Manajemen Akun/Dompet (Account Health)
* **Saldo Awal**: Mendukung pengisian saldo awal saat membuat atau mengubah akun.
* **Perhitungan Real-time**: Saldo akhir akun dihitung secara dinamis dari `Saldo Awal + Total Pemasukan - Total Pengeluaran`.
* **Akun Utama (Autoselect)**: Kemampuan menetapkan salah satu akun sebagai akun utama. Akun ini otomatis terpilih ketika menambah transaksi atau hutang baru.

### 5. Buku Kas Pembantu (Utang & Piutang)
* **Manajemen Kontak Ledger**: Pencatatan saldo utang (kita meminjam uang) dan piutang (orang lain meminjam uang kita) per nama kontak.
* **Sinkronisasi Atomik**: Setiap kali utang/piutang ditambah atau dilunasi, riwayat transaksi utama di halaman Home otomatis sinkron secara berkala.
* **Fitur Pelunasan Instan**: Tombol satu klik untuk melunasi seluruh sisa saldo kontak tertentu.

### 6. Pemantauan Aset Kripto (Crypto Portfolio)
* **Integrasi API Indodax**: Memuat harga pasar bid/ask secara real-time dari bursa Indodax.
* **Matriks 2x3 Komprehensif**: Menampilkan metrik investasi lengkap meliputi *Qty*, *Market Buy Price*, *Market Sell Price*, *Average Purchase Price*, *Current Market Price*, dan *P&L (Profit/Loss)*.
* **Privasi (Hide Balance)**: Fitur menyembunyikan saldo portofolio dengan penyimpanan status secara persisten menggunakan Hive.

### 7. Pengaturan & Keamanan Data (Settings & Backup)
* **Batas Maksimal Pengeluaran (Warning Limit)**: Fitur menetapkan batas maksimal pengeluaran bulanan. Jika pengeluaran bulan berjalan melebihi batas, kartu peringatan (*warning card*) akan muncul di halaman utama.
* **Backup & Restore JSON**: Fitur ekspor dan impor seluruh basis data aplikasi dalam format berkas JSON ke memori lokal telepon secara mandiri tanpa dependensi pihak ketiga.

---

## 🛠️ Arsitektur & Teknologi

* **Framework**: Flutter (Dart)
* **Penyimpanan Lokal**: Hive & Hive Flutter (NoSQL database lokal yang sangat cepat)
* **Manajemen State**: State lokal terintegrasi dengan fungsi sinkronisasi global melalui callback.
* **Paket Dependensi Utama**:
  * `hive_flutter` untuk database lokal
  * `path_provider` untuk mengakses direktori penyimpanan lokal
  * `http` untuk pemanggilan API harga kripto Indodax
  * `cupertino_icons` untuk aset ikonografi

---

## 🚀 Cara Install & Menjalankan

### **Prasyarat (Prerequisites)**
Sebelum memulai, pastikan perangkat Anda telah terpasang:
* **Flutter SDK** (Versi 3.12.2 atau lebih baru)
* **Dart SDK**
* Koneksi internet (untuk mengunduh paket dependensi dan memperbarui harga kripto)
* Emulator/Device Android, iOS, atau lingkungan build desktop (Windows)

### **Langkah-langkah Install**
1. **Kloning Repositori**:
   ```bash
   git clone https://github.com/fadilroni/digital-wallet-app
   cd digital-wallet-app
   ```
2. **Unduh Dependensi**:
   Unduh semua paket Flutter/Dart yang dibutuhkan dengan menjalankan perintah berikut di terminal:
   ```bash
   flutter pub get
   ```

### **Langkah-langkah Menjalankan (Run)**
Untuk menjalankan aplikasi dalam mode pengembangan:
1. **Cek Perangkat yang Tersedia**:
   ```bash
   flutter devices
   ```
2. **Jalankan Aplikasi**:
   ```bash
   flutter run
   ```
   *Pilih perangkat target yang sesuai ketika diminta.*

---

## 📁 Struktur Proyek (Project Structure)

Berikut adalah struktur folder dan berkas utama dari proyek ini:

```text
digital-wallet-app/
├── android/                  # Konfigurasi native untuk platform Android
├── assets/                   # Aset gambar, ikon, dan logo aplikasi
├── lib/                      # Kode utama aplikasi (Dart)
│   ├── main.dart             # Titik masuk utama (entry point) aplikasi
│   ├── data_model.dart       # Model data Hive, database lokal, & logika backup
│   └── screens/              # Halaman-halaman UI aplikasi
│       ├── home_screen.dart      # Halaman Dashboard, Filter, & Form Transaksi
│       ├── akun_screen.dart      # Halaman Manajemen Akun & Saldo Awal
│       ├── kategori_screen.dart  # Halaman Manajemen Kategori (Drag & Drop)
│       ├── utang_screen.dart     # Halaman Kas Utang & Piutang
│       ├── asset_screen.dart     # Halaman Portofolio Kripto (API Indodax)
│       └── grafik_screen.dart    # Halaman Grafik Pie Chart Pengeluaran
├── web/                      # Konfigurasi build untuk platform Web
├── windows/                  # Konfigurasi build untuk platform Windows Desktop
└── pubspec.yaml              # Konfigurasi dependensi, aset, & metadata proyek
```

---

## 🤝 Kontribusi (Contributing)

Kontribusi sangat diapresiasi! Jika Anda ingin meningkatkan atau menambahkan fitur pada aplikasi ini, ikuti langkah berikut:

1. **Fork** repositori ini.
2. Buat branch fitur baru Anda:
   ```bash
   git checkout -b feature/fitur-baru
   ```
3. Commit perubahan Anda dengan pesan yang jelas:
   ```bash
   git commit -m "Menambahkan fitur: Deskripsi Fitur Baru"
   ```
4. Push branch tersebut ke repositori Fork Anda:
   ```bash
   git push origin feature/fitur-baru
   ```
   *Atau buat pull request dari branch Anda ke repositori utama.*

---

## 📄 Lisensi (License)

Proyek ini dilisensikan di bawah **MIT License** - Lisensi Open Source yang bebas digunakan, dimodifikasi, dan didistribusikan secara komersial maupun non-komersial. Lihat berkas `LICENSE` untuk informasi lebih lanjut.

---

## 👤 Pembuat (Author)

* **Fadil Roni** - *Developer Utama* - [GitHub](https://github.com/FadilRoni)

---

## ☕ Dukungan (Support)

Jika aplikasi ini bermanfaat bagi Anda, dukung proyek ini dengan cara:
* Memberikan 🌟 **Star** pada repositori ini.
* Melaporkan masalah (bugs) atau saran fitur baru melalui menu **Issues** di GitHub.

---

## 📝 Riwayat Perubahan (Changelog)

### **Versi 2.0.2 (Terbaru)**
* **Perhitungan Saldo Akun Real-time**:
  * Mengintegrasikan kalkulasi saldo secara dinamis yang menggabungkan `Saldo Awal` dengan seluruh riwayat transaksi masuk dan keluar secara real-time.
* **Migrasi Data Lintas Package ID**:
  * Memperbarui mekanisme backup/restore JSON untuk mendeteksi berkas cadangan di folder package lama (`com.example.dompet_pribadi`) sebelum folder baru (`com.example.dompet_digital`), memudahkan transisi data pengguna saat memperbarui aplikasi.

### **Versi 2.0.1**
* **Rebranding Aplikasi**: 
  * Mengubah nama paket dan aplikasi menjadi **Dompet Digital**.
  * Memperbarui konfigurasi Gradle (`applicationId` & `namespace` menjadi `app.bantudigital.dompet_digital`).
  * Memindahkan kelas activity Android (`MainActivity.kt`) ke package directory yang baru.
  * Mengubah judul aplikasi di web dan meta iOS.
* **Optimalisasi Navigasi**:
  * Menghapus animasi geser halaman (*slide*) ketika pengguna mengetuk/men-tap menu bawah (**BottomNavigationBar**) menggunakan `jumpToPage`, memberikan perpindahan menu yang instan.
  * Tetap mempertahankan animasi geser layar yang mulus jika pengguna memindahkan menu dengan mengusap (*swipe*) layar ke kanan/kiri.

### **Versi 2.0.0**
* **Fitur Akun Utama (Autoselect)**: Menambahkan tombol "Set Utama" pada akun agar terpilih secara otomatis saat membuat transaksi atau utang baru.
* **Navigasi Gesture**: Menambahkan kemampuan berpindah menu dengan cara mengusap layar ke kiri atau kanan.
* **Fitur Batas Pengeluaran Maksimal**: Menambahkan menu *Settings* dengan input limit pengeluaran bulanan. Menampilkan kartu peringatan merah di bawah filter kategori di halaman Home jika total pengeluaran melebihi limit.
* **Input Saldo Awal**: Menambahkan kolom input "Saldo Awal" pada dialog tambah/edit akun dengan pemisah ribuan otomatis.
* **Drag-and-Drop Kategori**: Mengubah daftar kategori menjadi `ReorderableListView` agar urutannya dapat diubah dengan menyeret ikon *drag handle* di sebelah kiri ikon kategori. Urutan baru langsung disinkronkan ke form transaksi.

### **Versi 1.4.0**
* **Modul Aset Kripto**:
  * Integrasi API pasar Indodax untuk mendapatkan harga bid dan ask secara real-time.
  * Desain ulang kartu aset dengan tata letak grid 2x3 yang menampilkan Qty, Average Purchase Price, Current Market Price, Market Buy/Sell Price, dan persentase Profit/Loss (P&L).
  * Menambahkan fitur persisten "Sembunyikan Saldo" (isHideSaldo) menggunakan penyimpanan Hive.

### **Versi 1.3.0**
* **Integrasi Buku Kas Utang & Piutang**:
  * Menambahkan pilihan akun/dompet pada transaksi utang/piutang.
  * Sinkronisasi atomik transaksi utang/piutang ke daftar transaksi utama (Home), termasuk pelunasan.
  * Penghapusan kontak utang akan otomatis menghapus transaksi terkait di daftar utama untuk menjaga konsistensi data.

### **Versi 1.2.0**
* **Tampilan Tanggal & Saldo Akun**:
  * Pengelompokan daftar transaksi berdasarkan tanggal transaksi di halaman Home.
  * Perhitungan saldo per akun yang dihitung secara dinamis dari riwayat transaksi.
  * Desain ulang interaksi detail akun menggunakan bottom sheet yang elegan.

### **Versi 1.1.0**
* **Optimalisasi Form & Antarmuka**:
  * Menghapus form input statis di halaman utama, kategori, dan akun, digantikan dengan Floating Action Button (FAB) yang memicu dialog popup.
  * Penyatuan logika tambah data terpusat di halaman `HomeScreen`.
  * Migrasi fitur backup data dari menggunakan plugin eksternal (`file_picker`, `share_plus`) menjadi backup/restore berbasis file JSON menggunakan `path_provider` murni untuk stabilitas kompilasi Android.

### **Versi 1.0.0**
* **Rilis Perdana**:
  * Fitur dasar pencatatan transaksi masuk dan keluar.
  * Manajemen akun, kategori transaksi dasar, dan laporan grafik pie.
  * Penyimpanan data terstruktur berbasis Hive Box.
