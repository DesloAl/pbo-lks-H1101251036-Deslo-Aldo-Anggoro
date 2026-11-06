# PBO LKS - Portofolio Praktikum

Nama    : Deslo Aldo Anggoro
NIM     : H1101251036
kelas   : A

## Daftar Pertemuan
    [ ] Pertemuan 1 - Setup dan database        : https://github.com/DesloAl/pbo-lks-H1101251036-Deslo-Aldo-Anggoro/tree/main/pertemuan-01
    [ ] Pertemuan 2 - core OOP                  : https://github.com/DesloAl/pbo-lks-H1101251036-Deslo-Aldo-Anggoro/tree/main/pertemuan-02
    [ ] Pertemuan 3 - Framework dan routing     : https://github.com/DesloAl/pbo-lks-H1101251036-Deslo-Aldo-Anggoro/tree/main/pertemuan-03
    [ ] Pertemuan 4 - Testing Backend           : https://github.com/DesloAl/pbo-lks-H1101251036-Deslo-Aldo-Anggoro/tree/main/pertemuan-04
    [ ] Pertemuan 5 - CRUD Kategori             : https://github.com/DesloAl/pbo-lks-H1101251036-Deslo-Aldo-Anggoro/tree/main/pertemuan-05
    [ ] Pertemuan 6 - Frontend                  : https://github.com/DesloAl/pbo-lks-H1101251036-Deslo-Aldo-Anggoro/tree/main/pertemuan-06
    [ ] Pertemuan 7 - Integrasi dan finalisasi  : https://github.com/DesloAl/pbo-lks-H1101251036-Deslo-Aldo-Anggoro/tree/main/pertemuan-07

## Fitur

### Backend (REST API, port 8000)

- CRUD **Buku** (`judul`, `penulis`, `tahun`, `stok`)
- CRUD **Kategori** (`nama`, `deskripsi`)
- Validasi input; respons **422** jika data tidak valid (contoh: nama kategori kosong)
- Respons JSON seragam (`success`, `message`, `data`)
- Arsitektur **MVC** dengan lapisan Controller, Service, Repository, dan Model
- Penerapan **SOLID**, Repository Pattern, Dependency Injection (Container), dan Front Controller
- Autoload **PSR-4** dengan Composer
- Konfigurasi sensitif lewat file **.env**
- **CORS** aktif agar bisa diakses frontend

### Frontend (port 3000)

- Aplikasi satu halaman (SPA) dengan hash routing
- Halaman **Dashboard**: statistik total buku dan kategori, serta daftar buku terbaru
- Halaman **Buku**: tampil, tambah, ubah, dan hapus (dengan konfirmasi)
- Halaman **Kategori**: tampil, tambah, ubah, dan hapus
- Notifikasi toast untuk sukses dan error
- Tampilan responsif dengan Tailwind CSS

### Daftar Endpoint

| Method | Endpoint | Fungsi |
|---|---|---|
| GET | `/api/books` | Daftar buku |
| GET | `/api/books/{id}` | Detail buku |
| POST | `/api/books` | Tambah buku |
| PUT | `/api/books/{id}` | Ubah buku |
| DELETE | `/api/books/{id}` | Hapus buku |
| GET | `/api/categories` | Daftar kategori |
| GET | `/api/categories/{id}` | Detail kategori |
| POST | `/api/categories` | Tambah kategori |
| PUT | `/api/categories/{id}` | Ubah kategori |
| DELETE | `/api/categories/{id}` | Hapus kategori |

## Struktur Proyek

```
pbo-lks-H1101251036-Deslo-Aldo-Anggoro/
├── rest-api-perpustakaan/      # Backend (PHP, port 8000)
│   ├── public/index.php        # Front Controller
│   ├── src/                    # Config, Core, Database, Models, Repositories, Services, Controllers
│   ├── database/schema.sql
│   ├── .env.example
│   └── composer.json
├── frontend-perpustakaan/      # Frontend (HTML + Tailwind, port 3000)
│   ├── index.html
│   ├── css/custom.css
│   └── js/                     # config.js, api.js, utils.js, app.js, pages/
└── pertemuan-01 ... pertemuan-07/   # Bukti screenshot LKS
```

