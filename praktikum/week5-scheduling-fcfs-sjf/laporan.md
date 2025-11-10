# Laporan Praktikum Minggu 5
Topik: Penjadwalan CPU – FCFS dan SJF  

---

## Identitas
- **Nama**  : Sukmani Intan Jumala
- **NIM**   : 250202983
- **Kelas** : 1 IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menghitung *waiting time* dan *turnaround time* untuk algoritma FCFS dan SJF.  
2. Menyajikan hasil perhitungan dalam tabel yang rapi dan mudah dibaca.  
3. Membandingkan performa FCFS dan SJF berdasarkan hasil analisis.  
4. Menjelaskan kelebihan dan kekurangan masing-masing algoritma.  
5. Menyimpulkan kapan algoritma FCFS atau SJF lebih sesuai digunakan.  

---

## Dasar Teori
1. Penjadwalan CPU, merupakan mekanisme yang dilakukan sistem operasi untuk menentukan urutan proses yang akan dijalankan oleh prosesor. Jumlah prosesor yang menunggu terkadang melebihi kapasitas CPU, maka sistem perlu mengatur gilira agar sumber daya dapat digunakan secara efisien
(Silberschatz et al., 2018).
2. Algoritma FCFS (First Come, First Served) adalah algoritma penjadwalan paling sederhana yang bekerja berdasarkan urutan kedatangan proses. Proses yang tiba terlebih dahulu akan dijalankan lebih dulu, begitupun sebaliknya.
3. Algoritma SJF (Shortest Job First), bekerja dengan memilih proses yang memiliki waktu eksekusi paling singkat untuk dijalankan terlebih dahulu.
4. Perbandingan FCFS dan SJF, FCFS lebih teratur dan mudah diterapkan, namun cenderung kurang efisien jika waktu proses bervariasi, sedangkan SJF dapat bekerja lebih cepat dan efisien secara keseluruhan, namun bisa membuat proses berdurasi panjang tertunda.

---

## Langkah Praktikum
1. **Siapkan Data Proses**
   Gunakan tabel proses berikut sebagai contoh (boleh dimodifikasi dengan data baru):
   | Proses | Burst Time | Arrival Time |
   |:--:|:--:|:--:|
   | P1 | 6 | 0 |
   | P2 | 8 | 1 |
   | P3 | 7 | 2 |
   | P4 | 3 | 3 |

2. **Eksperimen 1 – FCFS (First Come First Served)**
   - Urutkan proses berdasarkan *Arrival Time*.  
   - Hitung nilai berikut untuk tiap proses:
     ```
     Waiting Time (WT) = waktu mulai eksekusi - Arrival Time
     Turnaround Time (TAT) = WT + Burst Time
     ```
   - Hitung rata-rata Waiting Time dan Turnaround Time.  
   - Buat Gantt Chart sederhana:  
     ```
     | P1 | P2 | P3 | P4 |
     0    6    14   21   24
     ```

3. **Eksperimen 2 – SJF (Shortest Job First)**
   - Urutkan proses berdasarkan *Burst Time* terpendek (dengan memperhatikan waktu kedatangan).  
   - Lakukan perhitungan WT dan TAT seperti langkah sebelumnya.  
   - Bandingkan hasil FCFS dan SJF pada tabel berikut:

     | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
     |------------|------------------|----------------------|------------|-------------|
     | FCFS | ... | ... | Sederhana dan mudah diterapkan | Tidak efisien untuk proses panjang |
     | SJF | ... | ... | Optimal untuk job pendek | Menyebabkan *starvation* pada job panjang |

4. **Eksperimen 3 – Visualisasi Spreadsheet (Opsional)**
   - Gunakan Excel/Google Sheets untuk membuat perhitungan otomatis:
     - Kolom: Arrival, Burst, Start, Waiting, Turnaround, Finish.
     - Gunakan formula dasar penjumlahan/subtraksi.
   - Screenshot hasil perhitungan dan simpan di:
     ```
     praktikum/week5-scheduling-fcfs-sjf/screenshots/
     ```

5. **Analisis**
   - Bandingkan hasil rata-rata WT dan TAT antara FCFS & SJF.  
   - Jelaskan kondisi kapan SJF lebih unggul dari FCFS dan sebaliknya.  
   - Tambahkan kesimpulan singkat di akhir laporan.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 5 - CPU Scheduling FCFS & SJF"
   git push origin main
   ```
   
---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](<screenshots/eksperimen1_fcfs_dan_sjf>)

---

## Analisis Hasil
**Eksperimen 1 – FCFS (First Come First Served)**
- Urutkan proses berdasarkan *Arrival Time*. 

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---

## Tugas
1. Hitung *waiting time* dan *turnaround time* dari minimal 2 skenario FCFS dan SJF.  
2. Sajikan hasil perhitungan dalam tabel perbandingan (FCFS vs SJF).  
3. Analisis kelebihan dan kelemahan tiap algoritma.  
4. Simpan seluruh hasil dan analisis ke `laporan.md`.  

---

## Quiz
1. Apa perbedaan utama antara FCFS dan SJF?
   Jawaban: Perbedaan utama terletak di penjadwalan eksekusi. FCFS mengekskusi proses berdasarkan urutan waktu kedatangannya, sedangkan SJF mengekskusi proses dengan melihat waktu eksekusi yang paling singkat/paling cepat terselesaikan.
2. Mengapa SJF dapat menghasilkan rata-rata waktu tunggu minimum?
   Jawaban: SJF menghasilkan rata rata waktu tunggu minimum, karena menjalankan proses yang memiliki waktu eksekusi paling singkat. Dengan begitu, proses-proses yang memiliki waktu eksekusi singkat bisa cepat selesai tanpa menunggu proses panjang. Sehingga rata-rata waktu tunggu keseluruhan  menjadi lebih minimum dan efisien.
4. Apa kelemahan SJF jika diterapkan pada sistem interaktif?
   Jawaban: Algoritma ini sulit diterapkan pada sistem interaktif karena sulit menebak berapa lama proses berjalan. Pada sistem interaktif proses datang secara acak dan burst time nya tidak dapat diprediksi dengan pasti. Akibatnya sistem bisa salah menentukan urutan eksekusi dan untuk proses dengan burst time panjang bisa tertunda terus menerus karena selalu kalah prioritas dengan proses yang lebih singkat, sehingga sistem menjadi kurang responsif dan kurang adil terhadap kebutuhan pengguna.
---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
