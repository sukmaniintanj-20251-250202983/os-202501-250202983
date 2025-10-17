
# Laporan Praktikum Minggu [X]
Topik: Struktur Systemm Call dan Fungsi Kernel
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

## D. Tugas & Quiz
### Tugas
1. Dokumentasikan hasil eksperimen `strace` dan `dmesg` dalam bentuk tabel observasi.  
2. Buat diagram alur system call dari aplikasi → kernel → hardware → kembali ke aplikasi.  
3. Tulis analisis 400–500 kata tentang:
   - Mengapa system call penting untuk keamanan OS?  
   - Bagaimana OS memastikan transisi user–kernel berjalan aman?  
   - Sebutkan contoh system call yang sering digunakan di Linux.  
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
