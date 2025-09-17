# Five-Star Feedback

## Langkah Eksploitasi

1. Akses Halaman Admin di Juice Shop
   - Buka aplikasi Juice Shop pada URL `http://localhost:3000/#/administration` untuk mengakses halaman administrasi.
   - Di halaman ini, kamu bisa melihat daftar pengguna yang terdaftar dan umpan balik pelanggan yang diberikan untuk toko Juice Shop.
<img width="2879" height="1637" alt="image" src="https://github.com/user-attachments/assets/85852c15-3ca2-4f50-a566-7528364c9bc5" />

2. Menghapus Five-Star Feedback
   - Untuk menyelesaikan tantangan "Five-Star Feedback", kita perlu menghapus semua ulasan lima bintang dari halaman admin. Dengan mengeksploitasi kontrol akses yang tidak memadai, kita  bisa menghapus ulasan tersebut meskipun tidak memiliki hak akses admin.
<img width="2878" height="1230" alt="image" src="https://github.com/user-attachments/assets/243fc139-f547-4bd7-a6da-c4228509b05d" />

### CATATAN (NOTES)

- Status: Berhasil
- Teknik: Broken Access Control
Teknik ini memanfaatkan kontrol akses yang lemah pada aplikasi, yang memungkinkan pengguna yang tidak berwenang untuk menghapus umpan balik pelanggan.
- Alasan Keberhasilan:
Aplikasi tidak membatasi akses untuk mengelola umpan balik pelanggan dengan benar. Hal ini memungkinkan siapa saja yang dapat mengakses halaman admin untuk menghapus ulasan, termasuk yang memberikan rating tinggi.
- Refleksi:
Untuk mencegah eksploitasi seperti ini, Menggunakan kontrol akses berbasis peran (role-based access control) untuk membatasi hak akses admin ke pengguna yang sah dan memastikan bahwa hanya pengguna dengan hak akses admin yang dapat mengelola data sensitif seperti umpan balik pelanggan.

