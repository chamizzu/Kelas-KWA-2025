# No Sql Injection

## Langkah Eksploitasi

https://play.picoctf.org/practice/challenge/443?page=1&search=injection 

<img width="1240" height="780" alt="Screenshot 2025-09-10 202150" src="https://github.com/user-attachments/assets/7f649e99-01ff-4283-bf3c-43e195557ad4" />

1. Langkah awal adalah memahami bagaimana proses login bekerja. Dengan memasukkan kredensial standar (misalnya, email: admin, password: ****) dan mencoba login, aplikasi merespons dengan pesan "Invalid credentials".
<img width="1117" height="971" alt="Screenshot 2025-09-10 202912" src="https://github.com/user-attachments/assets/f01616b5-0b8b-40bf-9a5a-3c9de4b5934e" />

2. Data login yang sudah direkam tadi dipindahkan ke alat (Burp Repeater) yang memungkinkan pengiriman ulang data yang sudah diubah. Isi dari kolom email dan password diubah dengan sebuah perintah khusus: `{"email":"{\"$ne\":\"null\"}","password":"{\"$ne\": \"null\"}"}`. Perintah ini meminta database untuk mencari entri pengguna mana saja yang kolom email dan password-nya tidak kosong, tanpa perlu mencocokkan isinya.
<img width="2275" height="914" alt="Screenshot 2025-09-10 203055" src="https://github.com/user-attachments/assets/2bac800a-420e-44b2-a155-176a1fc246ef" />

3. Selanjutnya, server mengirimkan respons yang menyatakan sukses dan menyertakan sebuah kode akses panjang yang disebut token. Kode yang disalin tadi dimasukkan ke dalam sebuah alat penerjemah (dekoder) Base64. Alat tersebut mengubah kode kembali ke bentuk teks aslinya, yang ternyata adalah flag yang dicari: `picoCTF{jBhD2y7XoNzPv_1YXS9Ew5qL0ul6pasql_injection_25ba4de1}`.
<img width="1210" height="969" alt="Screenshot 2025-09-10 203223" src="https://github.com/user-attachments/assets/e3159061-8c2f-4ca5-a96e-9730afcc1d8c" />


## CATATAN

a. Hasil: Berhasil
b. Alasan:
c. Refleksi:
