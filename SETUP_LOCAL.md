# Setup Aplikasi UKOM Prep Secara Lokal

Panduan ini menjelaskan cara menjalankan aplikasi UKOM Prep di komputer lokal Anda.

## ✅ Persyaratan Sistem

Sebelum memulai, pastikan Anda sudah menginstal:

1. **Node.js & npm** (versi 18 atau lebih baru)
   - Download dari: https://nodejs.org/
   - Verifikasi instalasi: `node --version` dan `npm --version`

2. **PostgreSQL** (versi 12 atau lebih baru)
   - Download dari: https://www.postgresql.org/download/
   - Verifikasi instalasi: `psql --version`

3. **Git** (untuk clone repository)
   - Download dari: https://git-scm.com/

## 📋 Langkah-Langkah Setup

### 1. Clone Repository / Download Project

```bash
# Jika Anda punya repository git
git clone <your-repo-url>
cd ukom-prep

# Atau jika download dari Replit, extract file dan masuk ke folder
cd ukom-prep
```

### 2. Install Dependencies

```bash
npm install
```

Ini akan menginstal semua package yang dibutuhkan untuk frontend dan backend.

### 3. Setup Database PostgreSQL

#### A. Buat Database Baru

```bash
# Buka PostgreSQL
psql -U postgres

# Di dalam psql prompt, jalankan:
CREATE DATABASE ukom_prep;
\q
```

#### B. Catat Connection String

Anda akan membutuhkan connection string dalam format:
```
postgresql://username:password@localhost:5432/ukom_prep
```

Contoh (jika menggunakan user default postgres):
```
postgresql://postgres:password@localhost:5432/ukom_prep
```

Ganti `password` dengan password PostgreSQL Anda.

### 4. Setup Environment Variables

Buat file `.env.local` di root folder project dengan isi:

```env
# Database
DATABASE_URL=postgresql://postgres:your_password@localhost:5432/ukom_prep
PGHOST=localhost
PGPORT=5432
PGUSER=postgres
PGPASSWORD=your_password
PGDATABASE=ukom_prep

# Session
SESSION_SECRET=your-random-secret-key-here-min-32-chars

# Optional: Jika ingin menggunakan Replit Auth (skip jika tidak perlu)
REPL_ID=your-repl-id
ISSUER_URL=https://replit.com/oidc
```

**PENTING:**
- Ganti `your_password` dengan password PostgreSQL Anda
- Ganti `your-random-secret-key-here-min-32-chars` dengan string random 32+ karakter
- Untuk `SESSION_SECRET`, bisa gunakan: `openssl rand -base64 32` (di terminal)

### 5. Setup Database Schema

```bash
# Push schema ke database
npm run db:push
```

Ini akan membuat semua tabel yang diperlukan di database Anda.

### 6. Jalankan Development Server

```bash
npm run dev
```

Server akan start di `http://localhost:5000`

Jika ada pesan seperti:
```
[express] serving on port 5000
```

Maka setup berhasil! ✅

## 🌐 Akses Aplikasi

Setelah server running, buka browser dan akses:

### Public Routes:
- **Halaman Utama**: http://localhost:5000/
- **Tryout UKOM**: http://localhost:5000/exam/select?mode=tryout
- **Simulasi UKOM**: http://localhost:5000/exam/select?mode=simulasi

### Admin Routes:
- **Admin Login**: http://localhost:5000/admin/login
- (Contact administrator for credentials)

## 🛠️ Troubleshooting

### Error: "connect ECONNREFUSED 127.0.0.1:5432"

**Penyebab**: PostgreSQL tidak running atau tidak terinstal

**Solusi**:
```bash
# Windows
# Buka Services dan pastikan PostgreSQL running

# macOS
brew services start postgresql

# Linux
sudo systemctl start postgresql
```

### Error: "database "ukom_prep" does not exist"

**Solusi**: Database belum dibuat. Jalankan langkah 3A lagi.

### Error: "EADDRINUSE: address already in use :::5000"

**Penyebab**: Port 5000 sudah digunakan

**Solusi**:
```bash
# Kill proses yang menggunakan port 5000
# Windows
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# macOS/Linux
lsof -i :5000
kill -9 <PID>
```

### Error: Missing modules atau dependencies

**Solusi**:
```bash
# Clear node_modules dan reinstall
rm -rf node_modules package-lock.json
npm install
npm run dev
```

## 📱 Folder Structure

```
project-root/
├── client/              # Frontend (React + Vite)
│   ├── src/
│   │   ├── pages/      # Halaman aplikasi
│   │   ├── components/ # Komponen UI
│   │   └── lib/        # Utility functions
│   └── index.html
├── server/             # Backend (Express.js)
│   ├── routes.ts       # API endpoints
│   ├── storage.ts      # Database operations
│   └── db.ts           # Database connection
├── shared/             # Shared code
│   └── schema.ts       # Data schemas & validation
├── .env.local          # Environment variables (buat ini!)
├── package.json        # Dependencies
└── vite.config.ts      # Vite configuration
```

## 🎯 Fitur Yang Tersedia

### Mode Tryout
- Latihan per mata kuliah (6 subjects)
- 100 soal per section
- 100 menit per session
- Bookmark dan tracking jawaban
- Hasil dengan persentase

### Mode Simulasi (Dalam Development)
- Simulasi ujian lengkap 180 soal
- 180 menit durasi
- Soal terdistribusi dari semua mata kuliah

### Admin Panel
- Login dengan email: `admin@local`
- Tambah, edit, hapus soal
- Filter soal per mata kuliah/section
- Manage bank soal lengkap

## 🔧 Commands Penting

```bash
# Development
npm run dev              # Start dev server

# Database
npm run db:push         # Sync schema ke database
npm run db:studio      # Buka visual database editor (jika setup)

# Build
npm run build           # Build untuk production
npm run preview         # Preview build hasil

# Lainnya
npm run type-check      # Check TypeScript errors
```

## 📚 Stack Technology

- **Frontend**: React 18 + TypeScript + Vite
- **Backend**: Express.js + TypeScript
- **Database**: PostgreSQL + Drizzle ORM
- **UI Components**: Shadcn/ui + Radix UI
- **Styling**: Tailwind CSS
- **Forms**: React Hook Form + Zod
- **State**: TanStack Query

## ✨ Tips Pengembangan

1. **Hot Reload**: Saat development, perubahan code otomatis di-reload
2. **Database**: Gunakan `npm run db:push` untuk sync schema changes
3. **Debugging**: Buka browser DevTools (F12) untuk melihat logs
4. **API Testing**: Gunakan Postman atau Insomnia untuk test endpoints

## 🚀 Deployment ke Production (Opsional)

Untuk deploy ke platform lain (Heroku, Vercel, Railway, dll):

1. Setup environment variables di platform target
2. Pastikan database PostgreSQL tersedia
3. Run: `npm run build`
4. Deploy sesuai instruksi platform

## 📞 Support

Jika ada error atau pertanyaan:
1. Check console logs (browser DevTools F12)
2. Check terminal logs
3. Verifikasi DATABASE_URL dan environment variables
4. Pastikan PostgreSQL running dan database sudah dibuat

---

**Happy Coding!** 🎉

Semoga setup berjalan lancar. Jika ada masalah, pastikan semua persyaratan sistem sudah terinstal dengan benar.