## Prasyarat

- PHP 8.0 atau lebih baru
- Composer 2.x
- MySQL atau MariaDB (disarankan lewat Laragon atau XAMPP)
- Browser modern dan koneksi internet (Tailwind dan font dimuat dari CDN)

## Cara Menjalankan

### 1. Clone repository

```bash
git clone https://github.com/DesloAl/pbo-lks-H1101251036-Deslo-Aldo-Anggoro.git
cd pbo-lks-H1101251036-Deslo-Aldo-Anggoro
```

### 2. Siapkan Backend

```bash
cd rest-api-perpustakaan
composer install
```

Salin file konfigurasi, lalu sesuaikan isinya:

```bash
# Windows (cmd)
copy .env.example .env

# Linux / macOS / Git Bash
cp .env.example .env
```

Isi `.env` (sesuaikan dengan MySQL Anda):

```
DB_HOST=127.0.0.1
DB_PORT=3306
DB_NAME=perpustakaan
DB_USERNAME=root
DB_PASSWORD=
```

### 3. Siapkan Database

Nyalakan MySQL (Laragon: klik **Start All**), lalu impor skema:

```bash
mysql -u root -p < database/schema.sql
```

Alternatif: buka HeidiSQL atau phpMyAdmin, lalu jalankan isi file `database/schema.sql`.

### 4. Jalankan Backend (Terminal 1)

```bash
cd rest-api-perpustakaan
php -S localhost:8000 -t public
```

Uji dengan membuka `http://localhost:8000/api/books`. Hasilnya harus berupa JSON.

### 5. Jalankan Frontend (Terminal 2)

Buka terminal baru, biarkan terminal backend tetap berjalan:

```bash
cd frontend-perpustakaan
php -S localhost:3000
```

Buka **http://localhost:3000** di browser. Jangan membuka `index.html` langsung dari file explorer, karena ES Module tidak jalan lewat `file://`.

Alternatif: gunakan ekstensi **Live Server** di VS Code, lalu klik kanan `index.html` dan pilih **Open with Live Server**.

## Contoh Pengujian API (cURL)

Perintah berikut untuk **cmd/Cmder di Windows**. Di Git Bash atau Linux/macOS, gunakan kutip tunggal pada `-d`.

```bash
# Tambah kategori
curl -i -X POST http://localhost:8000/api/categories -H "Content-Type: application/json" -d "{\"nama\":\"Sastra\",\"deskripsi\":\"Buku sastra klasik dan modern\"}"

# Validasi nama kosong (harus 422)
curl -i -X POST http://localhost:8000/api/categories -H "Content-Type: application/json" -d "{\"nama\":\"\"}"

# Hapus kategori ID 2
curl -i -X DELETE http://localhost:8000/api/categories/2
```

## Troubleshooting Singkat

| Masalah | Solusi |
|---|---|
| Frontend tampil "Not Found" | Jalankan `php -S localhost:3000` dari dalam folder `frontend-perpustakaan`, tanpa `-t` |
| Layar tetap "Memuat aplikasi..." | Buka F12 → Console; biasanya ada file JS yang belum dibuat atau salah nama |
| "Tidak dapat terhubung ke API" | Pastikan backend jalan di port 8000 dan blok CORS ada di `public/index.php` |
| `Unexpected token '<'` / `Fatal error` | Buka `http://localhost:8000/api/books` untuk melihat pesan error PHP aslinya |
| `SQLSTATE[HY000] [2002]` | MySQL belum jalan, atau `DB_PORT` di `.env` tidak sesuai |
| `Unknown database` / tabel tidak ada | Impor ulang `database/schema.sql` |

## Catatan

- File `.env` tidak boleh di-commit; gunakan `.env.example` sebagai template.
- `Access-Control-Allow-Origin: *` hanya untuk development. Untuk production, ganti dengan domain frontend yang spesifik.