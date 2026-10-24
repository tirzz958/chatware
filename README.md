# ChatWave — versi simpel (Firebase + Cloudflare Pages)

Frontend satu file: `index.html`. Tidak memerlukan VPS, Pterodactyl, backend sendiri, atau build command.

## Setup Firebase (sekitar 10–15 menit)
1. Buka https://console.firebase.google.com/ lalu buat project.
2. Tambahkan Web App (ikon `</>`), salin config dari Project settings → Your apps.
3. Buka `index.html`, cari `const firebaseConfig = { ... }`, ganti semua nilai `GANTI_...` dengan config proyekmu.
4. Authentication → Sign-in method → aktifkan Email/Password.
5. Firestore Database → Create database.
6. Storage → Get started.
7. Firestore → Rules, tempel `firestore.rules`, lalu Publish.
8. Storage → Rules, tempel `storage.rules`, lalu Publish.
9. Buat dua akun untuk mencoba chat di dua browser/perangkat.

## Deploy ke Cloudflare Pages
1. Buat repository GitHub dan unggah `index.html`, `firestore.rules`, `storage.rules`, `README.md`.
2. Cloudflare Dashboard → Workers & Pages → Create → Pages → Connect to Git.
3. Pilih repository. Build command kosong (atau `exit 0`); output directory ` / ` tidak perlu diisi untuk Direct Upload. Untuk Git integration, pilih folder root sebagai output directory sesuai UI Cloudflare.
4. Deploy. Tambahkan domain `*.pages.dev` ke Firebase Authentication → Settings → Authorized domains.
5. Buka domain Pages.

## Penting tentang versi starter ini
- Chat pribadi dan grup dibuat dengan pendekatan sederhana. Pencarian pengguna memakai email.
- Rules user read saat ini mengizinkan pengguna login membaca profil/email untuk pencarian sederhana. Ini dapat membocorkan email. Sebelum publik, ubah ke sistem username/invite atau implementasikan pencarian lewat backend tepercaya.
- Untuk pesan realtime, Firestore listener dipakai langsung.
- Upload media menyimpan download URL di pesan. Aturan Storage tetap membatasi akses melalui autentikasi dan keanggotaan chat; jangan menjadikan bucket publik.
- Centang dibaca di UI masih sangat dasar dan belum diimplementasikan sebagai read-receipt per anggota yang lengkap.
- Status online/last seen realtime belum lengkap di versi mini.
- Panggilan suara/video belum disertakan pada versi ini. Implementasi panggilan perlu WebRTC + signaling, serta kemungkinan TURN. Firebase bukan layanan panggilan otomatis.
- UI dan validasi frontend bukan batas keamanan; Rules-lah yang mengatur akses data.
- Uji Rules dengan Firebase Emulator Suite atau dua akun sebelum mempublikasikan.
- Jangan pernah memasukkan service account private key ke frontend. Firebase web config/API key bukan pengganti Security Rules.

Dokumentasi:
- https://firebase.google.com/docs/auth/web/password-auth
- https://firebase.google.com/docs/firestore/query-data/listen
- https://firebase.google.com/docs/storage/security
- https://developers.cloudflare.com/pages/

