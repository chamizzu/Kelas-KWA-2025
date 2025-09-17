# View Basket

## Langkah Eksploitasi

1. Buka Halaman Keranjang Belanja
   - Di halaman ini, kamu dapat melihat produk yang ditambahkan ke dalam keranjang, harga, dan kuantitasnya.
   - Buka Developer Tools di browser (tekan F12 atau klik kanan dan pilih "Inspect").
   - Pergi ke tab Application dan cari bagian Session Storage. Di situ, kamu akan menemukan nilai bid (Basket ID) dan itemTotal yang terkait dengan keranjang belanja pengguna.
   - Disini kita menemukan bahwa `bid` user kita saat ini dengan nilai `value : 2`
<img width="2879" height="1505" alt="image" src="https://github.com/user-attachments/assets/26a1664c-6105-4cb9-81af-b85b1c73a875" />

2. Manipulasi Session Storage
   - Ubah nilai bid menjadi ID lain yang mungkin terkait dengan keranjang pengguna lain. Contoh, ubah bid menjadi 5.
   - Setelah di reload, bisa kita lihat sudah berhasil mengubah keranjangnya
<img width="2879" height="1522" alt="image" src="https://github.com/user-attachments/assets/fefa6815-a7a1-4374-998a-b67eae33fc23" />

### **Catatan (Notes)**

- **Status:** Berhasil
- **Teknik:** Broken Access Control - View Basket
   - Teknik ini memanfaatkan kerentanannya pada aplikasi yang memungkinkan manipulasi **session storage** untuk mengakses objek (keranjang) yang tidak seharusnya diakses oleh pengguna lain.

- **Alasan Keberhasilan:**
   1. Aplikasi tidak memvalidasi **BasketId** (ID keranjang) dengan benar di sisi server, yang memungkinkan pengguna mengubah nilai **BasketId** di **session storage** dan mengakses keranjang orang lain.
   2. Tidak ada kontrol akses berbasis peran (RBAC) untuk memastikan bahwa pengguna hanya dapat mengakses keranjang mereka sendiri.
   3. Manipulasi **session storage** memungkinkan akses ke keranjang yang tidak dimiliki oleh pengguna aktif.

- **Payload yang Digunakan:**
   Berikut adalah contoh payload yang digunakan untuk mengeksploitasi kerentanannya dalam **Session Storage** manipulation:
   ```json
   {
     "bid": "5",  
     "itemTotal": "54.93000000000001"
   }

- **Refleksi:**
  1. Untuk mencegah eksploitasi seperti ini, aplikasi harus menerapkan kontrol akses berbasis peran (RBAC) untuk memastikan bahwa hanya pengguna yang sah yang dapat mengakses dan mengelola keranjang mereka.
  2. Pemeriksaan BasketId dan akses data lainnya harus dilakukan di sisi server untuk memastikan hanya pengguna yang sah yang dapat mengakses keranjang mereka.
  3. Session storage dan data terkait harus dienkripsi atau diobfuscate untuk mencegah manipulasi langsung oleh pengguna yang tidak sah.
