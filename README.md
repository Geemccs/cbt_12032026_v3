# CBT MTsN 1 Mesuji — Sistem Ujian Berbasis Komputer

Aplikasi web CBT (Computer-Based Test) lengkap — konversi 1:1 dari React ke CodeIgniter 4.

## Tech Stack
- **Backend:** CodeIgniter 4 (PHP 8.2)
- **Frontend:** CI4 Views + Tailwind CSS CDN
- **Database:** MySQL 5.7+
- **Auth:** Session-based Multi Guard (Admin / Guru / Siswa)
- **Web Server:** Apache (aaPanel)
- **Timer:** JavaScript Countdown + PHP Server Sync
- **Auto-save:** AJAX Fetch API setiap pilih jawaban

## Requirements
- PHP >= 8.2
- MySQL >= 5.7
- Apache mod_rewrite enabled
- Composer
- aaPanel

## Instalasi di aaPanel

### 1. Clone Repositori
```bash
cd /www/wwwroot
git clone https://github.com/Geemccs/cbt_12032026_v3.git e-ujian.mtsn1mesui.sch.id
cd e-ujian.mtsn1mesui.sch.id
composer install --no-dev --optimize-autoloader
```

### 2. Setup Konfigurasi
```bash
cp env .env
nano .env
```
Isi .env (sudah dikonfigurasi untuk domain dan DB Anda):
```
CI_ENVIRONMENT = production
app.baseURL = 'https://e-ujian.mtsn1mesui.sch.id/'
database.default.hostname = localhost
database.default.database = eujian
database.default.username = eujian
database.default.password = eujian
```

### 3. Setup Database
Buat database di aaPanel > MySQL:
- DBName: eujian
- DBUser: eujian
- DBPass: eujian

### 4. Migrasi & Seeder
```bash
php spark migrate
php spark db:seed InitialDataSeeder
```

### 5. Setup Apache di aaPanel
- Root Directory: `/www/wwwroot/e-ujian.mtsn1mesui.sch.id/public`
- Atau gunakan .htaccess di root untuk redirect ke public/

### 6. Permission
```bash
chmod -R 755 writable/
chown -R www:www writable/
```

## Akun Default

| Role | Identifier | Password |
|------|-----------|---------|
| Admin | admin@mtsn.com | 123 |
| Guru | NIK: 1234567890123456 | 123 |
| Siswa | NISN: 1234567890 | 123 |

## Fitur Lengkap

### Admin
- Dashboard statistik (Siswa, Guru, Kelas, Mapel, Bank Soal, Ruang Ujian)
- CRUD Data Kelas & Mata Pelajaran (tambah masal)
- CRUD Data Guru & Siswa (import Excel, reset password masal)
- Relasi Guru ke Kelas & Mata Pelajaran
- Bank Soal (PG, Essay, Benar/Salah, Menjodohkan)
- Editor Soal Rich Text (Bold, Italic, Gambar, dll)
- Import Soal dari Word (.docx) & Excel
- Arsip Bank Soal
- Setup Ruang Ujian (token, jadwal, acak soal/opsi)
- Monitoring Ujian Real-time
- Export Nilai (Excel, PDF)
- Export Analisis Soal (Excel berwarna)
- Pengumuman per kelas
- Pengaturan ExamBrowser (SEB)
- Manajemen Administrator
- Ubah Password

### Guru
- Dashboard
- Bank Soal (milik sendiri)
- Ruang Ujian (milik sendiri)
- Monitoring Ujian
- Ubah Password

### Siswa
- Dashboard + Pengumuman
- Daftar Ujian Aktif
- Interface Ujian Full-screen
- Timer Countdown
- Auto-save jawaban (AJAX)
- Navigasi nomor soal (hijau=jawab, kuning=ragu)
- Hasil Ujian setelah submit
- Ubah Password

## Struktur Direktori
```
app/
  Controllers/   — Auth, Admin/, Guru/, Siswa/
  Models/        — Semua model database
  Views/         — Layout, auth, admin, guru, siswa
  Filters/       — AdminFilter, GuruFilter, SiswaFilter
  Config/        — Routes, Database, Filters
  Database/
    Migrations/  — 13 file migrasi
    Seeds/       — 12 seeder data awal
public/
  assets/
    js/          — app.js, timer.js, autosave.js
    css/         — custom.css
writable/        — Cache, logs, session
.env             — Konfigurasi environment
```

---
**Developer:** asmin pratama | **MTsN 1 Mesuji** | 2026