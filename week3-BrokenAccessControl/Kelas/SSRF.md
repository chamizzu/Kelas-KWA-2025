# SSRF

## Langkah Eksploitasi

1. Akses Halaman FTP di Aplikasi Juice Shop
   - URL: Akses halaman FTP di aplikasi OWASP Juice Shop dengan membuka `http://localhost:3000/#/ftp` di browser.
   - Pada halaman FTP ini, kamu akan melihat beberapa file yang bisa dipilih dan dianalisis.
<img width="2879" height="718" alt="image" src="https://github.com/user-attachments/assets/6c57deef-f7b2-471b-a547-226ee1b4e208" />

2. Pilih File dari Folder Quarantine yang Sesuai dengan Sistem Operasi Laptop
   - Di halaman /ftp pada aplikasi Juice Shop, pilih file yang sesuai dengan sistem operasi laptop kamu.
   - Disini karena aku pengguna laptop Windows, maka aku memilih file juicy_malware_windows_64.exe dari folder Quarantine.
   - Nanti setelah mengklik file tersebut, akan otomatis terdownload file nya.
<img width="2738" height="569" alt="image" src="https://github.com/user-attachments/assets/5863978f-8d67-4fef-bbd8-f1483c14649a" />
<img width="2796" height="643" alt="image" src="https://github.com/user-attachments/assets/fd792e82-8eaf-4bf5-9b86-b6c196a405cc" />

3. Unduh File Menggunakan Perintah curl di Terminal
   - Setelah memilih file juicy_malware_windows_64.exe, unduh file tersebut dengan menggunakan terminal.
   - Jalankan perintah curl untuk mengunduh file malware:
     `curl -LO "https://github.com/juice-shop/juicy-malware/raw/master/juicy_malware_windows_64.exe"`
   - Periksa apakah file berhasil diunduh dengan memeriksa ukuran file di direktori lokal kamu.
<img width="2372" height="286" alt="image" src="https://github.com/user-attachments/assets/6d0b509c-dd6f-4d47-9bf3-6719ebc41991" />

4. Analisis File Malware Menggunakan Notepad++
   - Setelah file diunduh, buka file juicy_malware_windows_64.exe menggunakan Notepad++ dengan plugin Hex-Editor.
   - Di Notepad++, pilih Plugins > Hex-Editor > View in Hex untuk melihat file dalam format biner (hexadecimal).
   - Cari string atau URL yang terkait dengan localhost atau server-side, disini kita menemukan URL yang berisi parameter kunci yang digunakan untuk eksploitasi SSRF. `http://localhost:3000/solve/challenges/server-side?key=tRy_H4rd3r_n0thIng_iS_Imp0ssibl3`
<img width="2879" height="1216" alt="image" src="https://github.com/user-attachments/assets/4752e0e0-692b-4b46-a031-7ed3f1ab84ff" />

5. Selanjutnya kita kembali membuka web JuiceShop nya, dan mengganti profile nya dengan Image URL yang sudah kita temukan. Dapat dilihat kita sudah berhasil menyelesaikan soal untuk eksploitasi SSRF
<img width="2363" height="1617" alt="image" src="https://github.com/user-attachments/assets/0ae54d08-f672-445b-89d8-6c18d779b21a" />
<img width="2879" height="616" alt="image" src="https://github.com/user-attachments/assets/5046a50b-c401-4c11-96a5-aaf5f5e3c3ec" />

### CATATAN (NOTES)

- Status: Berhasil
Exploit SSRF berhasil dilakukan dengan menemukan URL tersembunyi yang mengarah ke localhost:3000.
- Teknik: Exploit SSRF dengan mencari URL tersembunyi dalam file malware
Teknik SSRF dieksploitasi dengan menemukan URL yang berisi parameter kunci di dalam file juicy_malware_windows_64.exe.
- Payload: URL http://localhost:3000/solve/challenges/server-side?key=tRy_H4rd3r_n0thIng_iS_Imp0ssibl3
URL ini memberikan akses ke tantangan dalam aplikasi OWASP Juice Shop.
- Alasan Keberhasilan: Aplikasi tidak memvalidasi atau membatasi permintaan dari server lokal (localhost), memungkinkan eksploitasi SSRF.
- Refleksi: Penting untuk membatasi akses ke server internal dan memvalidasi request yang masuk untuk menghindari SSRF. Implementasikan kontrol akses yang ketat dan gunakan WAF (Web Application Firewall) untuk menghindari serangan SSRF.


