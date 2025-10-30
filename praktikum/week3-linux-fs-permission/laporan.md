
# Laporan Praktikum Minggu 3
Topik: Manajemen File dan Permission di Linux

---

## Identitas
- **Nama**  : Sukmani Intan Jumala  
- **NIM**   : 250202983
- **Kelas** : 1 IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menggunakan perintah `ls`, `pwd`, `cd`, `cat` untuk navigasi file dan direktori.
2. Menggunakan `chmod` dan `chown` untuk manajemen hak akses file.
3. Menjelaskan hasil output dari perintah Linux dasar.
4. Menyusun laporan praktikum dengan struktur yang benar.
5. Mengunggah dokumentasi hasil ke Git Repository tepat waktu.

---

## Dasar Teori
Manajemen file di Linux berfungsi untuk mengatur penyimpanan dan pengaksesan data dalam sistem yang bersifat hierarkis, dimulai dari direktori utama atau root `ls`, `pwd`, `cd`dan `cat` yang membantu pengguna melihat, berpindah dan membaca isi direktori maupun file.

Selain itu, Linux juga menerapkan sistem permission yang mengatur hak akses pengguna terhadap file dan direktori. Terdapat tiga jenis hak akses, yaitu read (r), write (w), dan execute (x), yang berlaku bagi owner, group dan others. Pengaturan hak akses dapat dilakukan menggunakan perintah `chmod`, sedangkan perubahan kepemilikan file menggunakan `chown`. Pemahaman terhadap konsep ini penting agar pengguna dapat mengelola file dengan aman dan efisien.

---

## Langkah Praktikum
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).
   - Pastikan folder kerja berada di dalam direktori repositori Git praktikum:
     ```
     praktikum/week3-linux-fs-permission/
     ```

2. **Eksperimen 1 – Navigasi Sistem File**
   Jalankan perintah berikut:
   ```bash
   pwd
   ls -l
   cd /tmp
   ls -a
   ```
   - Jelaskan hasil tiap perintah.
   - Catat direktori aktif, isi folder, dan file tersembunyi (jika ada).

3. **Eksperimen 2 – Membaca File**
   Jalankan perintah:
   ```bash
   cat /etc/passwd | head -n 5
   ```
   - Jelaskan isi file dan struktur barisnya (user, UID, GID, home, shell).

4. **Eksperimen 3 – Permission & Ownership**
   Buat file baru:
   ```bash
   echo "Hello <NAME><NIM>" > percobaan.txt
   ls -l percobaan.txt
   chmod 600 percobaan.txt
   ls -l percobaan.txt
   ```
   - Analisis perbedaan sebelum dan sesudah chmod.  
   - Ubah pemilik file (jika memiliki izin sudo):
   ```bash
   sudo chown root percobaan.txt
   ls -l percobaan.txt
   ```
   - Catat hasilnya.

5. **Eksperimen 4 – Dokumentasi**
   - Ambil screenshot hasil terminal dan simpan di:
     ```
     praktikum/week3-linux-fs-permission/screenshots/
     ```
   - Tambahkan analisis hasil pada `laporan.md`.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 3 - Linux File System & Permission"
   git push origin main
---


## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](<screenshots/eksperimen week 3.png>)

---

## Analisis Hasil
**Eksperimen 1 – Navigasi Sistem File**
- Catatan: 
  - Direktori aktif: `/tmp`
  - Isi folder: `systemd-private-xxxx`, `snap-private-tmp`
  - File tersembunyi: `.X11-unix`, `.font-unix`
- Perintah`pwd` menunjukkan bahwa direktori aktif berada di`/tmp` 
- Perintah ls -l menampilkan isi direktori beserta detail seperti hak akses, pemilik, dan ukuran file
- Perintah cd /tmp digunakan untuk berpindah ke direktori `/tmp`, tetapi karena sejak awal sudah disana, maka lokasi tidak berubah
- ls -a menampilkan seluruh isi folder termasuk file tersembunyi seperti `.X11-unix` dan `.font-unix`
  
