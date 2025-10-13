
# Laporan Praktikum Minggu [X]
Topik: [Arsitektur Sistem Operasi dan Kernel]

---

## Identitas
- **Nama**  : Sukmani Intan Jumala  
- **NIM**   : 250202983  
- **Kelas** : 1IKRA

---

## Tujuan
Mengenal peran sistem operasi, fungsi kernel sebagai pengatur utama, serta dapat membandingkan model arsitektur OS.

---

## Dasar Teori
1. Sistem operasi bertugas mengatur semua aktivitas di komputer
2. Kernel menjadi otak utama yang mengatur proses dan pengunaan memori
3. Arsitektur menentukan cara komponen OS bekerja sama
4. Ada 3 model umum: Monolithic , Microkernel, dan Layered
5. Percobaan ini bertujuan memahami kinerja setiap arsitektur

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
![alt text](<screenshots/Screenshot.png>)

---

## Analisis
- Makna hasil percobaan.
  Kode "uname -a" menampilkan informasi lengkap yang ada di sistem,
  Kode "whoami" menampilkan semua user yang sedang aktif di sistem,
  Kode "lsmod | head" menampilkan daftar modul kernel yang sedang aktif (hanya 10 baris pertama),
  Kode "dmesg | head" menampilkan pesan-pesan yang dicatat kernel (hanya 10 baris pertama)
- Hasil eksperimen menunjukkan hubungan langsung dengan teori,seperti berikut: membuktikan bahwa kernel berfungsi sesuai teori yaitu mengelola sumber daya utama seperti CPU, memori dan proses. Penghubung ke kernel saat melakukan hal penting seperti membaca file, menunjukkan bahwa program menggunakan system call, yang memiliki peran sebagai jembatan penghubung. Desain arsitektur membuktikan bahwa cara OS dirancang sangat memengaruhi seberapa cepat dan efisien sistem bekerja
- Perbedaan Linux vs Windows yaitu: Di lingkungan Linux, perintah-perintah tersebut dirancang untuk berinteraksi secara langsung dan mendalam dengan inti sistem (kernel) untuk mendapat informasi detail. Pada lingkungan windows, arsitekturnya berbeda sehingga perintah-perintah tersebut tidak akan dikenali. Untuk mendapat informasi serupa, harus menggunakan aplikasi terpisah.
---

## Kesimpulan
Praktikum ini menyimpulkan bahwa sistem operasi memainkan peran utama sebagai perantara antara pengguna, perangkat lunak, dan perangkat keras. Melalui komponen seperti kernel dan system cell, OS mengatur sumber daya komputer secara efisien. Perbedaan arsitektur antara Linux dan Windows, secara langsung memengaruhi cara sistem beroperasi. sehingga penting untuk memahami konsep OS untuk penggunaan komputer yang optimal

---

## Quiz
1. Sebutkan 3 fungsi utama sistem operasi  
   **Jawaban:** 1.Manajemen sumber daya (Resource Management)
   2. Manajemen file dan sistem penyimpanan (File Management)
   3. Manajemen Proses (Process Management)
2. Jelaskan perbedaan antara kernel mode dan user mode
   **Jawaban:** Kernel mode dimana mode sistem operasi memiliki hak akses penuh ke semua bagian komputer termasuk perangkat keras. Sedangkan di user mode, program tidak memiliki akses langsung ke perangkat keras, semua harus melewati izin lewat kernel.  
3. Sebutkan contoh OS dengan arsitektur monolithic dan microkernel 
   **Jawaban:** Monolithic: Linux, MS-DOS,Unix Tradisional
   Microkernel: Minix, MacOS, QNX  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
Bagian paling menantang di minggu ini bagi saya adalah pemahaman materi itu sendiri. Saya merasa sangat gaptek dan sangat tertinggal dari yang lain, sedikit sulit untuk memahami materi karena belum dibekali apapun sebelumnya.
- Bagaimana cara Anda mengatasinya?
Saya mengatasi hal tersebut dengan mencari tau di berbagai sumber setelah kelas selesai. Memanfaatkan AI untuk mencari poin-poin yang belum dipahami sebelumnya, serta melihat penjelasan di video youtube.    

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
