# Admin Section

## Langkah Eksploitasi

1. Akses Halaman Admin di Juice Shop
   - Pertama, buka aplikasi Juice Shop pada `http://localhost:3000/#/profile`.
   - Pada menu akun pengguna, pastikan sedang login adalah `admin@juice-sh.op`.
<img width="859" height="641" alt="image" src="https://github.com/user-attachments/assets/682118a0-7637-4757-b549-297cf8889165" />

2. Periksa URL Admin di Halaman Dashboard
   - Dengan menggunakan alat pengembang di browser (Developer Tools), periksa elemen HTML untuk menemukan endpoint yang terkait dengan halaman admin.
   - Pada halaman dashboard, ditemukan path yang terkait dengan akses admin: `/administration`.
<img width="2879" height="1649" alt="image" src="https://github.com/user-attachments/assets/a9462a65-faf5-4a03-b665-4f25d91aa649" />

3. Menemukan dan Mengakses Halaman Admin
   - Berdasarkan analisis, ditemukan URL path admin pada main.js yang terlihat jelas. Akses langsung halaman admin dengan URL `http://localhost:3000/#/administration` 
<img width="2062" height="1496" alt="image" src="https://github.com/user-attachments/assets/7a42d770-9d73-44e4-a904-1e9abd704b1f" />

4. Akses Halaman Admin Tanpa Autentikasi
   - Ternyata, halaman admin dapat diakses meskipun pengguna yang login bukan admin. Hal ini menunjukkan adanya broken access control, karena seharusnya akses ke halaman admin harusnya dibatasi untuk pengguna dengan hak akses tertentu.
<img width="2860" height="1641" alt="image" src="https://github.com/user-attachments/assets/a7b9b163-e66d-40c1-b9cc-5a7f4d188340" />

### CATATAN (NOTES) 

- Status: Berhasil
- Teknik: Broken Access Control
Eksploitasi ini dilakukan dengan memanfaatkan kelemahan dalam kontrol akses aplikasi yang memungkinkan pengguna biasa mengakses halaman admin tanpa validasi akses.
- Alasan Keberhasilan:
Aplikasi Juice Shop tidak memiliki mekanisme kontrol akses yang membatasi pengguna dengan role tertentu untuk mengakses halaman admin. Hal ini memungkinkan pengguna dengan akses biasa untuk mengakses dan melihat data sensitif, seperti feedback pelanggan dan daftar pengguna terdaftar.
- Refleksi:
Untuk mencegah eksploitasi seperti ini, aplikasi harus memastikan bahwa setiap halaman atau fitur yang membutuhkan akses terbatas dilindungi dengan kontrol akses yang tepat, seperti:
a. Memastikan validasi role pengguna sebelum mengizinkan akses ke halaman atau data sensitif.
b. Menggunakan kontrol berbasis peran (role-based access control) untuk membatasi akses berdasarkan hak pengguna.
c. Memastikan bahwa URL untuk admin dan fitur sensitif lainnya tidak mudah diakses atau ditebak.

