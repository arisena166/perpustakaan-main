<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

## Tentang Perpustakaan Sederhana

Sistem Informasi Manajemen Perpustakaan Sederhana ini adalah -seperti namanya- sebuah sistem sederhana untuk mengelola perpustakaan dari manajemen pustakawan, anggota, buku, hingga peminjaman buku yang dibuat dengan sesederhana mungkin agar mudah digunakan.

Sebetulnya dulu sudah pernah ada aplikasinya, tetapi source codenya tidak ada lagi. Adapun videonya bisa dilihat di [YouTube](https://www.youtube.com/watch?v=Chu2aATRjKg).

## Fitur Perpustakaan Sederhana

| Status | Role          | Modul                     | Keterangan |
| :----: | ------------- | ------------------------- | :--------: |
|   ✅   | _Semua_       | Login                     |     👍     |
|   ❌   | _Semua_       | Login dengan Gmail        |     ✨     |
|   ✅   | Administrator | Manajemen Pustakawan      |    👍📬    |
|   ✅   | Pustakawan    | Manajemen Anggota         |    👍📬    |
|   ✅   | Pustakawan    | Manajemen Buku            |     👍     |
|   ❌   | Pustakawan    | Manajemen Kategori Buku   |     👍     |
|   ✅   | Pustakawan    | Manajemen Peminjaman Buku |  👍║▌💰📬  |
|   ✅   | Pustakawan    | Cetak Kartu Angota        |   ✨💰📬   |
|   ❌   | Anggota       | Histori Peminjaman Buku   |     👍     |
|   ✅   | _Semua_       | Ubah Profil               |     👍     |
|   ✅   | _Semua_       | Ubah Password             |     👍     |

Keterangan:
Sint ea quam exercit
✅ = Sudah ada dan mungkin butuh modifikasi lebih baik  
🔧 = Sudah ada dan butuh perbaikan segera
❌ = Belum ada  
⏲️ = Dalam pengerjaan  
📬 = Butuh SMTP  
║▌ = Butuh barcode scanner (atau logikanya)  
💰 = Butuh perhitungan uang  
👍 = Wajib ada  
✨ = _Nice to have_

> **Administrator juga dapat akses terhadap seluruh aksi yang dapat dilakukan oleh Pustakawan.**

## Kebutuhan Sistem

- PHP 8.1+
- [Composer](https://getcomposer.org)

## Proses Instalasi

- *Fork* repositori ini terlebih dahulu. Lebih senang lagi kalau klik tanda *Star* juga. 
- Kemudian *clone* ke dalam komputer Anda. `git clone url-repositori`
- Masuk ke dalam folder projek. `cd perpustakaan` 
- *Install dependencies*. `composer install`
- Salin file env. `cp .env.example .env`
- Sesuaikan nilai pada env, misalnya kredensial database
- Masukkan data. `php artisan migrate --seed`
- Jalankan projek. `php artisan serve`
- Buka di browser `http://localhost:8000`

## Alur Bisnis

### Login

-   Seluruh user bisa login setelah melakukan verifikasi email.

### Manajemen Pustakawan

-   Admin menambahkan user pustakawan dari panel (minimal nama dan email).
-   Pustakawan menerima email verifikasi berisi link untuk set password.
-   Pustakawan belum bisa login sebelum melakukan verifikasi di atas.
-   Pustakawan belum bisa melakukan transaksi peminjaman buku sebelum melengkapi seluruh data diri.

### Manajemen Anggota

-   Pustakawan menambahkan user anggota dari panel (minimal nama dan email).
-   Anggota menerima email verifikasi berisi link untuk set password.
-   Anggota belum bisa login sebelum melakukan verifikasi di atas.
-   Anggota belum bisa meminjam buku sebelum melengkapi seluruh data diri.

### Peminjaman Buku

-   Pustakawan scan kartu anggota atau input nomor anggota dahulu.
-   Selanjutnya tinggal scan barcode ISBN pada buku.
-   Secara _default_, batas waktu peminjaman adalah tiga (3) hari. Lebih dari itu akan dikenakan biaya Rp 500.
-   Nominal denda diatur di file .env dengan _key_ **DENDA_RUPIAH**.

## Cara menjalankan aplikasi
1. Install [Composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos) secara global (tanpa docker)
2. Install [Docker](https://docs.docker.com/get-docker/)
3. Install `make`, biasanya sudah terpasang secara default oleh OS yang dipakai. Tetapi untuk [Windows, bisa menggunakan Chocolatey](https://stackoverflow.com/a/32127632)
4. Salin repositori dan masuk ke repositori yang telah disalin
    ```sh
    git clone https://github.com/nurfachmi/perpustakaan.git
    cd perpustakaan
    ```
5. Salin file `.env.example` dan beri nama `.env`
    ```sh
    cp .env.example .env
    ```
6. Jalankan command `make` untuk install *dependencies*, dan migrasi db dengan *dummy* data
    ```sh
    make
    ```
    Setelah berhasil, aplikasi sudah bisa diakses pada `http://localhost`. Dan bisa masuk dengan email `admin@nurfachmi.com` dan password `password`.

    Selain aplikasi, terdapat juga antarmuka mail server di `http://localhost:8025` dan SMTP server di port `:1025` yang bisa digunakan untuk melihat email yang dikirim dari aplikasi.

Selain itu, terdapat beberapa `make` *command* yang tersedia
- `make install`
    Untuk menginstall *dependencies* yang dibutuhkan menjalankan Laravel sail
- `make run`
    Untuk menjalankan aplikasi
- `make migrate`
    Mempersiapkan database dan table untuk menjalankan aplikasi (hanya perlu sekali run atau ketika ada perubahan dimodel)
- `make seed`
    Mengisi database dengan *dummy* data untuk keperluan testing (hanya perlu sekali run atau ketika ada perubahan dimodel dan seeder)
- `make restart`
    Menjalankan ulang aplikasi
- `make stop`
    Menghentikan aplikasi
- `make rebuild`
    Jika ingin merebuild image docker (Bisa digunakan ketika ada perubahan yang tidak langsung terlihat)

## Kontribusi

Terima kasih atas niatan kontribusinya kepada Sistem Informasi Manajemen Perpustakaan Sedehana ini.

Silahkan ajukan _Pull Request_ jika ada penambahan, pengurangan, atau perbaikan fitur serta ajukan _Issue_ jika menemukan kekeliruan dalam sistem yang ada, khususnya dari demo yang disediakan.

## License

Sistem Informasi Manajemen Pepustakaan Sederhana dibuat dengan [MIT license](https://opensource.org/licenses/MIT).
