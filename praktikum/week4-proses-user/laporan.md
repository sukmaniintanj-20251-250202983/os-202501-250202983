
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
whoami
id
groups
sudo adduser praktikan
sudo passwd praktikan
ps aux | head -10
top -n 1
sleep 1000 &
ps aux | grep sleep
kill <PID>
pstree -p | head -20
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

## Analisis Hasil Percobaan
**Eksperimen 1 – Identitas User**
Jelaskan setiap output dan fungsinya!
- Perintah `whoami`<br>
  Output : `belinda`<br>
  Perintah ini menampilkan nama pengguna yang sedang aktif di sistem. Hasil percobaan menunjukkan bahwa user yang sedang digunakan adalah `belinda`
- Perintah `id`
  Output :
  ```bash
  uid=1001(belinda) gid=1001(belinda) groups=1001(belinda),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),100(users)
  ```
  Perintah ini menampilkan informasi identitas lengkap pengguna:
  - uid (user ID): Nomor unik untuk user `belinda`
  - gid (group ID): Nomor grup utama yang dimiliki user
  - groups: Daftar grup yang diikuti oleh user `belinda`
- Perintah `groups`
  Output : `belinda adm cdrom sudo dip plugdev users`
  Perintah ini menampilkan daftar grup yang diikuti user saat ini. Grup ini menentukan hak akses user terhadap file dan sistem.
  - `sudo`: bisa menjalankan perintah sebagai admin
  - `adm`: bisa membaca log sistem
  - `plugdev`: bisa mengakses perangkat eksternal seperti USB
- Perintah `sudo adduser praktikan`
  Output : `fatal: The user `praktikan` already exists.`
  Artinya akun tersebut sudah pernah dibuat sebelumnya, mungkin pada sesi lain atau oleh pengguna lain di komputer yang sama. Jadi sistem tidak membuat ulang akun tersebut
- Perintah `sudo passwd praktikan`
  Output : `passwd: password updated successfully`
  Perintah ini digunakan untuk mengubah password bagi user `praktikan`

**note**:
Eksperimen ini dilakukan di lab kampus UPB dengan menggunakan akun utama bernama `belinda`. Setelah meninjau ulang hasil percobaan, saya baru menyadari bahwa langkah untuk uji login ke user baru, yang seharusnya memasukkan kode `su - praktikan` belum sempat dijalankan. Hasil percobaan tersebut belum saya perbarui karena keterbatasan waktu di lab.

**Eksperimen 2 – Monitoring Proses**
Jelaskan kolom penting seperti PID, USER, %CPU, %MEM, COMMAND!  

|Kolom|Keterangan|
|-----|----------|
|PID|Merupakan nomor unik yang diberikan sistem untuk setiap proses. Dengan PID ini kita bisa menghentikan atau memantau proses tertentu|
|USER|Menunjukkan nama pengguna yang menjalankan proses. Pada hasil percobaan terlihat proses milik `root` dan `belinda`(user aktif) ini membantu mengetahui siapa pemilik tiap proses|
|%CPU|Menunjukkan presentase penggunaan CPU oleh proses tersebut. Semakin besar nilainya, semakin besar pula sumber daya prosesor yang digunakan|
|%MEM| Menunjukkan presentase penggunaan memori (RAM). Nilai kecil seperti 0.1 atau 0.2 menunjukkan bahwa proses hanya memakai sedikit memori. Dari hasil percobaan, semua proses menggunakan memori dengan sangat ringan|
|COMMAND|Menunjukkan nama perintah atau program yang dijalankan. Kolom ini membantu kita mengenali proses apa saja yang sedang bekerja di sistem|

**Eksperimen 3 – Kontrol Proses**
Catat PID proses `sleep`!  
Proses `sleep` berhasil dijalankan dengan PID = 415
  ```bash
[1] 415
belinda    415  0.0  0.0   2608   580 pts/0    S    12:49   0:00 sleep 1000
  ```
Pada percobaan ini, proses `sleep` berhasil dijalankan dengan PID 415. Setelah melakukan pengamatan untuk analisa, diketahui bahwa proses `sleep` belum dihentikan, karena saat mencoba menghentikan proses menggunakan perintah `kill<PID>`, terjadi error karena PID belum diganti. Seharusnya perintah yang benar `kill 415`. Hal ini baru diketahui saat hasil `pstree` pada eksperiman berikutnya masih menampilkan proses `sleep` yang aktif.

   **Eksperimen 4 – Analisis Hierarki Proses**
Amati hierarki proses dan identifikasi proses induk (`init`/`systemd`)! 


## Tugas
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