**Eksperimen 2 – Membaca File**

  Hasil:
  ```bash
  root:x:0:0:root:/root:/bin/bash
  daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
  bin:x:2:2:bin:/bin:/usr/sbin/nologin
  sys:x:3:3:sys:/dev:/usr/sbin/nologin
  sync:x:4:65534:sync:/bin:/bin/sync
  ```
  
  | Kolom | Keterangan | Contoh hasil (output) |
  |-------|------------|-----------------------|
  | username | Nama akun pengguna dalam sistem | `root`, `daemon`, `bin`, `sys`, `sync` |
  | password | Ditandai dengan `x`, artinya password disimpan di `etc/shadow/` | `x` |
  | UID (User ID) | Nomor identitas unik setiap pengguna | `0`,`1`,`2`,`3`,`65534` |
  | GID (Group ID) | Nomor grup utama pengguna | `0`,`1`,`2`,`3`,`65534` |
  | info | Deskripsi singkat akun pengguna | `root`, `daemon`, `bin`, `sys`, `sync` |
  | home | Direktori utama pengguna | `/root`, `/usr/sbin`, `bin`, `/sbin`, `/bin` |
  | shell | Program shell yang dijalankan saat login | `/bin/bash`, `/usr/sbin/nologin`, `/bin/sync`|

Berdasarkan hasil di atas, file `/etc/passwd` berisi daftar pengguna sistem beserta informasi dasar seperti UID, GID, direktori home, dan shell yang digunakan. Beberapa akun seperti daemon dan bin tidak memiliki akses login langsung karena menggunakan `/usr/sbin/nologin`, sedangkan akun root memiliki akses penuh dengan shell aktif /bin/bash

**Eksperimen 3 – Permission & Ownership**

| Perintah  | Output / Hasil  | Keterangan          |
| --------- | --------------- | ------------------- |
| `echo "Hello <INTAN><25202983>" > percobaan.txt`  | Membuat file baru bernama `percobaan.txt` berisi teks `Hello <INTAN><25202983>` | Perintah `echo` digunakan untuk menulis teks ke dalam file baru |
| `ls -l percobaan.txt`  | `-rw-r--r-- 1 labupb labupb 25 Oct 23 18:49 percobaan.txt` | File `percobaan.txt` memiliki permission awal **rw-r--r--** (pemilik dapat membaca & menulis, grup & lainnya hanya bisa membaca) |
| `chmod 600 percobaan.txt` | Mengubah izin akses file | Perintah `chmod 600` membatasi akses hanya untuk pemilik file |
| `ls -l percobaan.txt` | `-rw------- 1 labupb labupb 25 Oct 23 18:49 percobaan.txt` | Setelah diubah, hanya pemilik (`labupb`) yang bisa membaca dan menulis file. Pengguna lain tidak bisa mengaksesnya |
| `sudo chown root percobaan.txt` | Tidak dijalankan (karena tidak memiliki izin `sudo`) | Perintah ini seharusnya mengubah kepemilikan file menjadi `root`, namun di lingkungan lab kampus tidak dapat dilakukan karena akses `sudo` dibatasi |

Perbedaan sebelum dan sesudah `chmod`

