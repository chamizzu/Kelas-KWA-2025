# Unprotected admin functionality with unpredictable URL - PortSwigger
https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality-with-unpredictable-url

## Langkah Eksploitasi

1. Gunakan alat pengembang (Developer Tools) pada browser untuk memeriksa kode sumber halaman. Ini bisa dilakukan dengan klik kanan pada halaman dan memilih "Inspect" atau menekan tombol F12. Di dalam kode sumber atau JavaScript yang ada, cari informasi yang mengarah ke URL admin panel. Bisa kita lihat sudah ditemukan URL admin yaitu `admin-e2ea40`, maka salin dan buka URL tersebut untuk mengakses panel admin.
<img width="2879" height="1544" alt="image" src="https://github.com/user-attachments/assets/55ffabcc-66ff-4511-8411-15d819ad531c" />


2. Di dalam admin panel, cari daftar pengguna dan temukan pengguna dengan nama Carlos. Pilih untuk menghapus akun tersebut.
<img width="2544" height="909" alt="image" src="https://github.com/user-attachments/assets/3138d48f-7957-445d-8497-98eb736a7303" />


3. Tadaa!! Kita sudah berhasil menghapus akun `carlos`
<img width="2441" height="1149" alt="image" src="https://github.com/user-attachments/assets/6c63ccc3-64a6-472d-a464-b7354abff2fa" />


### NOTES

- Status: Berhasil
- Teknik: Penggunaan Developer Tools untuk memeriksa sumber halaman
- Payload: URL admin yang ditemukan dalam kode JavaScript
- Alasan: Admin panel tidak dilindungi dengan autentikasi yang memadai dan URL-nya terdeteksi melalui analisis sumber halaman.
- Refleksi: Penggunaan teknik ini menunjukkan pentingnya untuk selalu melindungi akses admin panel dan menyembunyikan URL serta memastikan aplikasi memiliki autentikasi yang kuat.

