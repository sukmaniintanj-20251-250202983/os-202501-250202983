
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
Eksperimen 1
![Screenshot hasil](<screenshots/eksperimen_1.png>)
Eksperimen 2
![Screenshot hasil](<screenshots/eksperimen_2.png>)
Eksperimen 3 dan 4
![Screenshot hasil](<screenshots/eksperimen_3dan4.png>)

---

## Analisis Hasil Percobaan
**Eksperimen 1 – Identitas User**  
Jelaskan setiap output dan fungsinya!
- Perintah `whoami`<br>
  Output : `belinda`<br>
  Perintah ini menampilkan nama pengguna yang sedang aktif di sistem. Hasil percobaan menunjukkan bahwa user yang sedang digunakan adalah `belinda`
- Perintah `id`<br>
  Output :
  ```bash
  uid=1001(belinda) gid=1001(belinda) groups=1001(belinda),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),100(users)
  ```
  Perintah ini menampilkan informasi identitas lengkap pengguna:
  - uid (user ID): Nomor unik untuk user `belinda`
  - gid (group ID): Nomor grup utama yang dimiliki user
  - groups: Daftar grup yang diikuti oleh user `belinda`
- Perintah `groups`<br>
  Output : `belinda adm cdrom sudo dip plugdev users`
  Perintah ini menampilkan daftar grup yang diikuti user saat ini. Grup ini menentukan hak akses user terhadap file dan sistem.
  - `sudo`: bisa menjalankan perintah sebagai admin
  - `adm`: bisa membaca log sistem
  - `plugdev`: bisa mengakses perangkat eksternal seperti USB
- Perintah `sudo adduser praktikan`<br>
  Output : `fatal: The user `praktikan` already exists.`
  Artinya akun tersebut sudah pernah dibuat sebelumnya, mungkin pada sesi lain atau oleh pengguna lain di komputer yang sama. Jadi sistem tidak membuat ulang akun tersebut
- Perintah `sudo passwd praktikan`<br>
  Output : `passwd: password updated successfully`
  Perintah ini digunakan untuk mengubah password bagi user `praktikan`

**note**:
Eksperimen ini dilakukan di lab kampus UPB dengan menggunakan akun utama bernama `belinda`. Setelah meninjau ulang hasil percobaan, saya baru menyadari bahwa langkah untuk uji login ke user baru, yang seharusnya memasukkan kode `su - praktikan` belum sempat dijalankan. Hasil percobaan tersebut belum saya perbarui karena keterbatasan waktu di lab.

**Eksperimen 2 – Monitoring Proses**  
Jelaskan kolom penting seperti PID, USER, %CPU, %MEM, COMMAND!  

|Kolom|Keterangan|
|-----|----------|
|**PID**|Merupakan nomor unik yang diberikan sistem untuk setiap proses. Dengan PID ini kita bisa menghentikan atau memantau proses tertentu|
|**USER**|Menunjukkan nama pengguna yang menjalankan proses. Pada hasil percobaan terlihat proses milik `root` dan `belinda`(user aktif) ini membantu mengetahui siapa pemilik tiap proses|
|**%CPU**|Menunjukkan presentase penggunaan CPU oleh proses tersebut. Semakin besar nilainya, semakin besar pula sumber daya prosesor yang digunakan|
|**%MEM**| Menunjukkan presentase penggunaan memori (RAM). Nilai kecil seperti 0.1 atau 0.2 menunjukkan bahwa proses hanya memakai sedikit memori. Dari hasil percobaan, semua proses menggunakan memori dengan sangat ringan|
|**COMMAND**|Menunjukkan nama perintah atau program yang dijalankan. Kolom ini membantu kita mengenali proses apa saja yang sedang bekerja di sistem|

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
```bash
systemd(1)─┬─agetty(168)
            ├─agetty(171)
            ├─cron(152)
            ├─dbus-daemon(153)
            ├─init-systemd(Ub2)─┬─SessionLeader(278)─┬─Relay(280)(279)─┬─(bash(280)─┬─head(419)
            │                   │                                                  ├─pstree(418)
            │                   │                                                  └─sleep(415)
            │                   ├─init(7)───{init}(8)
            │                   ├─login(281)───bash(346)
            │                   └─{init-systemd(Ub)}(9)
            ├─rsyslogd(177)─┬─{rsyslogd}(195)
            │               ├─{rsyslogd}(196)
            │               └─{rsyslogd}(197)
            ├─systemd(332)───(sd-pam)(333)
            ├─systemd-journal(49)
            ├─systemd-logind(160)
            ├─systemd-resolve(145)
            ├─systemd-timesyncd(146)───{systemd-timesyn}(150)
            ├─systemd-udevd(91)
            └─unattended-upgr(194)───{unattended-upgr}(230)
```
- Proses induk utama pada sistem adalah `systemd`(PID 1)
- Beberapa proses turunan yang muncul antara lain `agetty`, `cron`, `dbus-daemon`, `systems-logind`, dan `systemd-udevd`
- Proses `sleep(415)` merupakan proses anak dari `bash(280)` yang dijalankan oleh pengguna `belinda`, menunjukkan bahwa proses dari sebelumnya masih aktif

---

## Tugas
1. Dokumentasikan hasil semua perintah dan jelaskan fungsi tiap perintah.

