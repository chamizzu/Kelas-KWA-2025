# Manipulate Basket

## Langkah Eksploitasi

1. Akses Keranjang Pribadi
   - Pertama, tambahkan produk ke dalam keranjang pribadi untuk mengamati struktur request HTTP dan parameter yang terlibat.
   - Setiap operasi keranjang (tambah, ubah) direferensikan dengan ID keranjang yang spesifik, yang terikat dengan pengguna.

2. Identifikasi Parameter Keranjang di Request
   - Gunakan Burp Suite untuk menangkap request HTTP yang dikirimkan saat produk ditambahkan ke dalam keranjang.
   - Catatan: Parameter BasketId termasuk dalam request body, yang mengindikasikan kemungkinan masalah IDOR (Insecure Direct Object Reference), di mana ID keranjang dapat dimanipulasi.
<img width="2202" height="1477" alt="image" src="https://github.com/user-attachments/assets/8e14aa51-510c-4143-ab6e-693bf5a7aada" />

3. Manipulasi Basket ID
   - Ubah parameter BasketId di request yang telah diintersepsi dengan mengganti ID keranjang milik pengguna lain untuk menguji potensi masalah IDOR.
   - Pada gambar pertama, jika hanya ada satu ID keranjang yang digunakan `BasketId: "5"`, aplikasi merespons dengan error karena ID tersebut tidak valid untuk operasi.
<img width="2190" height="1335" alt="image" src="https://github.com/user-attachments/assets/4688ae97-c20d-45af-812f-77571cdce065" />

4. Melewati Pengecekan Keamanan dengan Double Parameter Injection
   - Coba menggandakan parameter BasketId di request body, di mana satu ID adalah ID yang valid dan satu lagi adalah ID yang dimodifikasi.
   - Pada gambar kedua, kita melihat request yang berisi dua BasketId: satu yang valid `BasketId: "5"` dan satu yang dimodifikasi `BasketId: "2"`.
   - Catatan: Server hanya memeriksa BasketId pertama untuk pengecekan kontrol akses, namun menggunakan BasketId kedua untuk operasi, yang berhasil menambah produk ke keranjang pengguna lain.
<img width="2192" height="1344" alt="image" src="https://github.com/user-attachments/assets/6d85e190-f0ad-4c0d-9b22-27533a594006" />

### **Catatan (Notes)**

- **Status:** Berhasil
- **Teknik:** IDOR (Insecure Direct Object Reference)
   - Teknik ini memanfaatkan kerentanannya pada aplikasi yang memungkinkan pengguna mengakses atau mengubah objek yang tidak seharusnya diakses, dalam hal ini `BasketId`, yang seharusnya hanya dapat diakses oleh pengguna yang memiliki keranjang tersebut.
- **Alasan Keberhasilan:**
   1. Aplikasi tidak memvalidasi dengan benar bahwa `BasketId` yang digunakan dalam request adalah milik pengguna yang sedang aktif, yang memungkinkan manipulasi ID keranjang untuk menambah produk ke keranjang orang lain.
   2. Server hanya memeriksa **`BasketId` pertama** untuk pengecekan akses tetapi menggunakan **`BasketId` kedua** untuk operasi, yang memungkinkan eksploitasi ini.
   3. Menggandakan parameter `BasketId` memungkinkan server memproses ID yang dimodifikasi dan berhasil menambah produk ke keranjang yang salah.
- **Payload yang Digunakan:**
   Berikut adalah contoh payload yang digunakan untuk mengeksploitasi kerentanannya:
   ```json
   {
     "ProductId": 24,
     "BasketId": "2",
     "BasketId": "5",
     "quantity": 1
   }
- **Refleksi:**
  1. Untuk mencegah eksploitasi seperti ini, disarankan untuk menambahkan kontrol akses berbasis peran (RBAC) untuk memastikan hanya pengguna yang sah yang dapat mengakses dan mengelola keranjang mereka.
  2. Validasi parameter BasketId harus dilakukan di sisi server untuk memastikan ID keranjang yang digunakan dalam request sesuai dengan yang dimiliki oleh pengguna yang sedang aktif.
  3. Server harus memeriksa semua parameter terkait akses data (seperti BasketId) sebelum melakukan operasi sensitif seperti menambah atau mengubah item dalam keranjang.




