# User ID controlled by request parameter - PortSwigger
https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter

## Langkah Eksploitasi

1. Masuk ke aplikasi menggunakan kredensial yang diberikan: `wiener:peter`.
<img width="2434" height="1247" alt="image" src="https://github.com/user-attachments/assets/9b89ac70-819a-4489-aba6-f501f5475f49" />

2. Setelah login, buka halaman akun wiener. Perhatikan bahwa URL mengandung parameter id yang berisi username wiener yaitu `API WIENER  QhSA84KL8WtJcipLHVPzZl7x6H009isr`
<img width="2469" height="1226" alt="image" src="https://github.com/user-attachments/assets/852d47c8-e0b0-4b44-98b5-cb1fbbda1540" />

3. Di Burp Repeater, ubah parameter id dalam permintaan menjadi carlos untuk mengakses data pengguna Carlos. Setelah mengubah parameter id, ambil API key milik Carlos dari respon dan kirimkan sebagai solusi untuk menyelesaikan lab, kita dapat menemukan API Carlos adalah `NVibRqYn31JLKBcBsqOnh21eKd4HZ4KM`
<img width="1620" height="1291" alt="image" src="https://github.com/user-attachments/assets/79f9287e-4912-4588-b894-c3ed197aff62" />
<img width="1324" height="576" alt="image" src="https://github.com/user-attachments/assets/4bbb3f7c-4794-4821-808a-8e31953925e0" />
<img width="2631" height="1469" alt="image" src="https://github.com/user-attachments/assets/a82d7685-cdcf-467f-a649-02d0e87e0b64" />


### Catatan (Notes)

- Status: Berhasil
- Teknik: Manipulasi parameter ID dan analisis respon dengan Burp Suite
- Payload: Mengubah parameter id ke "carlos" untuk mengakses data milik pengguna Carlos
- Alasan: Kerentanannya terletak pada pengalihan akses yang tidak terbatas ke data pengguna lain.
- Refleksi: Lab ini menyoroti pentingnya pengamanan akses terhadap parameter ID untuk mencegah eskalasi privilese horizontal






