# Unprotected admin functionality - PortSwigger
https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality 

## Langkah Eksploitasi

1. Masuk ke halaman lab yang disediakan untuk memulai eksploitasi. Tambahkan `/robots.txt` di akhir URL lab untuk mengakses file `robots.txt`. Contoh URL: http://lab-url/robots.txt. Pada file robots.txt, perhatikan baris yang berisi kata `Disallow`. Biasanya, file ini mengungkapkan direktori atau path yang tidak ingin diindeks oleh mesin pencari, yang mungkin mencakup admin panel.
<img width="1366" height="410" alt="image" src="https://github.com/user-attachments/assets/9b46f58b-3ddc-469f-bbe8-dbd4c7a25dc6" />

2. Setelah mengetahui path admin dari file robots.txt, ganti `/robots.txt` dengan `/administrator-panel` di URL, misalnya: http://lab-url/administrator-panel. Hal ini akan mengarahkan kita ke panel admin.
<img width="2634" height="913" alt="image" src="https://github.com/user-attachments/assets/513ab28b-a41d-4d8d-aea5-05043272deee" />

3. Setelah berhasil mengakses panel admin, cari daftar pengguna yang terdaftar dan temukan pengguna dengan nama `Carlos`. Pilih dan hapus akun Carlos untuk menyelesaikan lab.
<img width="2589" height="972" alt="image" src="https://github.com/user-attachments/assets/0327f959-82bf-410b-bb84-d15320159643" />

### Catatan (Notes)

- Status: Berhasil
- Teknik: Menggunakan file robots.txt untuk menemukan path admin yang tidak terlindungi
- Payload: URL admin panel yang ditemukan setelah memeriksa robots.txt
- Alasan: Admin panel terungkap melalui file robots.txt yang seharusnya tidak mengungkapkan path admin secara publik
- Refleksi: Menyembunyikan informasi penting seperti path admin dari file robots.txt sangat penting untuk mencegah potensi eksploitasi, dan penting untuk memastikan bahwa akses admin dilindungi dengan baik.
