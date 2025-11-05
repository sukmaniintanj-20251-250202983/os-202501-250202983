
# Laporan Praktikum Minggu 4
Topik: Manajemen Proses dan User di Linux

---

## Identitas
- **Nama**  : Sukmani Intan Jumala
- **NIM**   : 250202983  
- **Kelas** : 1 IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menjelaskan konsep proses dan user dalam sistem operasi Linux.  
2. Menampilkan daftar proses yang sedang berjalan dan statusnya.  
3. Menggunakan perintah untuk membuat dan mengelola user.  
4. Menghentikan atau mengontrol proses tertentu menggunakan PID.  
5. Menjelaskan kaitan antara manajemen user dan keamanan sistem. 

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
lsmod | head
dmesg | head
```

## Langkah Praktikum
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).  
   - Pastikan Anda sudah login sebagai user non-root.  
   - Siapkan folder kerja:
     ```
     praktikum/week4-proses-user/
     ```

2. **Eksperimen 1 – Identitas User**
   Jalankan perintah berikut:
   ```bash
   whoami
   id
   groups
   ```
   - Jelaskan setiap output dan fungsinya.  
   - Buat user baru (jika memiliki izin sudo):
     ```bash
     sudo adduser praktikan
     sudo passwd praktikan
     ```
   - Uji login ke user baru.

3. **Eksperimen 2 – Monitoring Proses**
   Jalankan:
   ```bash
   ps aux | head -10
   top -n 1
   ```
   - Jelaskan kolom penting seperti PID, USER, %CPU, %MEM, COMMAND.  
   - Simpan tangkapan layar `top` ke:
     ```
     praktikum/week4-proses-user/screenshots/top.png
     ```

4. **Eksperimen 3 – Kontrol Proses**
   - Jalankan program latar belakang:
     ```bash
     sleep 1000 &
     ps aux | grep sleep
     ```
   - Catat PID proses `sleep`.  
   - Hentikan proses:
     ```bash
     kill <PID>
     ```
   - Pastikan proses telah berhenti dengan `ps aux | grep sleep`.

5. **Eksperimen 4 – Analisis Hierarki Proses**
   Jalankan:
   ```bash
   pstree -p | head -20
   ```
   - Amati hierarki proses dan identifikasi proses induk (`init`/`systemd`).  
   - Catat hasilnya dalam laporan.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 4 - Manajemen Proses & User"
   git push origin main
   ```
---


## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](<screenshots/eksperimen_1.png>)
![Screenshot hasil](<screenshots/eksperimen_2.png>)
![Screenshot hasil](<screenshots/eksperimen_3dan4.png>)

---

## D. Tugas & Quiz
### Tugas
1. Dokumentasikan hasil semua perintah dan jelaskan fungsi tiap perintah.  
2. Gambarkan hierarki proses dalam bentuk diagram pohon (`pstree`) di laporan.  
3. Jelaskan hubungan antara user management dan keamanan sistem Linux.  
4. Upload laporan ke repositori Git tepat waktu.

### Quiz
Tuliskan jawaban di bagian **Quiz** pada laporan:
1. Apa fungsi dari proses `init` atau `systemd` dalam sistem Linux?
   *jawaban*: `init` atau `systemd`berfungsi sebagai pengatur utama yang memastikan seluruh proses dan layanan dalam sistem linux berjalan dengan lancar dan terkoordinasi sejak komputer dinyalakan hingga dimatikan. Proses `init` atau `systemd` merupakan proses pertama yang dijalankan setelah kernel linux aktif dan memiliki PID 1 sebagai induk dari semua proses yang berfungsi untuk menyiapkan proses agar siap digunakan. Pada sistem lama digunakan `init`, sedangkan sistem modern memakai `systemd` yang lebih cepat dan efisien.
2. Apa perbedaan antara `kill` dan `killall`?
   *jawaban*: Perintah `kill` dan `killall` sama sama berfungsi untuk menghentikan proses yang sedang berjalan, tapi dengan cara yang berbeda. `kill` digunakan jika kita tahu nomor prosesnya (PID), jadi hanya menghentikan satu proses tertentu. Sementara `killall` bisa menghentikan semua proses yang memiliki nama program yang sama tanpa harus mencari PID nya. Jadi `kill` bekerja berdasarkan ID proses, sedangkan `killall` bekerja sebagai nama proses.
3. Mengapa user `root` memiliki hak istimewa di sistem Linux?
   *jawaban*: user `root` merupakan penggunan dengan hak istimewa tertinggi. Akun ini bisa melakukan apapun di sistem, seperti mengubah pengaturan penting, menghapus file sistem, memasang software atau mengatur hak akses pengguna lain. Alasan `root` memiliki hak istimewa adalah karena linux di desain dengan sistem keamanan berlapis, hanya pengguna tertentu (`root`) yang boleh melakukan tindakan yang bisa memengaruhi seluruh sistem. Dengan begitu, sistem jadi lebih aman karena pengguna biasa tidak bisa secara tidak sengaja merusak atau mengubah bagian penting di sistem
---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.


---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
