
# Laporan Praktikum Minggu [5]
Topik: Scheduling FCFS SJF

---

## Identitas
- **Nama**  : [Belinda Lani Regina]  
- **NIM**   : [250320576]  
- **Kelas** : [1DSRA]

---

## Tujuan
> 1. Dapat menghitung waiting time dan turnaround time untuk algoritma FCFS dan SJF.
> 2. Dapat menyajikan hasil perhitungan dalam tabel yang rapi dan mudah dibaca.
> 3. Dapat membandingkan performa FCFS dan SJF berdasarkan hasil analisis.
> 4. Dapat menjelaskan kelebihan dan kekurangan masing-masing algoritma.
> 5. Dapat menyimpulkan kapan algoritma FCFS atau SJF lebih sesuai digunakan.

---

## Dasar Teori
1. Konsep Penjadwalan CPU, penjadwalan CPU menentukan urutan eksekusi proses untuk memaksimalkan efisiensi sistem dan pemanfaatan prosesor (Silberschatz et al., 2018).
2. Algoritma FCFS (First Come, First Served), menjalankan proses sesuai urutan kedatangan. Sederhana namun dapat menyebabkan convoy effect ketika proses panjang menghambat proses lain (Tanenbaum & Bos, 2015).
3. Algoritma SJF (Shortest Job First), memilih proses dengan waktu eksekusi terpendek terlebih dahulu. Memberikan average waiting time terbaik, tetapi dapat menyebabkan starvation untuk proses panjang (Silberschatz et al., 2018; OSTEP, 2018).
4. Evaluasi Kinerja, kinerja algoritma diukur melalui waiting time dan turnaround time rata-rata untuk menentukan efisiensi (Silberschatz et al., 2018).

---

## Langkah Praktikum
1. Siapkan Data Proses Gunakan tabel proses berikut sebagai contoh (boleh dimodifikasi dengan data baru):

| **Proses** | **Burst Time** | **Arrival Time** |
| :--------- | :------------: | :--------------: |
| P1         |        6       |         0        |
| P2         |        8       |         1        |
| P3         |        7       |         2        |
| P4         |        3       |         3        |

2. **Eksperimen 1 – FCFS (First Come First Served)**
   
   - Urutkan proses berdasarkan Arrival Time.
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
   
   - Urutkan proses berdasarkan Burst Time terpendek (dengan memperhatikan waktu kedatangan).
   - Lakukan perhitungan WT dan TAT seperti langkah sebelumnya.
   - Bandingkan hasil FCFS dan SJF pada tabel berikut:

| **Algoritma** | **Avg Waiting Time** | **Avg Turnaround Time** | **Kelebihan**                  | **Kekurangan**                            |
| :------------ | :------------------: | :---------------------: | :----------------------------- | :---------------------------------------- |
| FCFS          |         ...          |           ...           | Sederhana dan mudah diterapkan | Tidak efisien untuk proses panjang        |
| SJF           |         ...          |           ...           | Optimal untuk job pendek       | Menyebabkan *starvation* pada job panjang |

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
```
git add .
git commit -m "Minggu 5 - CPU Scheduling FCFS & SJF"
git push origin main
```
---

## Hasil Eksekusi
S![alt text](<screenshots/Sheduling FCFS dan SJF.png>)

---

## Analisis
- Jelaskan makna hasil percobaan.  
```
Makna Hasil FCFS (First Come First Served)
- Proses dijalankan berdasarkan urutan kedatangan (Arrival Time).
- Proses yang datang lebih dulu akan dieksekusi lebih dulu tanpa memperhatikan waktu eksekusi (Burst Time).
Dari tabel:
- Urutan eksekusi: P1 → P2 → P3 → P4
- Waktu tunggu rata-rata = 8,75
- Turnaround time rata-rata = 14,75
Jadi, dapat dikatakan bahwa FCFS sederhana namun kurang efisien jika ada proses dengan waktu eksekusi panjang datang lebih dulu, proses lain harus menunggu lama (efek convoy). Akibatnya, waiting time dan turnaround time rata-rata menjadi tinggi.

Makna Hasil SJF (Shortest Job First)
- Proses dijalankan berdasarkan Burst Time paling pendek di antara proses yang sudah datang.
Dari tabel:
- Urutan eksekusi: P1 → P2 → P3 → P4
- Waktu tunggu rata-rata = 6,25
- Turnaround time rata-rata = 12,25
Jadi, dapat dikatakan bahwa dengan memilih proses berdurasi pendek terlebih dahulu, total waktu tunggu dan turnaround menjadi lebih kecil. Algoritma ini lebih efisien daripada FCFS dalam rata-rata waktu eksekusi. Namun, kekurangannya adalah jika proses pendek terus datang, proses panjang bisa tertunda (starvation).
```
---

