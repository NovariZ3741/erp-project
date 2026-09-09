# ERP Dasar — Laravel & Filament

Proyek ini merupakan **sistem ERP (Enterprise Resource Planning) dasar berbasis web** yang dibuat menggunakan **Laravel** dan **Filament**.

Proyek ini dibuat sebagai sarana pembelajaran untuk memahami bagaimana membangun sistem administrasi/ERP menggunakan Laravel, khususnya dalam pembuatan **Admin Panel menggunakan Filament**.

---

## 📌 Tujuan Proyek

ERP ini dirancang sebagai dasar untuk mengelola berbagai data operasional perusahaan dalam satu sistem.

Fitur yang akan dikembangkan secara bertahap meliputi:

- 🔐 Login dan autentikasi pengguna
- 👤 Manajemen pengguna
- 🏢 Manajemen perusahaan
- 📦 Manajemen produk/barang
- 🏷️ Manajemen kategori
- 👥 Manajemen pelanggan
- 🚚 Manajemen pemasok
- 🛒 Penjualan
- 📥 Pembelian
- 📊 Dashboard dan laporan
- 🔑 Hak akses pengguna
- 📝 Riwayat transaksi

> Proyek ini masih dalam tahap pengembangan dan fitur dapat bertambah seiring proses pembelajaran.

---

# 🛠️ Teknologi

Teknologi utama yang digunakan:

- **PHP 8.3+**
- **Laravel 13**
- **Filament**
- **MySQL / MariaDB**
- **Composer**
- **Node.js & NPM**
- **Git & GitHub**

---

# 📋 Persyaratan

Sebelum menjalankan proyek, pastikan komputer telah memiliki:

1. PHP
2. Composer
3. Node.js
4. NPM
5. MySQL/MariaDB
6. Git

Untuk memeriksa instalasi:

```bash
php -v
composer -V
node -v
npm -v
git --version
```

---

# 🚀 Instalasi

## 1. Clone Repository

Clone repository ke komputer:

```bash
git clone <URL-REPOSITORY>
```

Masuk ke folder proyek:

```bash
cd erp-project
```

---

## 2. Install Dependency Laravel

Jalankan:

```bash
composer install
```

Perintah ini akan menginstall seluruh dependency PHP yang terdapat pada `composer.json`.

---

## 3. Install Dependency Frontend

Jalankan:

```bash
npm install
```

Kemudian build asset:

```bash
npm run build
```

Saat melakukan development, dapat menggunakan:

```bash
npm run dev
```

---

# ⚙️ Konfigurasi Environment

Buat file `.env` berdasarkan `.env.example`.

```bash
cp .env.example .env
```

Pada Windows, jika perintah tersebut tidak dapat digunakan, buat salinan `.env.example` secara manual dan beri nama:

```text
.env
```

Kemudian generate application key:

```bash
php artisan key:generate
```

---

# 🗄️ Konfigurasi Database

Buat database baru melalui MySQL/MariaDB.

Contoh:

```text
erp_project
```

Kemudian ubah konfigurasi database pada `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=erp_project
DB_USERNAME=root
DB_PASSWORD=
```

Sesuaikan username dan password dengan konfigurasi database lokal.

Setelah itu jalankan migration:

```bash
php artisan migrate
```

Jika project memiliki seeder:

```bash
php artisan db:seed
```

Atau:

```bash
php artisan migrate:fresh --seed
```

> `migrate:fresh` akan menghapus seluruh tabel yang ada. Jangan gunakan pada database production.

---

# 🎨 Filament

Filament digunakan sebagai **admin panel** untuk mengelola data ERP.

Secara sederhana:

```text
Laravel
   │
   ├── Model
   ├── Migration
   ├── Controller
   │
   └── Filament
        └── Admin Panel
             ├── Resource
             ├── Form
             ├── Table
             └── Page
```

Filament membantu membuat halaman CRUD tanpa harus membuat seluruh halaman administrasi dari awal.

---

# 📚 Konsep Dasar Filament

## 1. Resource

Resource merupakan bagian utama yang digunakan untuk membuat halaman administrasi sebuah model.

Contohnya:

```bash
php artisan make:filament-resource Company
```

Perintah tersebut akan membuat resource untuk model `Company`.

Resource biasanya memiliki beberapa bagian:

```text
CompanyResource
├── Pages
│   ├── CreateCompany
│   ├── EditCompany
│   └── ListCompanies
├── Schemas
└── Tables
```

Struktur dapat berbeda tergantung versi Filament yang digunakan.

---

# 📝 Form

Form digunakan untuk memasukkan atau mengubah data.

Contoh field:

```text
TextInput
Textarea
Select
DatePicker
FileUpload
Toggle
```

Misalnya data perusahaan:

```text
Nama Perusahaan
Alamat
Nomor Telepon
Email
Logo
```

Form akan digunakan pada halaman:

```text
Create
Edit
```

---

# 📊 Table

Table digunakan untuk menampilkan data yang tersimpan di database.

Contohnya:

```text
+----+----------------+----------------+
| ID | Company        | Phone          |
+----+----------------+----------------+
| 1  | Company A      | 08123456789    |
| 2  | Company B      | 08234567890    |
+----+----------------+----------------+
```

Filament menyediakan berbagai column seperti:

```text
TextColumn
ImageColumn
IconColumn
BadgeColumn
```

Table juga dapat memiliki:

- Search
- Sort
- Filter
- Pagination
- Actions
- Bulk Actions

---

# 🖼️ File Upload dan Image

Untuk mengupload gambar, misalnya logo perusahaan, gunakan `FileUpload`.

Contoh konsep:

