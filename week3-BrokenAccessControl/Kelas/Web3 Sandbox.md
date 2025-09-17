# Web3 Sandbox

## Langkah Eksploitasi

1. Buka Developer Tools dan Cek Sumber Kode
   - Buka Developer Tools di browser (tekan F12 atau klik kanan dan pilih "Inspect").
   - Di tab Sources, kamu bisa melihat file JavaScript yang dijalankan pada halaman tersebut, seperti main.js. Di sini, kamu bisa melihat adanya referensi ke path `web3-sandbox`, yang mengindikasikan adanya ruang untuk eksploitasi pada platform Web3.
<img width="2431" height="1342" alt="image" src="https://github.com/user-attachments/assets/6a0f326c-689b-4c19-851a-8b3871155baf" />

2. Akses Web3 Sandbox
   - Masukkan URL /web3-sandbox di browser `http://localhost:3000/web3-sandbox`.
   - Kamu akan dibawa ke halaman Web3 Sandbox yang menyediakan tempat untuk menulis dan meng-upload kontrak pintar
<img width="2879" height="1639" alt="image" src="https://github.com/user-attachments/assets/201365e0-58c2-4c8b-a29b-8f55301412f8" />

### CATATAN ( NOTES ):

- **Status:** Berhasil
- **Vulnerable Technique:** Web3 Sandbox Code Exposure  
   - Teknik ini memanfaatkan kerentanannya pada platform Web3 sandbox yang memungkinkan kontrak pintar yang tidak disengaja dideploy dan dieksploitasi.

- **Alasan Keberhasilan:**
   - Tidak ada pengamanan yang memadai untuk memastikan bahwa kontrak pintar yang ditulis dan dideploy di sandbox tidak diekspos ke publik atau pihak yang tidak berwenang.
   - Kurangnya validasi atau penyaringan terhadap kontrak yang dideploy memungkinkan kontrak untuk diakses dan dimanipulasi.
   - Tidak adanya pengamanan terhadap kontrak yang terupload mengakibatkan potensi eksploitasi yang tinggi.

- **Refleksi:**
   - Untuk mencegah eksploitasi seperti ini, platform Web3 sandbox harus memastikan bahwa tidak ada kontrak yang secara tidak sengaja dapat dideploy ke publik tanpa melalui pemeriksaan atau audit terlebih dahulu.
   - Kontrak pintar yang diupload harus memiliki pengamanan yang memadai dan validasi untuk mencegah adanya akses oleh pihak yang tidak berwenang.
   - Pengguna harus diberi peringatan atau pelatihan untuk memastikan tidak ada kontrak yang dideploy tanpa izin atau kesalahan konfigurasi.

- **Payload Contoh:**
   ```json
   {
     "contract": "HelloWorld",
     "method": "get",
     "result": "Hello Contracts"
   }