| Sebelum `(ls -l percobaan.txt) | Sesudah `(chmod 600 percobaan.txt)` |
| -------------------------------- | ----------------------------------- |
| `-rw-r--r--` → pemilik bisa membaca & menulis, grup dan lainnya hanya bisa membaca | `-rw-------` → hanya pemilik yang bisa membaca & menulis, pengguna lain tidak memiliki akses |

---

### Tugas
**Fungsi tiap perintah dan arti kolom permission (`rwxr-xr--`)**

| Perintah | Fungsi                                                                                                                  |
| ------------ | ------------------------------------------------------------------------------------------------------------------- |
| `pwd`        | Menampilkan direktori aktif saat ini (working directory).                                                           |
| `ls -l`      | Menampilkan daftar isi direktori dengan informasi detail seperti permission, pemilik, ukuran, dan waktu modifikasi. |
| `cd`         | Berpindah ke direktori lain.                                                                                        |
| `cat`        | Menampilkan isi file ke terminal.                                                                                   |
| `chmod`      | Mengubah hak akses (permission) file atau direktori.                                                                |
| `chown`      | Mengubah kepemilikan file atau direktori (user/group owner).                                                        |

Arti kolom permission `rwxr-xr--`:
- Pemilik: memiliki hak baca tulis dan eksekusi
- Grup: hanya memiliki hak baca dan eksekusi
- Lainnya: hanya memiliki hak baca

Struktur `rwxr-xr--` berarti:
- `rwx` : hak akses untuk pemilik (user), artinya dapat membaca (read), menulis (write), dan menjalankan (execute) file
- `r-x` : hak akses untuk grup, artinya hanya dapat membaca dan menjalankan file, tetapi tidak dapat menullis atau mengubahnya
- `r--` : hak akses untuk pengguna lain (others), artinya hanya dapat membaca file tanpa bisa menulis atau menjalankan

**Analisis peran `chmod` dan `chown` dalam keamanan sistem Linux**
   Peran `chmod` dan `chown` dalam keamanan sistem Linux adalah untuk mengontrol akses dan kepemilikan file agar sistem tetap aman.
`chmod`: Mengatur izin akses (read, write, execute) sehingga hanya pengguna yang berhak dapat membuka, mengubah, atau menjalankan file.
`chown`: Menentukan pemilik dan grup file agar hanya pengguna yang sah yang memiliki kendali atas file tersebut.

---

## Quiz
1. Apa fungsi dari perintah chmod?
   *jawaban* : Fungsi perintah `chmod` adalah untuk mengubah izin akses (hak akses) pada file atau direktori, sehingga kita    bisa menentukan siapa yang boleh membaca (read), menulis (write), atau menjalankan (execute) file tersebut 
2. Apa arti dari kode permission rwxr-xr--?
   *jawaban* :

| Bagian  | Subjek           | Izin                 | Arti                                                               |
| ------- | ---------------- | -------------------- | ------------------------------------------------------------------ |
| **rwx** | Pemilik (owner)  | read, write, execute | Pemilik bisa membaca, menulis, dan menjalankan file                |
| **r-x** | Grup (group)     | read, execute        | Anggota grup bisa membaca dan menjalankan, tapi tidak bisa menulis |
| **r--** | Lainnya (others) | read                 | Pengguna lain hanya bisa membaca file                              |

3. Jelaskan perbedaan antara chown dan chmod.

| Perintah    | Fungsi Utama                              | Yang Diubah          | Contoh Penggunaan           |
| ----------- | ----------------------------------------- | -------------------- | --------------------------- |
| **`chown`** | Mengubah **kepemilikan (owner dan group)** suatu file atau folder | Pemilik dan grup file  | `chown user:group file.txt` |
| **`chmod`** | Mengubah **izin akses (permissions)** suatu file atau folder  | Hak akses (read, write, execute) | `chmod 755 file.txt`  |

---

## Kesimpulan
Dari tiga eksperimen yang dilakukan, dapat disimpulkan bahwa pengelolaan file dan permission di sistem operasi Linux merupakan hal yang sangat penting dalam menjaga keamanan dan keteraturan sistem.
Perintah dasar seperti pwd, ls, cd, dan cat membantu pengguna untuk menavigasi serta membaca isi file dalam sistem.
Sementara itu, chmod berfungsi untuk mengatur hak akses terhadap file atau direktori, dan chown digunakan untuk mengubah kepemilikan file.

Hasil eksperimen menunjukkan bahwa perubahan permission dengan chmod berhasil membatasi akses hanya untuk pemilik file, sedangkan perintah chown tidak dapat dijalankan karena hak akses sudo dibatasi di lingkungan lab kampus.
Hal ini menunjukkan pentingnya kebijakan keamanan dalam sistem multiuser seperti Linux, agar tidak semua pengguna memiliki kendali penuh terhadap sistem.

Jadi secara keseluruhan, praktikum ini memberikan pemahaman nyata mengenai bagaimana Linux mengatur akses pengguna dan peran administrator dalam menjaga keamanan sistem

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini? Semuanya 
- Bagaimana cara Anda mengatasinya? Belajar! mencoba dan mencoba!

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