```php
FileUpload::make('logo')
    ->image()
    ->disk('public')
    ->directory('logos')
```

`directory()` digunakan untuk menentukan lokasi penyimpanan file yang di-upload.

Sedangkan untuk menampilkan gambar pada table:

```php
ImageColumn::make('logo')
    ->disk('public')
```

Jangan menyamakan penggunaan `directory()` pada `FileUpload` dengan `ImageColumn`.

---

# 🔗 Storage Link

Jika menggunakan disk `public`, buat symbolic link storage:

```bash
php artisan storage:link
```

File yang di-upload ke:

```text
storage/app/public/logos
```

dapat diakses melalui:

```text
public/storage/logos
```

---

# 🧱 Membuat Model + Migration + Resource

Contoh alur pengembangan data `Company`:

```text
1. Buat Model
       ↓
2. Buat Migration
       ↓
3. Tentukan struktur database
       ↓
4. Jalankan Migration
       ↓
5. Buat Filament Resource
       ↓
6. Buat Form
       ↓
7. Buat Table
       ↓
8. Test CRUD
```

Contoh perintah:

```bash
php artisan make:model Company -m
```

Kemudian buat resource:

```bash
php artisan make:filament-resource Company
```

---

# 🔐 Admin Panel

Setelah Filament dikonfigurasi, admin panel dapat diakses melalui URL:

```text
http://127.0.0.1:8000/admin
```

Untuk menjalankan server Laravel:

```bash
php artisan serve
```

Kemudian buka:

```text
http://127.0.0.1:8000/admin
```

---

# 👨‍💻 Workflow Pengembangan

Pengembangan fitur sebaiknya dilakukan secara bertahap.

Contoh workflow:

```text
Analisis kebutuhan
       ↓
Desain database
       ↓
Migration
       ↓
Model
       ↓
Filament Resource
       ↓
Form
       ↓
Table
       ↓
Testing
       ↓
Commit Git
       ↓
Push GitHub
```

---

# 🌱 Struktur Project

Struktur utama Laravel:

```text
erp-project/
│
├── app/
│   ├── Filament/
│   │   └── Resources/
│   │
│   ├── Models/
│   └── Providers/
│
├── database/
│   ├── migrations/
│   └── seeders/
│
├── resources/
│   ├── views/
│   └── css/
│
├── routes/
│   └── web.php
│
├── public/
│
├── storage/
│
├── tests/
│
├── .env
├── composer.json
├── package.json
└── README.md
```

---

# 🧪 Menjalankan Project

Untuk development:

Terminal 1:

```bash
php artisan serve
```

Terminal 2:

```bash
npm run dev
```

Kemudian akses:

```text
http://127.0.0.1:8000
```

Untuk admin panel:

```text
http://127.0.0.1:8000/admin
```

---

# 🐛 Troubleshooting

## `vendor/autoload.php` tidak ditemukan

Jika muncul:

```text
Failed opening required vendor/autoload.php
```

jalankan:

```bash
composer install
```

---

## `public/storage` tidak ditemukan

Jalankan:

```bash
php artisan storage:link
```

---

## Asset tidak ditemukan

Jalankan:

```bash
npm install
npm run build
```

Untuk development:

```bash
npm run dev
```

---

## Database tidak ditemukan

Pastikan:

1. Database sudah dibuat.
2. Konfigurasi `.env` benar.
3. MySQL/MariaDB sedang berjalan.
4. Migration sudah dijalankan.

Kemudian:

```bash
php artisan migrate
```

---

# 📌 Catatan Pembelajaran Filament

Filament bukan pengganti Laravel.

Filament berjalan **di atas Laravel** dan memanfaatkan komponen Laravel seperti:

- Eloquent
- Model
- Migration
- Authentication
- Validation
- Database

Karena itu, sebelum membuat fitur dengan Filament, penting untuk memahami dasar:

```text
PHP
 ↓
Laravel
 ↓
Database & Eloquent
 ↓
Filament
 ↓
ERP
```

Filament digunakan untuk mempercepat pembuatan **administrative interface**, sedangkan Laravel tetap menjadi framework utama aplikasi.

---

# 📈 Roadmap

### Phase 1 — Dasar

- [x] Setup Laravel
- [x] Setup Filament
- [x] Admin Panel
- [ ] Company
- [ ] User

### Phase 2 — Master Data

- [ ] Produk
- [ ] Kategori
- [ ] Pelanggan
- [ ] Supplier
- [ ] Satuan
- [ ] Gudang

### Phase 3 — Transaksi

- [ ] Pembelian
- [ ] Penjualan
- [ ] Detail transaksi
- [ ] Stok
- [ ] Pembayaran

### Phase 4 — Laporan

- [ ] Laporan penjualan
- [ ] Laporan pembelian
- [ ] Laporan stok
- [ ] Laporan keuntungan

### Phase 5 — Hak Akses

- [ ] Administrator
- [ ] Kasir
- [ ] Gudang
- [ ] Manager
- [ ] Permission

---

# 🤝 Kontribusi

Pengembangan proyek dilakukan secara bertahap menggunakan Git.

Sebelum mengerjakan fitur:

1. Buat issue.
2. Buat branch.
3. Kerjakan fitur.
4. Test fitur.
5. Commit perubahan.
6. Push branch.
7. Buat Pull Request.

Contoh branch:

```text
feature/company-management
feature/product-management
feature/sales
feature/purchase
```

---

# 📄 Status Project

**Status:** 🚧 Development

Project ini dibuat sebagai proyek pembelajaran dan pengembangan ERP dasar menggunakan Laravel dan Filament.
