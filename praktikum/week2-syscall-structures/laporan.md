
# Laporan Praktikum Minggu [X]
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : Sukmani Intan Jumala 
- **NIM**   : 250202983
- **Kelas** : S1 Informatika

---
## Deskripsi Singkat
## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
> Mahasiswa mampu menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
lsmod | head
dmesg | head
```

---

## Hasil Eksekusi
![Screenshot hasil](<screenshots/strace ls 1.png>)
![Screenshot hasil](<screenshots/strace ls 2.png>)
![Screenshot hasil](<screenshots/strace -e trace=open,read,write,close cat etcpasswd.png>)
![Screenshot hasil](<screenshots/dmesg  tail -n 10.png>)
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

## Quiz
1. Apa fungsi utama system call dalam sistem operasi?
   **Jawaban:**Fungsi utama nya adalah supaya aplikasi bisa meminta bantuan sistem operasi untuk melakukan sesuatu yang aplikasi sendiri tidak bisa langsung lakukan, seperti membuka file, mengakses perangkat seperti keyboard, printer, atau layar, serta mengatur memori supaya aplikasi bisa berjalan lancar.
3. Sebutkan 4 kategori system call yang umum digunakan. 
   **Jawaban:**1. Manajemen proses
   2. Manajemen file
   3. Manajemen memori
   4. Manajemen perangkat I/O
5. Mengapa system call tidak bisa dipanggil langsung oleh user program?  
   **Jawaban:**System call tidak bisa dipanggil langsung oleh program pengguna karena alesan keamanan dan ketertiban  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
