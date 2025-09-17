# Easter Egg

## Langkah Eksploitasi

1. Akses Halaman FTP di Juice Shop
   - Pertama, buka halaman FTP di aplikasi Juice Shop pada `http://localhost:3000/ftp`.
   - Pada halaman ini, kamu dapat melihat beberapa file yang tersedia untuk diakses, termasuk folder quarantine dan file lain seperti acquisitions.md, eastere.gg, legal.md, dan announcement_encrypted.md.
<img width="2879" height="768" alt="image" src="https://github.com/user-attachments/assets/36e0c367-67e9-4fec-a2be-f55b2cdff71d" />

2. Coba Akses File eastere.gg
   - Cobalah untuk mengakses file `eastere.gg` yang ada di dalam halaman FTP. Kamu akan mendapatkan error 403 yang menunjukkan bahwa hanya file dengan ekstensi .md dan .pdf yang diizinkan untuk diakses.
<img width="2400" height="973" alt="image" src="https://github.com/user-attachments/assets/fbbbe334-78a1-4423-8aac-a2dc75268a35" />

3. Manipulasi URL untuk Mengakses File yang Tidak Diperbolehkan
   - Setelah mendapatkan error, coba manipulasi URL dan ubah `eastere.gg` menjadi `http://localhost:3000/ftp/eastere.gg%2500.pdf`. Ini memungkinkan kamu untuk mengakses file yang terlarang.
   - Akses URL yang dimodifikasi dan file eastere.gg%00.pdf akan terunduh.
<img width="2588" height="339" alt="image" src="https://github.com/user-attachments/assets/25841663-28f8-4e7e-bbf0-49920fd32260" />

4. Buka File PDF yang Terunduh
   - Setelah mengunduh file tersebut, buka file PDF yang terunduh. Di dalam file tersebut, terdapat pesan tersembunyi yaitu `L2d1ci9xcmlmL25lci9mYi9zaGFhbC9ndXJsL3V2cS9uYS9ybmZncmUvcnR0L2p2Z3V2YS9ndXIvcm5mZ3JlL3J0dA==` yang mengarah ke petunjuk lebih lanjut dengan menggunakan Base64 encoding.
<img width="1880" height="851" alt="image" src="https://github.com/user-attachments/assets/da26ba5b-c824-42bc-b1f0-bf6ceeca6067" />

5. Dekode Base64 untuk Mengungkapkan Pesan Tersembunyi
   - Salin string Base64 yang ada pada file tersebut dan buka situs Base64 Decode untuk mendekodekannya. Disini kita mendapatkan `/gur/qrif/ner/fb/shaal/gurl/uvq/na/rnfgre/rtt/jvguva/gur/rnfgre/rtt`, gunakan situs ROT13.com untuk mendekode string ini.
<img width="1797" height="1477" alt="image" src="https://github.com/user-attachments/assets/1d5d5565-640b-4ea3-9872-61de2b7abca8" />

6. Dapatkan Pesan Tersembunyi Setelah ROT13
   - Setelah melakukan dekripsi ROT13, kamu akan mendapatkan pesan yang menyatakan bahwa para pengembang telah menyembunyikan sebuah "easter egg".
   - Pesan yang muncul akan memberikan petunjuk lebih lanjut, yaitu `/the/devs/are/so/funny/they/hid/an/easter/egg/within/the/easter/egg`
<img width="1650" height="1527" alt="image" src="https://github.com/user-attachments/assets/ec815d7f-3448-4db1-b52c-11a5c7094340" />

## CATATAN (NOTES)

- Status: Berhasil
- Teknik: Broken Access Control
Eksploitasi ini dilakukan dengan memanfaatkan kontrol akses yang lemah pada halaman FTP, yang memungkinkan manipulasi URL untuk mengakses file yang seharusnya terbatas.
- Alasan Keberhasilan:
Aplikasi tidak membatasi jenis file yang dapat diakses, dan manipulasi URL memungkinkan file yang tidak seharusnya diakses, seperti file dengan ekstensi yang dibatasi, untuk terbuka.
- Refleksi:
Untuk mencegah eksploitasi seperti ini, aplikasi harus memvalidasi dan membatasi jenis file yang dapat diakses oleh pengguna dan menggunakan teknik kontrol akses berbasis peran untuk mencegah akses yang tidak sah ke data sensitif atau file yang tidak seharusnya dibuka.