## Kesimpulan
1. Algoritma SJF lebih efisien dibandingkan FCFS karena menghasilkan waktu tunggu dan turnaround time rata-rata yang lebih rendah.
2. FCFS memiliki kelemahan convoy effect, yaitu proses dengan burst time pendek harus menunggu proses panjang selesai terlebih dahulu.
3. Pemilihan algoritma penjadwalan yang tepat sangat berpengaruh terhadap kinerja sistem, terutama dalam hal efisiensi waktu dan pemanfaatan CPU.
---

## Tugas
1. Hitung waiting time dan turnaround time dari minimal 2 skenario FCFS dan SJF
- Skenario 1
  - FCFS
\
  Waiting Time: 8,75
\
Turnaround Time: 14,75

  - SJF
\
  Waiting Time: 6,25
\
Turnaround Time: 12,25

- Skenario 2
  - FCFS
\
  Waiting Time: 3,75
\
Turnaround Time: 7,25

  - SJF
\
  Waiting Time: 3,25
\
Turnaround Time: 6,75


2. Sajikan hasil perhitungan dalam tabel perbandingan (FCFS vs SJF).
   
 FCFS
     
| **Proses**    | **Burst Time** | **Arrival Time** | **Start** | **Waiting Time** | **Turnaround Time** | **Finish** |
| ------------- | -------------- | ---------------- | --------- | ---------------- | ------------------- | ---------- |
| P1            | 6              | 0                | 0         | 0                | 6                   | 6          |
| P2            | 8              | 1                | 6         | 5                | 13                  | 14         |
| P3            | 7              | 2                | 14        | 12               | 19                  | 21         |
| P4            | 3              | 3                | 21        | 18               | 21                  | 24         |
| **Total**     |                |                  |           | **35**           | **59**              |            |
| **Rata-Rata** |                |                  |           | **8,75**         | **14,75**           |            |

   SJF
   
| **Proses**    | **Burst Time** | **Arrival Time** | **Start** | **Waiting Time** | **Turnaround Time** | **Finish** |
| ------------- | -------------- | ---------------- | --------- | ---------------- | ------------------- | ---------- |
| P1            | 6              | 0                | 0         | 0                | 6                   | 6          |
| P2            | 3              | 3                | 6         | 3                | 6                   | 9          |
| P3            | 7              | 2                | 9         | 7                | 14                  | 16         |
| P4            | 8              | 1                | 16        | 15               | 23                  | 24         |
| **Total**     |                |                  |           | **25**           | **49**              |            |
| **Rata-Rata** |                |                  |           | **6,25**         | **12,25**           |            |

 - Skenario 2

  FCFS

| **Proses**    | **Burst Time** | **Arrival Time** | **Start** | **Waiting Time** | **Turnaround Time** | **Finish** |
| ------------- | -------------- | ---------------- | --------- | ---------------- | ------------------- | ---------- |
| P1            | 4              | 0                | 0         | 0                | 4                   | 4          |
| P2            | 2              | 1                | 4         | 3                | 5                   | 6          |
| P3            | 5              | 2                | 6         | 4                | 9                   | 11         |
| P4            | 3              | 3                | 11        | 8                | 11                  | 14         |
| **Total**     |                |                  |           | **15**           | **29**              |            |
| **Rata-Rata** |                |                  |           | **3,75**         | **7,25**            |            |

SJF

