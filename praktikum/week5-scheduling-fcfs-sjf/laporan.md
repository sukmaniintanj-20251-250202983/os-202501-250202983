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
![Screenshot hasil](<screenshots/eksperimen_fcfs_sjf.png>)

---

## Analisis Hasil
- **Proses berdasarkan *Arrival Time***

|Process|Arrival Time|Burst Time|Start Time|Finish Time|Waiting Time|Turnaround Time (TAT)|
|:-------:|:------------:|:----------:|:----------:|:-----------:|:------------:|:---------------------:|
|P1|0|6|0|6|0|6|
|P2|1|8|6|14|5|13|
|P3|2|7|14|21|12|19|
|P4|3|3|21|24|18|21|

Rata-rata Waiting Time = 8.75   
Rata-rata Turnaround Time = 14.75   
Gantt Chart :

```
| P1 |   P2   |   P3   | P4 |
0     6       14       21  24
```
- **Proses berdasarkan *Burst Time***

|Process|Arrival Time|Burst Time|Start Time|Finish Time|Waiting Time|Turnaround Time (TAT)|
|:-------:|:------------:|:----------:|:----------:|:-----------:|:------------:|:---------------------:|
|P1|0|6|0|6|0|6|
|P4|3|3|6|9|3|6|
|P3|2|7|9|16|7|14|
|P2|1|8|16|24|15|23|

Rata-rata Waiting Time = 6.25   
Rata-rata Turnaround Time = 12.25   
Gantt Chart :

```
| P1 | P4 |   P3   |   P2   |
0     6    9       16       24
```
- **Perbandingan hasil rata-rata WT dan TAT antara FCFS dan SJF**

|Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
|------------|------------------|----------------------|------------|-------------|
| FCFS | 8.75 | 14.75 | Sederhana dan mudah diterapkan | Tidak efisien untuk proses panjang |
| SJF | 6.25 | 12.25 | Optimal untuk job pendek | Menyebabkan *starvation* pada job panjang |

---
  
- **Jelaskan kondisi kapan SJF lebih unggul dari FCFS dan sebaliknya**  
  Berdasarkan hasil perhitungan pada data diatas, algoritma FCFS memiliki rata-rata waiting time sebesar 8.75 dan turnaround time sebesar 14.75, sedangkan algoritma SJF memiliki rata-rata waiting time sebesar 6.25 dan turnaround time sebesar 12.25. Perbedaan tersebut memperlihatkan SJF lebih unggul dalam hal efisiensi waktu, kondisi ini terjadi karena pada SJF, proses dengan waktu eksekusi pendek seperti P4 (burst time = 3) dapat langsung dijalankan setelah P1, sehingga proses lain tidak menunggu terlalu lama. Akibatnya, total waktu tunggu seluruh proses menjadi lebih singkat.

   Sebaliknya, algoritma FCFS akan lebih unggul jika setiap proses memiliki waktu eksekusi yang hampir sama atau jika sistem menuntut keadilan urutan. Berdasarkan data, FCFS menjalankan proses sesuai urutan kedatangan, yaitu P1 → P2 → P3 → P4, sehingga tidak ada proses yang dilewati. Namun karena P2 memiliki burst time cukup panjang (8), proses lain seperti P3 dan P4 jadi menunggu lama, menyebabkan waktu tunggu rata-rata meningkat.


## Kesimpulan
1. Berdasarkan hasil perhitungan pada praktikum, SJF memiliki rata-rata waktu tunggu (6.25) dan waktu penyelesaian (12.25) yang lebih rendah dibanding FCFS dengan rata-rata waktu tunggu (8.75) dan waktu penyelesaian (14.75). Hal ini menunjukkan bahwa SJF lebih efisien dalam mengelola proses dengan variasi burst time yang berbeda-beda.
2. FCFS tetap unggul untuk sistem yang menuntut keadilan dan kestabilan, karena setiap proses dieksekusi sesuai urutan kedatangan tanpa ada yang diabaikan.
3. Secara umum, pemilihan algoritma CPU scheduling bergantung pada kebutuhan sistem. Gunakan SJF untuk efisiensi waktu dan FCFS untuk keadilan antar proses.


---

## Tugas
- **Hasil hitung *waiting time* dan *turnaround time* dari minimal 2 skenario FCFS dan SJF.**
![Screenshot hasil](<screenshots/skenario_1.png>)
![Screenshot hasil](<screenshots/skenario_2.png>)
Pada skenario 2, semua proses mempunyai arrival time = 0, dan memiliki nilai rata-rata FCFS dan SJF berbeda tipis karena semua proses datang bersamaan di awal.

- **Hasil perhitungan, analisis kelebihan dan kekurangan dalam tabel perbandingan (FCFS vs SJF).**  

   Skenario 1

   |Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
   |------------|------------------|----------------------|------------|-------------|
   | FCFS |6.75| 11.75 | Proses dikerjakan sesuai urutan kedatangan, sederhana dan mudah diterapkan | Kurang efisien saat ada proses panjang (contohnya P3 dengan burst 8), karena meningkatkan waktu tunggu proses lain |
   | SJF | 4.25 | 9.25 | Lebih efisien karena mengeksekusi proses dengan waktu terpendek lebih dulu, menurunkan rata-rata waktu tunggu dan penyelesaian. | Risiko starvation jika ada proses panjang yang terus tertunda (seperti P3) | 

   Skenario 2

   |Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
   |------------|------------------|----------------------|------------|-------------|
   | FCFS |4.33| 9.67 | Stabil dan adil, semua proses dijalankan sesuai urutan tanpa diprioritaskan | Tidak seefisien SJF karena urutan tidak mempertimbangkan durasi proses |
   | SJF | 3.67 | 9.00 | Lebih cepat menyelesaikan seluruh proses, cocok karena semua arrival time = 0 sehingga pemilihan proses pendek efektif | Kurang cocok jika proses datang tidak bersamaan karena bisa menyebabkan penundaan untuk proses panjang |

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
  Pada praktikum ini, saya merasa memahami algoritma SJF lebih sulit daripada FCFS, karena perlu memperhatikan lebih yaitu urutan proses berdasarkan waktu eksekusi terpendek dan waktu kedatangan secra bersamaan.
- Bagaimana cara Anda mengatasinya?
  Untuk mengatasinya, saya mencoba memahami ulang rumusnya beberapa kali dan melihat contoh kasus dari sumber lain

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
