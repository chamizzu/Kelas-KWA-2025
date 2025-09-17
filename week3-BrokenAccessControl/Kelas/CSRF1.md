# CSRF

## Langkah Eksploitasi

1. Akses Halaman Profil Pengguna
   - Pertama, buka aplikasi Juice Shop pada http://localhost:3000/profile.
   - Pada halaman ini, kamu akan melihat profil pengguna dengan opsi untuk mengubah username dan mengupload foto profil.
   - Disini kita akan mencoba mengubah `username` akun JuiceShop
<img width="2879" height="1359" alt="image" src="https://github.com/user-attachments/assets/3139a663-2fb8-4ce5-a146-31572be899e5" />

2. Memeriksa Request HTTP Menggunakan Burp Suite
   - Gunakan Burp Suite untuk memeriksa request HTTP yang dikirimkan saat kamu melakukan perubahan pada profil pengguna.
   - Di dalam Burp Suite, pastikan kamu mengaktifkan intercept untuk menangkap request POST yang dikirim ke http://localhost:3000/profile.
   - Request yang terdeteksi di Burp Suite menunjukkan parameter username=mizu yang dikirim dalam body request.
<img width="2201" height="1417" alt="image" src="https://github.com/user-attachments/assets/21d0d464-3055-4e5d-bb17-5bb0bf14bb91" />

3. Membuat Halaman CSRF
   - Untuk mengeksploitasi CSRF, buat sebuah file HTML dengan form yang secara otomatis mengirimkan request POST ke URL `http://localhost:3000/profile`.
   - Form tersebut menggunakan metode POST dan menyertakan parameter username yang diubah menjadi nilai baru, misalnya "HelloAkuAisyah".
   - Berikut adalah kode HTML punyaku untuk melakukan CSRF:
     ```<html>
<body>
  <form action="http://localhost:3000/profile" method="POST">
    <input type="hidden" name="username" value="HelloAkuAisyah" />
  </form>
  <script>document.forms[0].submit();</script>
</body>
</html>
``` 
<img width="1237" height="458" alt="image" src="https://github.com/user-attachments/assets/23e008a0-931b-4006-8d90-e51e7b57a24f" />

  - Jalankan server Python pada port 8000 untuk meng-host file HTML ini menggunakan perintah: `python -m http.server 8000`
  - Setelah server dijalankan, buka file csrf2.html di browser. Ini akan mengirimkan request secara otomatis ke aplikasi Juice Shop.
  - Setelah request CSRF terkirim, kembali ke halaman profil pengguna di Juice Shop. Username pengguna akan berubah sesuai dengan nilai yang dikirimkan melalui CSRF.
<img width="1137" height="269" alt="image" src="https://github.com/user-attachments/assets/521f8bbf-c0b5-42d0-83cb-c49c6b8e32c9" />
<img width="2879" height="1612" alt="image" src="https://github.com/user-attachments/assets/c66f7f30-2be8-45a7-8b16-59b5cd70e2fa" />

### CATATAN (NOTES)

- Status: Berhasil
- Teknik: CSRF (Cross-Site Request Forgery)
Teknik ini digunakan untuk mengeksploitasi aplikasi yang tidak memvalidasi permintaan yang datang dari origin yang tidak sah, memungkinkan pelaku untuk memanipulasi data profil pengguna tanpa persetujuan mereka.
- Payload:
Payload yang digunakan berupa form POST yang disisipkan di halaman CSRF. Form ini mengirimkan parameter username yang telah diubah menjadi `HelloAkuAisyah`, yang kemudian memanipulasi profil pengguna.
- Alasan Keberhasilan:
Aplikasi Juice Shop tidak dilengkapi dengan perlindungan CSRF, seperti token CSRF yang biasanya digunakan untuk memvalidasi bahwa permintaan berasal dari pengguna yang sah. Selain itu, aplikasi juga tidak membatasi perubahan profil pengguna berdasarkan origin permintaan, sehingga eksploitasi ini menjadi mungkin.
- Refleksi:
Pastikan untuk selalu melindungi aplikasi dengan token CSRF untuk mencegah eksploitasi seperti ini. Gunakan teknik validasi yang tepat untuk memastikan hanya pengguna yang sah yang dapat melakukan perubahan.