| **Proses**    | **Burst Time** | **Arrival Time** | **Start** | **Waiting Time** | **Turnaround Time** | **Finish** |
| ------------- | -------------- | ---------------- | --------- | ---------------- | ------------------- | ---------- |
| P1            | 4              | 0                | 0         | 0                | 4                   | 4          |
| P2            | 2              | 3                | 4         | 1                | 3                   | 6          |
| P3            | 3              | 2                | 6         | 4                | 7                   | 9          |
| P4            | 5              | 1                | 9         | 8                | 13                  | 14         |
| **Total**     |                |                  |           | **13**           | **27**              |            |
| **Rata-Rata** |                |                  |           | **3,25**         | **6,75**            |            |


3. Analisis kelebihan dan kelemahan tiap algoritma!

| **Algoritma**                      | **Kelebihan**                                                                                                      | **Kelemahan**                                                                                                                                             |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **FCFS (First Come First Served)** | - Algoritma yang paling sederhana.<br>- Skemanya adil karena proses yang datang lebih dulu mendapat prioritas CPU. | - Terjadi *convoy effect*, yaitu proses kecil harus menunggu proses besar selesai.<br>- Tidak efisien untuk sistem dengan banyak proses kecil.            |
| **SJF (Shortest Job First)**       | - Paling optimal karena memberikan **minimum waiting time** untuk kumpulan proses yang mengantri.                  | - Tidak dapat digunakan untuk **penjadwalan CPU short-term** secara efektif.<br>- Sulit diterapkan jika waktu eksekusi proses tidak diketahui sebelumnya. |




## Quiz
1. Apa perbedaan utama antara FCFS dan SJF?
   **Jawaban: Perbedaan utama antara FCFS dan SJF yaitu jika FCFS bisa diartikan sebagai Proses yg tiba lebih dahulu akan dilayani lebih dahulu.Kalau ada proses tiba pada waktu yg sama, maka pelayanan mereka dilaksanakan melalui urutan mereka dalam antrian.Proses di antrian belakang harus menunggu sampai semua proses di depannya selesai.Setiap proses yang berada pada status ready dimasukkan ke dalam FCFS queue sesuai dengan waktu kedatangannya. Sedangkan SJF Setiap proses yang ada di ready queue akan dieksekusi berdasarkan burst time terkecil.
Mengakibatkan waiting time yang pendek untuk setiap proses dan waiting time rata-ratanya juga menjadi pendek, sehingga dapat dikatakan ini adalah algoritma yang optimal.**  
3. Mengapa SJF dapat menghasilkan rata-rata waktu tunggu minimum?  
   **Jawaban: Karena SJF adalah teknik penjadwalan bertujuan untuk meningkatkan efisiensi dan kinerja sistem. Algoritma ini bersifat non-preemptif, artinya setelah suatu proses mulai dieksekusi, proses tersebut tidak dapat diinterupsi hingga selesai. Ide dasar di balik algoritma SJF adalah memprioritaskan eksekusi proses dengan waktu burst terpendek atau waktu CPU yang dibutuhkan paling sedikit. Dengan demikian, algoritma meminimalkan waktu tunggu rata-rata dan waktu penyelesaian untuk proses-proses dalam antrean, sehingga menghasilkan kinerja sistem yang lebih baik secara keseluruhan dan menghasilkan rata-rata minimum.**  
4. Apa kelemahan SJF jika diterapkan pada sistem interaktif?  
   **Jawaban: Kelemahan SJF jika diterapkan pada sistem interaktif adalah sifat non-preemptifnya, yang dapat menyebabkan proses yang lebih panjang jika selalu ada proses yang lebih pendek yang tiba dalam antrean. Selain itu, memprediksi waktu burst suatu proses dapat menjadi tantangan dalam skenario dunia nyata, sehingga implementasi praktis algoritma SJF menjadi kurang efektif.**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  - Yang paling menantang minggu ini menurut saya adalah cara menentukan start dan finish di SJF. 
- Bagaimana cara Anda mengatasinya?
  - Cara saya mengatasinya yaitu dengan mencoba memahaminya dari sumber-sumber yang saya dapatkan juga meminta diajarkan oleh teman saya yang sudah mengerti.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
