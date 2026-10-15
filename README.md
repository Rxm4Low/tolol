# RxLight Of Growing — Vercel Edition

Dashboard premium bergaya mobile-neon seperti referensi video: dark glass UI, neon lime/cyan/violet, login admin, overview cards, aktivitas, pengaturan, dan halaman tentang.

**Developer:** RxMa Official  
**Telegram:** @RxMaStayHigh  
**Contact:** 6285137893277  
**Copyright:** © By RxMa Official - RxLight Of Growing

## Yang disertakan
- Frontend responsif untuk desktop dan mobile.
- Login admin dengan bcrypt password hash dan session cookie HTTP-only.
- API Vercel Functions.
- PostgreSQL online melalui Neon.
- Tabel pengguna, pengaturan, dan aktivitas dibuat otomatis.
- Pengaturan aplikasi disimpan ke database.

## 1. Buat database online
1. Buka https://neon.tech/ lalu buat akun dan project PostgreSQL.
2. Salin **pooled connection string** dari dashboard Neon.
3. Simpan untuk Environment Variable `DATABASE_URL` di Vercel.

## 2. Upload ke GitHub
1. Ekstrak ZIP ini.
2. Buat repository baru di https://github.com/new.
3. Upload semua isi folder ini ke repository (file `package.json`, `vercel.json`, folder `api`, dan `public` harus berada di root repository).

## 3. Deploy di Vercel
1. Buka https://vercel.com/new dan import repository GitHub.
2. Tambahkan Environment Variables di Project Settings → Environment Variables:
   - `DATABASE_URL` = connection string Neon
   - `JWT_SECRET` = string acak rahasia minimal 32 karakter
   - `ADMIN_EMAIL` = email login admin yang kamu pilih
   - `ADMIN_PASSWORD` = password admin yang kuat, minimal 12 karakter
3. Klik Deploy. Setelah sukses, buka URL `.vercel.app` yang diberikan.
4. Jika mengubah environment variables, lakukan redeploy.

## 4. Login
Gunakan `ADMIN_EMAIL` dan `ADMIN_PASSWORD` yang kamu masukkan sendiri di Vercel. Akun admin awal dibuat otomatis pada request API pertama. Tidak ada kredensial admin bawaan di source code.

## Jalankan lokal (opsional)
```bash
npm install
cp .env.example .env
# Isi variabel di .env
npm run dev
```
Buka URL yang ditampilkan oleh Vercel CLI.

## API routes
- `GET /api/health`
- `POST /api/auth/login`
- `GET /api/auth/me`
- `POST /api/auth/logout`
- `GET /api/dashboard`
- `GET /api/activity`
- `GET /api/settings`
- `PUT /api/settings`

## Catatan keamanan dan deployment
- Jangan commit `.env` atau membagikan `DATABASE_URL`, `JWT_SECRET`, dan password admin.
- Gunakan password unik dan panjang. Simpan nilai rahasia hanya di Vercel Environment Variables.
- Gunakan database PostgreSQL hosted; SQLite lokal tidak digunakan di deployment Vercel.
- Endpoint login contoh ini sudah menggunakan password hashing dan cookie `HttpOnly`, tetapi untuk penggunaan publik berskala besar, tambahkan rate limiting/WAF dan pertimbangkan audit keamanan independen.
- Google Fonts membutuhkan koneksi internet; jika diblokir, tampilan memakai fallback system font.
