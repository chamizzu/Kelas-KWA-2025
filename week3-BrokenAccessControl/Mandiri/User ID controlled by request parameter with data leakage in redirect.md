# User ID controlled by request parameter with data leakage in redirect - PortSwigger
https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-data-leakage-in-redirect

## Langkah Eksploitasi

1. Login dengan Kredensial yang Disediakan yaitu dengan masuk ke aplikasi menggunakan kredensial yang diberikan: `wiener:peter`.
<img width="2450" height="1150" alt="image" src="https://github.com/user-attachments/assets/6d71e252-ab67-4d1f-bccc-ff0af9e0ed04" />

2. Kirim permintaan yang berisi ID pengguna Anda ke Burp Repeater untuk memodifikasi parameter, disini kita dapat melihat terdapat permintaan `GET my-account?id=wiener`
<img width="2879" height="1383" alt="image" src="https://github.com/user-attachments/assets/3d94dc14-dd62-4388-ba11-82513a36954c" />

3. Di Burp Repeater, ubah parameter id dalam permintaan menjadi `carlos`, yang akan mengalihkan kita ke data pengguna Carlos.
<img width="2200" height="1359" alt="image" src="https://github.com/user-attachments/assets/b61c8e0d-f5cf-48af-b585-73a3465677d9" />

4. Meskipun kita dialihkan ke halaman utama, periksa isi respon yang diterima karena mengandung API key milik pengguna Carlos. Disini kita menemukan API Carlos yaitu:
   <p>Your username is: carlos</p>
                        <div>Your API Key is: yoSTGJhq3kTA8w8Flu9gRNpiew0lFbUL</div>
<img width="1094" height="1354" alt="image" src="https://github.com/user-attachments/assets/e9c42494-6372-4c4c-b39b-aa75f130ed5a" />

5. Yeay kita sudah berhasil mengerjalan lab dan menemukan API Carlos!!
<img width="2503" height="682" alt="image" src="https://github.com/user-attachments/assets/e879389a-9d90-475d-bdd1-d6a65b60a74e" />

### Catatan (Notes)

- Status: Berhasil / Gagal
- Teknik: Manipulasi parameter ID dan analisis respon dengan Burp Suite
- Payload: Mengubah parameter id untuk mengakses data milik pengguna Carlos
- Alasan: Kerentanannya terletak pada pengalihan yang mengungkapkan informasi sensitif (API key) dalam tubuh respon yang tidak dilindungi.
- Refleksi: Lab ini menunjukkan pentingnya pengamanan akses kontrol dan memastikan bahwa data sensitif tidak bocor melalui respons yang tidak aman.




