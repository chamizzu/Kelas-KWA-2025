# Product Tampering

## Langkah Eksploitasi

1. Akses Halaman Produk
   - Pertama, seacrh OWASP SSL Advanced Forensic Tool (O-Saft) di aplikasi Juice Shop.
   - Pada halaman produk ini, kamu dapat melihat deskripsi produk, termasuk href link yang menuju halaman luar.
<img width="2879" height="1528" alt="image" src="https://github.com/user-attachments/assets/fec4a8fa-699f-4291-9682-1dba1b43ae9e" />

2. Identifikasi URL di Deskripsi Produk
   - Pada bagian deskripsi produk, terdapat link yang menuju ke halaman luar, misalnya link yang menunjuk ke OWASP Slack (https://owasp.slack.com).
   - Catatan: URL ini berfungsi sebagai bagian dari deskripsi produk, yang bisa jadi sasaran eksploitasi
<img width="2877" height="1618" alt="image" src="https://github.com/user-attachments/assets/6d18861a-dffa-4a6a-b656-f4a97c08c9d7" />

3. Masuk ke Halaman Accounting untuk Memperbarui Produk
   - Setelah memodifikasi link, lanjutkan dengan mengakses bagian Accounting dalam aplikasi Juice Shop.
   - Di sini, kamu dapat melihat produk-produk yang tersedia beserta harga dan kuantitasnya.
<img width="2879" height="1625" alt="image" src="https://github.com/user-attachments/assets/c017553d-3bae-45dc-b2f6-79c7843fbfbf" />

4. Update Harga dan Kuantitas Produk
   - Cari produk OWASP SSL Advanced Forensic Tool (O-Saft) di bagian Accounting.
   - Disini aku memperbarui harga produk menjadi 24.19 dan kuantitas menjadi 19.
   - Klik Save untuk menyimpan perubahan tersebut.
<img width="1155" height="145" alt="image" src="https://github.com/user-attachments/assets/aadb18d7-8d2f-45ea-a2d0-2917815c9893" />

5. Ubah Metode dari GET ke PUT:
   - Setelah itu, tentunya kita mengirim request dari update-an harga produk yang baru saja kita lakukan ke Repeater
   - Untuk memperbarui informasi produk (seperti mengubah link di deskripsi), kita perlu mengubah metode dari `GET menjadi PUT`. PUT digunakan untuk mengupdate data di server, yang memungkinkan kita mengganti konten dari produk yang ada.
<img width="757" height="692" alt="image" src="https://github.com/user-attachments/assets/3bf84f7c-55ee-4982-8d1d-b150a34c5605" />

6. Masukkan Link Baru di Deskripsi
   -  Setelah mengubah metode menjadi PUT, perbarui link di dalam deskripsi produk dengan link yang baru. Ubah dari:
     ```html
     <a href="https://www.owasp.org">More...</a>
     ```
     Menjadi:
     ```html
     <a href="https://owasp.slack.com" target="_blank">More...</a>
     ```
<img width="2217" height="1626" alt="image" src="https://github.com/user-attachments/assets/cd44bd02-1713-457c-a8dc-670b5fa8b6fa" />

7. Verifikasi Perubahan
   - Setelah mengirimkan request PUT, kamu dapat memverifikasi perubahan dengan membuka produk di web aplikasi dan memeriksa deskripsi produk untuk memastikan link telah berubah sesuai dengan yang diinginkan.
   - Link di deskripsi produk akan mengarah ke https://owasp.slack.com.
<img width="1990" height="1317" alt="image" src="https://github.com/user-attachments/assets/66c2f03a-1cfe-41e5-af83-08afb9d36525" />


### **Catatan (Notes)**

- **Status:** Berhasil
- **Teknik:** Broken Access Control - Product Tampering
   - Teknik ini memanfaatkan kerentanannya pada aplikasi yang memungkinkan manipulasi elemen halaman yang seharusnya tidak dapat diubah oleh pengguna, seperti **URL** dalam deskripsi produk. Pengguna dapat mengubah konten produk tanpa otorisasi yang tepat.
  
- **Alasan Keberhasilan:**
   1. Aplikasi tidak memvalidasi atau membatasi perubahan elemen seperti link di deskripsi produk, yang memungkinkan manipulasi oleh pengguna yang tidak sah.
   2. Metode request diubah dari **GET** menjadi **PUT**, yang memungkinkan pengguna untuk mengubah informasi produk yang ada tanpa pembatasan.
   3. Link di dalam deskripsi produk diubah untuk mengarahkan ke **https://owasp.slack.com** (misalnya) menggunakan request **PUT**, yang kemudian berhasil diterima dan diproses oleh server.

- **Payload yang Digunakan:**
   Berikut adalah contoh payload yang digunakan untuk mengeksploitasi kerentanannya dalam **PUT request**:
   ```json
   {
     "id": 9,
     "name": "OWASP SSL Advanced Forensic Tool (O-Saft)",
     "description": "<a href='https://owasp.slack.com' target='_blank'>More...</a>",
     "price": 24.19,
     "deluxePrice": 0.01,
     "image": "orange_juice.jpg"
   }

- **Refleksi:**
  1. Untuk mencegah eksploitasi seperti ini, disarankan untuk menambahkan kontrol akses berbasis peran (RBAC) untuk memastikan hanya pengguna yang sah yang dapat mengakses dan mengelola produk mereka.
  2. Validasi parameter dalam request PUT harus dilakukan di sisi server untuk memastikan data yang dikirim valid dan sesuai dengan otorisasi pengguna yang aktif.
  3. Server harus memeriksa semua parameter terkait data sensitif (seperti deskripsi, harga, dan link) sebelum melakukan operasi yang dapat memanipulasi konten atau informasi produk.
