| Perintah | Fungsi |
|----------|---------|
| `whoami` | Menampilkan nama user yang sedang aktif|
|`id`|Menunjukkan UID, GID, dan grup user|
|`groups`|Menampilkan daftar grup yang diikuti user|
|`sudo adduser praktikan`|Membuat akun user baru bernama praktikan|
|`sudo passwd praktikan`|Mengatur atau mengganti password user praktikan|
|`su - praktikan`|Berpindah login ke akun praktikan|
|`ps aux|`head -10`|
|`top -n 1|Menampilkan aktivitas sistem dan penggunaan CPU/RAM|
|`sleep 1000 &`|Menjalankan proses sleep di latar belakang|
|`ps aux| grep sleep`|
|`kill<PID>`|Menghentikan proses berdasarkan nomor PID|
|`pstree-p| head -20`|
|(hasil `pstree`)|Menunjukkan `systems(1)` sebagai proses induk utama dan sleep (415) sebagai turunan|
|-|Menunjukkan keterkaitan:proses sleep dari eksperimen 3 masih aktif pada eksperimen 4|

2. Gambarkan hierarki proses dalam bentuk diagram pohon (`pstree`) di laporan.
```bash
systemd(1)
 ├─agetty(168)
 ├─agetty(171)
 ├─cron(152)
 ├─dbus-daemon(153)
 ├─init-systemd(Ub2)
 │   ├─SessionLeader(278)
 │   │   └─bash(280)
 │   │       ├─head(419)
 │   │       ├─pstree(418)
 │   │       └─sleep(415)
 │   └─login(281)
 │       └─bash(346)
 ├─rsyslogd(177)
 ├─systemd-journal(49)
 ├─systemd-logind(160)
 ├─systemd-resolve(145)
 ├─systemd-timesyncd(146)
 ├─systemd-udevd(91)
 └─unattended-upgr(194)
```

3. Jelaskan hubungan antara user management dan keamanan sistem Linux.
   User management memiliki peran penting dalam menjaga keamanan sistem Linux. Melalui pengaturan user dan grup, sistem dapat membatasi hak akses setiap pengguna sesuai perannya. Dengan begitu, tidak semua user memiliki izin untuk mengubah konfigurasi penting atau menjalankan perintah berisiko.
Selain membatasi akses, user management juga membantu melacak aktivitas setiap pengguna sehingga jika terjadi kesalahan atau ancaman, sumbernya dapat diketahui. Jadi, pengelolaan user yang baik bukan hanya soal membuat akun, tetapi juga menjaga sistem tetap aman, tertib, dan terkontrol.

## Quiz
Tuliskan jawaban di bagian **Quiz** pada laporan:
1. Apa fungsi dari proses `init` atau `systemd` dalam sistem Linux?
   *jawaban*: `init` atau `systemd`berfungsi sebagai pengatur utama yang memastikan seluruh proses dan layanan dalam sistem linux berjalan dengan lancar dan terkoordinasi sejak komputer dinyalakan hingga dimatikan. Proses `init` atau `systemd` merupakan proses pertama yang dijalankan setelah kernel linux aktif dan memiliki PID 1 sebagai induk dari semua proses yang berfungsi untuk menyiapkan proses agar siap digunakan. Pada sistem lama digunakan `init`, sedangkan sistem modern memakai `systemd` yang lebih cepat dan efisien.
2. Apa perbedaan antara `kill` dan `killall`?
   *jawaban*: Perintah `kill` dan `killall` sama sama berfungsi untuk menghentikan proses yang sedang berjalan, tapi dengan cara yang berbeda. `kill` digunakan jika kita tahu nomor prosesnya (PID), jadi hanya menghentikan satu proses tertentu. Sementara `killall` bisa menghentikan semua proses yang memiliki nama program yang sama tanpa harus mencari PID nya. Jadi `kill` bekerja berdasarkan ID proses, sedangkan `killall` bekerja sebagai nama proses.
3. Mengapa user `root` memiliki hak istimewa di sistem Linux?
   *jawaban*: user `root` merupakan penggunan dengan hak istimewa tertinggi. Akun ini bisa melakukan apapun di sistem, seperti mengubah pengaturan penting, menghapus file sistem, memasang software atau mengatur hak akses pengguna lain. Alasan `root` memiliki hak istimewa adalah karena linux di desain dengan sistem keamanan berlapis, hanya pengguna tertentu (`root`) yang boleh melakukan tindakan yang bisa memengaruhi seluruh sistem. Dengan begitu, sistem jadi lebih aman karena pengguna biasa tidak bisa secara tidak sengaja merusak atau mengubah bagian penting di sistem
---

## Kesimpulan
1. Melalui praktikum ini, saya memahami cara mengelola user dan memantau proses yang berjalan di sistem linux, termask menambah mengubah, dan mengatur hak akses user.
2. Setiap proses di linux memiliki hierarki yang terstruktur dengan `systemd` sebagai proses induk utama, yang menjadi dasar dari semmua proses lain di sistem
3. Secara keseluruhan, praktikum ini menegaskan bahwa manajemen user dan proses merupakan bagian penting dalam sistem linux. Karena keduanya saling berhubungan dalam menjaga stabilitas keamanan sistem operasi.


---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  Masuk minggu keempat saya masih mengerjakan uji coba/eksperimen di lab kampus, karena belum memiliki laptop pribadi. Hal itu sedikit menghambat dalam mengerjakan tugas karena keterbatasan waktu di lab. Pada praktikum ini ada beberapa langkah yang tidak sesuai perintah atau terlewat, tetapi saya belum bisa mencoba uji coba ulang di kampus.
- Bagaimana cara Anda mengatasinya?  
Dengan keterbatasan waktu dan belum bisa melakukan-uji coba ulang, maka saya mencoba memahami hal hal yang terlewat dan menjelaskan nya di laporan. Bagi saya yang penting saya paham apa, kenapa, terdapat kesalahan dimananya dan harusnya seperti apa untuk perbaikan. Uji coba ulang akan saya lakukan di kesempatan.
---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
