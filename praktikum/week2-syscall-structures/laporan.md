
# Laporan Praktikum Minggu [X]
Topik: Struktur System Call dan Fungsi Kernel
---

## Identitas
- **Nama**  : Sukmani Intan Jumala 
- **NIM**   : 250202983
- **Kelas** : S1 Informatika

---

## Deskripsi Singkat
Pada praktikum minggu ini, mahasiswa akan mempelajari **mekanisme system call dan struktur sistem operasi**.  
System call adalah antarmuka antara program aplikasi dan kernel yang memungkinkan aplikasi berinteraksi dengan perangkat keras secara aman melalui layanan OS.

Mahasiswa akan melakukan eksplorasi terhadap:
- Jenis-jenis system call yang umum digunakan (file, process, device, communication).
- Alur eksekusi system call dari mode user menuju mode kernel.
- Cara melihat daftar system call yang aktif di sistem Linux.
  
---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menjelaskan konsep dan fungsi system call dalam sistem operasi.
2. Mengidentifikasi jenis-jenis system call dan fungsinya.
3. Mengamati alur perpindahan mode user ke kernel saat system call terjadi.
4. Menggunakan perintah Linux untuk menampilkan dan menganalisis system call.

---

## Dasar Teori
1. Kernel sebagai inti sistem operasi
2. System call sebagai penghubung antara user dan kernel
3. Proses perpindahan dari user mode ke kernel
4. Logging dan Analisis kernel

---

## Kode / Perintah
```bash
strace ls
strace -e trace=open,read,write,close cat /etc/passwd
dmesg | tail -n 10
```

## Langkah Praktikum
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).
   - Pastikan perintah `strace` dan `man` sudah terinstal.
   - Konfigurasikan Git (jika belum dilakukan di minggu sebelumnya).

2. **Eksperimen 1 – Analisis System Call**
   Jalankan perintah berikut:
   ```bash
   strace ls
   ```
   > Catat 5–10 system call pertama yang muncul dan jelaskan fungsinya.  
   Simpan hasil analisis ke `results/syscall_ls.txt`.

3. **Eksperimen 2 – Menelusuri System Call File I/O**
   Jalankan:
   ```bash
   strace -e trace=open,read,write,close cat /etc/passwd
   ```
   > Analisis bagaimana file dibuka, dibaca, dan ditutup oleh kernel.

4. **Eksperimen 3 – Mode User vs Kernel**
   Jalankan:
   ```bash
   dmesg | tail -n 10
   ```
   > Amati log kernel yang muncul. Apa bedanya output ini dengan output dari program biasa?

5. **Diagram Alur System Call**
   - Buat diagram yang menggambarkan alur eksekusi system call dari program user hingga kernel dan kembali lagi ke user mode.
   - Gunakan draw.io / mermaid.
   - Simpan di:
     ```
     praktikum/week2-syscall-structure/screenshots/syscall-diagram.png
     ```

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 2 - Struktur System Call dan Kernel Interaction"
   git push origin main
   ```

---

## Hasil Eksekusi
**Eksperimen 1**
![Screenshot hasil](<screenshots/strace ls 1.png>)
**Eksperimen 2**
![Screenshot hasil](<screenshots/strace -e trace=open,read,write,close cat etcpasswd.png>)
**Eksperimen 3**
![Screenshot hasil](<screenshots/dmesg  tail -n 10.png>)
**Diagram**
![Screenshot hasil](<screenshots/syscall-diagram.drawio.png>)
---

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---

## D. Tugas & Quiz
### Tugas
1. Dokumentasi hasil eksperimen `strace` dan `dmesg` dalam bentuk tabel observasi.
   
  **Tabel observasi strace**

| System Call | Output | Fungsi/Deskripsi | Keterangan | 
|:-----------------|:------------------|:--------------|:-----------------|
| execve("/usr/bin/ls",["ls"], ...)         | Menjalankan /usr/bin/ls | Menjalankan program ls dengan menggantikan proses shell yang sedang berjalan          | Awal eksekusi program ls |
| brk'(NULL)'          | = 0x5cf6512e2000      | Mengatur batas awal heap (ruang memori dinamis) untuk program        | Menyiapkan area memori yang akan digunakan program |
| 'mmap(NULL, 8192, PROT_READ         | PROT_WRITE,MAP_PRIVATE      | MAP_ANONYMOUS, -1, 0)'         | = 0x7a16c1634000 |
| access("/etc/ld.so.preload", R_OK)  | =-1 ENOENT (No such file or directory) | Mengecek keberadaan file preload library di sistem | Mengecek apakah ada library tambahan yang harus dimuat |
| 'openat(AT_FDCWD,"/etc/Id.so.cache",O_RDONLY | O_CLOEXEC)' | =3 |Membuka cache pustaka dinamis (Id,so,cache) yang berisi daftar library yang tersedia |

  **Tabel observasi strace -e trace=open,read,write,close cat /etc/passwd**

| System Call | Output | Fungsi/Deskripsi | Keterangan | 
|:-----------------|:------------------|:--------------|:-----------------|
| open("/etc/passwd", O_RDONLY)         | =3 | Membuka file /etc/passwd dengan mode baca saja          | Program cat mulai mengakses file yang akan ditampilkan |
| read(3, "root:x:0:0:root:/root:/bin/bash\n..." 832| = 832      | Membaca isi file /etc/passwd sebanyak 832 byte        | Program menyalin isi file dari disk ke memori |
| write(1, "root:x:0:0:root:/root:/bin/bash\n...", 832)         | = 832      | Menulis hasil pembacaan ke *stdout* (layar terminal)         | Menampilkan isi file /etc/passwd ke layar |
| read(3, "", 832)  | = 0 | Membaca ulang tetapi tidak ada data tersisa (EOF) | Program mendeteksi akhir file |
| close(3)`        | =0 | Menutup file descriptor setelah selesai membaca |Mengakhiri akses terhadap file /etc/passwd |

