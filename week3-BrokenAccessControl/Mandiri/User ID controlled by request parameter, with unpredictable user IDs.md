# User ID controlled by request parameter, with unpredictable user IDs - PortSwigger
https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-unpredictable-user-ids

## Langkah Eksploitasi

1. Masuk ke web menggunakan kredensial yang diberikan: `wiener:peter`. Setelah itu kia harus temukan postingan blog yang dibuat oleh Carlos. Klik pada postingan yang dibuat oleh Carlos dan perhatikan URL-nya. 
<img width="1869" height="1601" alt="image" src="https://github.com/user-attachments/assets/f505145c-ad28-4603-84b2-c9c5b27f4d7f" />

2. URL tersebut akan mengandung GUID (user ID) milik Carlos. Salin dan simpan user ID (GUID) yang terdapat dalam URL tersebut
<img width="2331" height="540" alt="image" src="https://github.com/user-attachments/assets/a3ca69ab-76ad-42f5-a43a-465bb04e1f2c" />

3. Setelah mencatat user ID Carlos, login dengan kredensial yang disediakan dan buka halaman akun Anda. Ubah Parameter "id" ke User ID Carlos yaitu `userId=8a1c7e4e-54e0-41bd-82f7-1c47c40502b5`
<img width="1963" height="1337" alt="image" src="https://github.com/user-attachments/assets/654694e0-f299-4795-a4ec-8e04b6ebc307" />
<img width="2363" height="439" alt="image" src="https://github.com/user-attachments/assets/b63eb07d-3cd9-4325-971b-b51ebda5b7fa" />

4. Setelah mengubah parameter id dan mengakses data Carlos, ambil API key yang ditampilkan dan kirimkan API key tersebut untuk menyelesaikan lab
`nFMiKd2VHuUpkRDhS3e7801YlQ4ytv27`
<img width="2388" height="1217" alt="image" src="https://github.com/user-attachments/assets/49df57bf-e2a3-4ef5-9036-8cd49f1a1d0e" />
<img width="2428" height="681" alt="image" src="https://github.com/user-attachments/assets/9bcd2b71-c5ed-4532-97d2-6446f559ec92" />

### Catatan (Notes)

- Status: Berhasil
- Teknik: Manipulasi parameter ID untuk mengakses data pengguna lain
- Payload: Mengubah parameter id ke GUID Carlos untuk mengakses data sensitif
- Alasan: Kerentanan terjadi karena sistem menggunakan GUID yang dapat diakses tanpa kontrol akses yang tepat.
- Refleksi: Lab ini menunjukkan pentingnya pengamanan terhadap pengidentifikasi unik pengguna (seperti GUID) dan perlunya kontrol akses horizontal yang kuat untuk mencegah eskalasi privilese.







