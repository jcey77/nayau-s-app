# Kedai Kanesyie — App's Premium Store

Website katalog premium dengan tema cream-putih vintage, bubble text, boneka ilustrasi, produk, stok, note, visibilitas produk, notifikasi stok rendah, login/daftar, role member, dan pengaturan OVO/GoPay/QRIS.

## File
- `index.html` — struktur halaman dan modal.
- `style.css` — desain responsif.
- `app.js` — fitur dan koneksi Supabase.
- `supabase.sql` — tabel, trigger, dan aturan keamanan (RLS).

## Setup supaya data tidak hilang dan bisa dipakai dari HP/perangkat lain
1. Buat project gratis di https://supabase.com/ lalu buka **Project Settings → API**.
2. Salin **Project URL** dan ** anon/public key**.
3. Buka `app.js`, isi `SUPABASE_URL` dan `SUPABASE_ANON_KEY`. Jangan pernah memasukkan `service_role` key ke website.
4. Di Supabase buka **SQL Editor → New query**, tempel seluruh isi `supabase.sql`, lalu klik Run.
5. Deploy tiga file (`index.html`, `style.css`, `app.js`) ke repository GitHub. Aktifkan **Settings → Pages → Deploy from a branch → main → /(root)**. Tunggu URL GitHub Pages muncul.
6. Buka website, pilih **Daftar**, buat akun menggunakan email owner. Verifikasi email jika Supabase memintanya.
7. Di Supabase → Table Editor → `profiles`, cari email owner tersebut dan ubah `role` menjadi `owner`. Alternatif: buka SQL Editor, ganti email pada query komentar terakhir di `supabase.sql`, lalu jalankan query itu.
8. Login ulang di website. Menu **Owner studio** akan muncul. Tambahkan produk, atur stok, payment, nomor OVO/GoPay, QRIS, WhatsApp, Telegram, ambang notifikasi stok, dan role member.

## Cara kerja login & keamanan
- Akun member dibuat lewat Supabase Auth. Password login adalah password akun masing-masing.
- Owner ditentukan oleh role `owner` di database, bukan sekadar password yang ditanam di JavaScript. Ini lebih aman daripada menyimpan sandi owner di source code GitHub.
- Kebijakan RLS membatasi perubahan produk, stok, payment, pengaturan, dan role hanya untuk owner.
- Role member yang tersedia: `silucu`, `sigemoi`, `sikecil`; tersedia juga `member` dan `admin`. Pada starter ini, `admin` belum diberi hak owner.
- URL WhatsApp awal diarahkan ke `https://wa.me/62895324866749` dan bisa diubah dari menu Owner → Payment.
- Gambar QRIS dimasukkan sebagai URL gambar publik. Jangan unggah foto QRIS privat ke tempat publik jika tidak ingin siapa pun melihatnya.

## Catatan
- Data tersimpan di Supabase, bukan hanya di cache browser. Karena itu katalog dan akun tetap ada setelah website ditutup atau dibuka dari perangkat lain.
- Untuk stok, web menampilkan peringatan ketika stok sama dengan atau di bawah ambang yang kamu atur.
- Mode tanpa konfigurasi Supabase hanya demo lokal (localStorage) dan **tidak** sinkron antarperangkat. Hubungkan Supabase sebelum dipakai jualan sungguhan.
- Jangan menaruh API secret/service role key, password pribadi, atau kredensial pembayaran sensitif di file frontend.