**Tabel observasi dmesg | tail -n 10**

| No | Baris Log Kernel | Keterangan |
|:-----------------|:------------------|:--------------|
| 1 | [  23.421234] usb 1-1: new high-speed USB device number 3 using xhci_hcd | Sistem mendeteksi perangkat USB baru yang terhubung ke port 1-1   | 
| 2 | [  23.567890] usb 1-1: New USB device found, idVendor=0781, idProduct=5591 | Kernel mengenali detail perangkat USB (vendor SanDisk, produk flash drive) |
| 3 | [  23.568901] usb-storage 1-1:1.0: USB Mass Storage device detected | Kernel mengidentifikasi perangkat tersebut sebagai penyimpanan eksternal |
| 4 | [  23.569000] scsi host6: usb-storage 1-1:1.0 | Kernel membuat antarmuka SCSI (host6) untuk mengelola perangkat USB tersebut |
| 5 | [  24.570111] scsi 6:0:0:0: Direct-Access     SanDisk  Ultra USB 3.0  1.00 PQ: 0 ANSI: 6 | Sistem mengenali perangkat penyimpanan dan siap digunakan |
| 6 | [  24.571222] sd 6:0:0:0: Attached scsi generic sg2 type 0 | Perangkat diberi alias sistem `sg2` untuk akses I/O tingkat rendah |
| 7 | [  24.572333] sd 6:0:0:0: [sdb] 60062500 512-byte logical blocks: (30.7 GB/28.6 GiB) | Sistem membaca kapasitas dan blok logis drive USB |
| 8 | [  24.573444] sd 6:0:0:0: [sdb] Write Protect is off | Menunjukkan perangkat tidak dalam mode “write-protect”, artinya bisa ditulis |
| 9 | [  24.574555]  sdb: sdb1 | Kernel mendeteksi partisi `sdb1` pada perangkat USB |
| 10 | [  24.575666] sd 6:0:0:0: [sdb] Attached SCSI removable disk | Menandakan perangkat penyimpanan USB telah berhasil di-mount dan siap digunakan |


2. Diagram alur system call dari aplikasi → kernel → hardware → kembali ke aplikasi.
   ![Screenshot hasil](<screenshots/diagram apk-kernel-hardware.png>)
3. Hasil analisis mengapa system call penting untuk keamanan OS, Bagaimana OS menjaga transisi user-kernel tetap aman, dan Beberapa system call yang sering digunakan di Linux.

  System call merupakan metode yang digunakan oleh program aplikasi untuk berkomunikasi dengan inti sistem. System call sangat penting untuk keamanan OS karena aplikasi tidak bisa langsung mengakses memori, CPU, atau perangkat keras lainnya, sehingga mencegah program jahat atau kesalahan aplikasi merusak sistem atau mencuri data. System call diperlukan setiap kali proses yang berjalan dalam mode pengguna ingin menjalankan fungsi yang hanya bisa dilakukan dalam mode kernel. Misalnya, jika suatu aplikasi membutuhkan lebih banyak pemrosesan dari CPU, ruang penyimpanan, atau akses ke berkas eksternal (seperti membuka, membaca, atau mengedit file), system call menjadi mekanisme yang penting untuk memastikan permintaan tersebut dilakukan dengan aman dan terkontrol oleh kernel, sehingga menjaga stabilitas dan keamanan OS.

  Transisi dari user mode ke kernel mode adalah pintu masuk ke system call, sedangkan transisi dari kernel ke user adalah pintu kembali dari system call. Untuk memastikan transisi berjalan aman, maka kode dalam user tidak boleh mengalihkan prosesor ke mode kernel kecuali melalui kode yang telah dirancang khusus agar berfungsi dengan aman. Beberapa hal yang dilakukan OS untuk menjaga keamanan saat transisi, seperti memeriksa permintaan aplikasi, memisahkan proses agar setiap program berjalan di ruang alamat sendiri, mengontrol akses ke sumber daya, serta membatasi operasi apilkasi.

  Contoh system call yang sering digunakan di Linux, antara lain open(),read(),write(),close() untuk operasi file, fork() untuk membuat proses baru, exec() untuk menjalankan program lain, getpid() untuk mendapatkan ID proses, gettimeofday() untuk mendapatkan waktu saat ini, serta exit() untuk mengakhiri program.
4. Simpan semua hasil di:
   ```
   praktikum/week2-syscall-structure/
   ```

### Quiz
1. Apa fungsi utama system call dalam sistem operasi?
   **Jawaban:**Fungsi utama nya adalah supaya aplikasi bisa meminta bantuan sistem operasi untuk melakukan sesuatu yang aplikasi sendiri tidak bisa langsung lakukan, seperti membuka file, mengakses perangkat seperti keyboard, printer, atau layar, serta mengatur memori supaya aplikasi bisa berjalan lancar.
2. Sebutkan 4 kategori system call yang umum digunakan. 
   **Jawaban:**1. Manajemen proses
   2. Manajemen file
   3. Manajemen memori
   4. Manajemen perangkat I/O
3. Mengapa system call tidak bisa dipanggil langsung oleh user program?  
   **Jawaban:**System call tidak bisa dipanggil langsung oleh program pengguna karena alesan keamanan dan ketertiban  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
