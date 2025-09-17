# Forged Feedback

## Langkah Eksploitasi

1. Akses Halaman Umpan Balik Pengguna
   - Pertama, buka aplikasi Juice Shop dan tidak perlu login pada halaman Feedback di URL `http://localhost:3000/#/contact`.
   - Pada halaman ini, kamu akan melihat form untuk memberikan umpan balik yang mencakup kolom untuk Author, Comment, Rating, dan CAPTCHA
<img width="2879" height="1492" alt="image" src="https://github.com/user-attachments/assets/9a179245-f0b8-4759-a659-5c2659da1968" />

2. Isi Formulir Umpan Balik dan Kirim
   - Coba kirimkan feedback dengan mengisi kolom "Comment", tanpa login, dan klik submit.
   - Feedback ini akan dikirimkan sebagai anonymous.
<img width="2879" height="1476" alt="image" src="https://github.com/user-attachments/assets/6da74b6e-31f6-484e-8824-4a8a8e7b1c3e" />

3. Periksa Request Menggunakan Burp Suite
   - Setelah mengirimkan Comment, buka Burp Suite dan aktifkan intercept untuk menangkap request POST yang dikirimkan ke server.
   - Pada tahap ini, di Burp Suite, kamu tidak melihat idUser di request body.
<img width="2182" height="1234" alt="image" src="https://github.com/user-attachments/assets/fcff07fc-197f-4f38-a2bc-20b6a6f950f7" />

4. Modifikasi Formulir Menggunakan Developer Tools
   - Klik kanan pada elemen form dan pilih Inspect atau tekan F12 untuk membuka Developer Tools.
   - Di dalam tab Elements, temukan elemen <input> yang bertanggung jawab untuk memasukkan idUser. Formulir ini mungkin memiliki elemen yang tersembunyi dengan atribut `hidden`.
   - Temukan elemen input dengan atribut hidden yang memiliki id="userId".
   - Hapus atribut hidden agar form ini bisa menerima input untuk User ID
<img width="2879" height="1560" alt="image" src="https://github.com/user-attachments/assets/78e224f3-1ad0-4922-bd89-738aa1cfdcb6" />

5. Isi User ID di Juice Shop
   - Setelah menghapus atribut hidden, halaman Customer Feedback di Juice Shop akan memungkinkan kita untuk mengisi kolom User ID.
   - Isi User ID sesuai dengan yang diinginkan, misalnya "mizu".
<img width="2879" height="1401" alt="image" src="https://github.com/user-attachments/assets/d9d0e46f-330a-43e2-a826-11832e4d0663" />

6. Cek di Burp Suite (User ID Muncul)
   - Kembali ke Burp Suite untuk memeriksa apakah User ID sekarang muncul dalam request POST.
   - Setelah feedback dikirim dengan User ID, kita akan melihat bahwa User ID kini muncul di dalam request
<img width="1892" height="1363" alt="image" src="https://github.com/user-attachments/assets/2d216ccb-ccc6-481b-b67b-40252f219488" />

## Catatan (Notes)

- Status: Berhasil
- Teknik: Broken Access Control
Teknik ini memanfaatkan kontrol akses yang lemah pada aplikasi, yang memungkinkan pengguna yang tidak berwenang untuk mengakses dan memodifikasi elemen formulir (seperti User ID) yang seharusnya terbatas hanya untuk pengguna yang sudah terautentikasi atau admin.
- Alasan Keberhasilan:
  1. Aplikasi tidak membatasi dengan benar akses untuk memodifikasi elemen form yang seharusnya dilindungi, seperti User ID. Meskipun pengguna tidak login, aplikasi tetap memberikan akses untuk mengirim feedback.
  2. Ketika elemen hidden untuk User ID dihapus menggunakan Developer Tools, kita dapat memodifikasi data yang dikirimkan oleh form, termasuk menyertakan User ID yang sebelumnya tidak ada.
  3. User ID yang dikirimkan melalui request POST muncul di Burp Suite, menunjukkan bahwa eksploitasi berhasil dilakukan setelah memodifikasi elemen di sisi klien.
- Refleksi:
  1. Untuk mencegah eksploitasi seperti ini, disarankan untuk menggunakan kontrol akses berbasis peran (role-based access control atau RBAC) guna membatasi akses admin ke pengguna yang sah.
  2. Pastikan bahwa hanya pengguna dengan hak akses admin yang dapat mengelola data sensitif seperti feedback pelanggan atau informasi yang terkait dengan pengguna.
  3. Selain itu, validasi sisi server harus diterapkan untuk memverifikasi keabsahan User ID yang dikirimkan, dan pemeriksaan akses harus dilakukan sebelum data diproses.




