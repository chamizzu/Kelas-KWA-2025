# Forged Review

## Langkah Eksploitasi

1. Akses Halaman Produk
   - Pertama, buka aplikasi Juice Shop dan pilih produk yang ingin diberikan review.
   - Coba kirimkan review dengan menulis komentar "aisa suka cheesecake & matcha".
   - Setelah review dikirimkan, aplikasi akan mengirimkan review tanpa validasi apakah pengguna tersebut adalah pemilik username yang dimasukkan dalam request.
<img width="1645" height="1531" alt="image" src="https://github.com/user-attachments/assets/1a18f31a-fba8-4711-95c6-dcc031ac7f78" />

2. Periksa Request Menggunakan Burp Suite
   - Setelah mengirimkan review, buka Burp Suite dan aktifkan intercept untuk menangkap request POST yang dikirimkan ke server.
   - Pada request POST ini, kita menemukan parameter author yang berisi nama pengguna yang memasukkan review, yang terlihat tidak divalidasi oleh server.
<img width="2195" height="1099" alt="image" src="https://github.com/user-attachments/assets/78a2a780-fbf8-461b-ba1a-4123bce11d5e" />

3. Modifikasi Parameter author
   - Modifikasi request dengan mengubah parameter author pada request body untuk menyertakan nama pengguna lain, misalnya mengganti author menjadi `bender@juice-sh.op`.
   - Catatan: Hal ini memungkinkan review diposting seolah-olah ditulis oleh pengguna lain.
<img width="2200" height="1438" alt="image" src="https://github.com/user-attachments/assets/55faff5b-0e1f-4291-9b6f-4d85a39558e4" />

4. Verifikasi Review yang Diposting
   - Setelah mengirimkan request yang dimodifikasi, buka aplikasi Juice Shop dan periksa apakah review tersebut sekarang muncul di bawah nama pengguna yang baru.
<img width="1510" height="1578" alt="image" src="https://github.com/user-attachments/assets/2841d09b-e43b-4715-912d-0d7a3abb3b5d" />

### Catatan (Notes)

- Status: Berhasil
- Teknik: Broken Access Control
Teknik ini memanfaatkan kontrol akses yang lemah pada aplikasi, yang memungkinkan pengguna yang tidak terautentikasi untuk mengakses dan mengubah elemen formulir (seperti author) yang seharusnya hanya bisa diubah oleh pengguna yang sudah terautentikasi.
- Payload yang Digunakan:
  1. Berikut adalah contoh payload yang digunakan untuk mengeksploitasi kerentanannya:
  2. message: Isi review yang dimasukkan oleh pengguna (contoh: "aisa suka cheesecake & matcha").
  3. author: Nama pengguna yang dimodifikasi, dalam hal ini "bender@juice-sh.op", yang mengubah pengirim review menjadi pengguna lain.
```json
{
  "message": "aisa suka cheesecake & matcha",
  "author": "bender@juice-sh.op"
}
```
- Alasan Keberhasilan:
  1. Aplikasi tidak memvalidasi dengan benar bahwa parameter author dalam request merupakan pengguna yang sedang terautentikasi, sehingga memungkinkan pengubahan nama pengguna yang tidak sah.
  2. Pengguna dapat memodifikasi request dan mengirimkan data yang seharusnya dibatasi, mengakibatkan review yang diposting dengan nama pengguna yang dimodifikasi.
  3. Setelah request dikirimkan kembali, review berhasil diposting dengan nama pengguna yang dimodifikasi, mengindikasikan kegagalan dalam kontrol akses.
- Refleksi:
  1. Untuk mencegah eksploitasi ini, disarankan untuk menerapkan kontrol akses berbasis peran (RBAC) yang memastikan hanya pengguna yang sah yang dapat mengubah atau memodifikasi review yang diajukan.
  2. Pastikan bahwa server memvalidasi identitas pengguna sebelum memproses data sensitif seperti nama pengirim review, untuk mencegah penyalahgunaan dan manipulasi data.
  3. Periksa data yang dikirim dari sisi klien untuk memastikan bahwa aplikasi tidak mempercayai data yang dimodifikasi oleh pengguna.


