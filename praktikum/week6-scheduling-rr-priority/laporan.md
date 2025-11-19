
# Laporan Praktikum Minggu [6]
Topik: Penjadwalan CPU – Round Robin (RR) dan Priority Scheduling

---

## Identitas
- **Nama**  : Belinda Lani Regina 
- **NIM**   : 250320576
- **Kelas** : 1DSRA

---

## Tujuan
> 1. Dapat menghitung waiting time dan turnaround time pada algoritma RR dan Priority.
> 2. Dapatenyusun tabel hasil perhitungan dengan benar dan sistematis.
> 3. Dapat membandingkan performa algoritma RR dan Priority.
> 4. Dapat menjelaskan pengaruh time quantum dan prioritas terhadap keadilan eksekusi proses.
> 5. Dapat menarik kesimpulan mengenai efisiensi dan keadilan kedua algoritma.

---

## Dasar Teori
1. Round Robin (RR) adalah algoritma preemptive yang menggunakan time quantum untuk membagi CPU secara adil kepada setiap proses; cocok untuk sistem time-sharing karena memberikan respons cepat dan teratur (Silberschatz et al., 2018; Tanenbaum & Bos, 2015).
2. Efektivitas RR sangat bergantung pada pemilihan quantum: terlalu kecil menyebabkan context switching tinggi, terlalu besar membuatnya menyerupai FCFS (OSTEP, 2018).
3. Priority Scheduling menjalankan proses berdasarkan tingkat prioritas, baik secara preemptive maupun non-preemptive, sehingga proses penting dapat dieksekusi lebih cepat (Silberschatz et al., 2018).
5. Algoritma prioritas dapat menimbulkan starvation untuk proses berprioritas rendah; solusi yang umum diterapkan adalah aging, yaitu menaikkan prioritas proses yang menunggu lama (Tanenbaum & Bos, 2015).
---

## Langkah Praktikum
1. Siapkan Data Proses Gunakan contoh data berikut (boleh dimodifikasi sesuai kebutuhan):

| Proses | Burst Time | Arrival Time | Priority |
| ------ | ---------- | ------------ | -------- |
| P1     | 5          | 0            | 2        |
| P2     | 3          | 1            | 1        |
| P3     | 8          | 2            | 4        |
| P4     | 6          | 3            | 3        |

2. Eksperimen 1 – Round Robin (RR)
   - Gunakan time quantum (q) = 3.
   - Hitung waiting time dan turnaround time untuk tiap proses.
   - Simulasikan eksekusi menggunakan Gantt Chart (manual atau spreadsheet).
```
| P1 | P2 | P3 | P4 | P1 | P3 | ...
0    3    6    9   12   15   18  ...
```
   - Catat sisa burst time tiap putaran.

3. Eksperimen 2 – Priority Scheduling (Non-Preemptive)
   - Urutkan proses berdasarkan nilai prioritas (angka kecil = prioritas tinggi).
   - Lakukan perhitungan manual untuk:
```
WT[i] = waktu mulai eksekusi - Arrival[i]
TAT[i] = WT[i] + Burst[i]
```
   - Buat tabel perbandingan hasil RR dan Priority.
     
4. Eksperimen 3 – Analisis Variasi Time Quantum (Opsional)
   - Ubah quantum menjadi 2 dan 5.
   - Amati perubahan nilai rata-rata waiting time dan turnaround time.
   - Buat tabel perbandingan efek quantum.
     
5. Eksperimen 4 – Dokumentasi
   - Simpan semua hasil tabel dan screenshot ke:
```
praktikum/week6-scheduling-rr-priority/screenshots/
```
  - Buat tabel perbandingan seperti berikut:
     
| Algoritma                 | Avg Waiting Time | Avg Turnaround Time | Kelebihan                    | Kekurangan                               |
| ------------------------- | ---------------: | ------------------: | ---------------------------- | ---------------------------------------- |
| RR (q=2)                  |             9.75 |               15.25 | Adil terhadap semua proses   | Tidak efisien jika quantum tidak tepat   |
| Priority (non-preemptive) |             5.25 |               10.75 | Efisien untuk proses penting | Potensi starvation pada prioritas rendah |

6. Commit & Push
```
git add .
git commit -m "Minggu 6 - CPU Scheduling RR & Priority"
git push origin main
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
1. Eksperimen 1

   - Round Robin (RR)

| Proses        | Burst Time | Arrival Time | Priority | Finish (P1) | Finish (P2)  | Finish (P3)  | WT      | TAT    |
| ------------- | ---------- | ------------ | -------- | ----------- | ------------ | ------------ | ------- | ------ |
| **P1**        | 5          | 0            | 2        | 3 (sisa 2)  | 14 (selesai) |       -      | 9       | 14     |
| **P2**        | 3          | 1            | 1        | 6 (selesai) |       -      |       -      | 2       | 5      |
| **P3**        | 8          | 2            | 4        | 9 (sisa 5)  | 17 (sisa 2)  | 22 (selesai) | 12      | 20     |
| **P4**        | 6          | 3            | 3        | 12 (sisa 3) | 20 (selesai) |       -      | 11      | 17     |
| **Jumlah**    |            |              |          |             |              |              | **34**  | **46** |
| **Rata-rata** |            |              |          |             |              |              | **8,5** | **14** |
```
| P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
0    3    6    9   12   14   17    20   22
```

2. Eksperimen 2

- Priority Scheduling

| Proses        | Burst Time | Arrival Time | Priority | Start | Finish | WT       | TAT       |
| ------------- | ---------- | ------------ | -------- | ----- | ------ | -------- | --------- |
| P1            | 5          | 0            | 2        | 0     | 5      | 0        | 5         |
| P2            | 3          | 1            | 1        | 5     | 8      | 4        | 7         |
| P3            | 6          | 3            | 4        | 8     | 14     | 5        | 11        |
| P4            | 8          | 2            | 3        | 14    | 22     | 12       | 20        |
| **Jumlah**    |            |              |          |       |        | **21**   | **43**    |
| **Rata-rata** |            |              |          |       |        | **5,25** | **10,75** |

```
|  P1  |  P2  |  P3  |  P4  |
0      5      8      14     22
```

- Tabel perbandingan hasil RR dan Priority
     
| Parameter                        | Round Robin (RR)                      | Priority Scheduling                               |
| -------------------------------- | ------------------------------------- | ------------------------------------------------- |
| Rata-rata Waiting Time (WT)      | **8,5**                               | **5,25**                                          |
| Rata-rata Turn Around Time (TAT) | **14**                                | **10,75**                                         |
| Jenis                            | Preemptive                            | Non-preemptive                                    |
| Kelebihan                        | Adil, setiap proses dapat jatah waktu | Waktu selesai cepat untuk proses prioritas tinggi |
| Kekurangan                       | Bisa menyebabkan waiting time besar   | Proses prioritas rendah menunggu sangat lama      |


3. Eksperimen 3

- Quantum 2
  
| **Proses**    | **Burst Time** | **Arrival Time** | **Priority** | **Finish (P1)** | **Finish (P2)** | **Finish (P3)** | **Finish (P4)** | **WT**    | **TAT**   |
| ------------- | -------------- | ---------------- | ------------ | --------------- | --------------- | --------------- | --------------- | --------- | --------- |
| **P1**        | 5              | 0                | 2            | 2               | 10              | 16              | Selesai         | 16        | 11        |
| **P2**        | 3              | 1                | 1            | 4               | 11              | Selesai         | Selesai         | 10        | 7         |
| **P3**        | 8              | 2                | 4            | 6               | 13              | 18              | 22              | 20        | 12        |
| **P4**        | 6              | 3                | 3            | 8               | 15              | 20              | Selesai         | 17        | 11        |
| **Jumlah**    |                |                  |              |                 |                 |                 |                 | **63**    | **41**    |
| **Rata-rata** |                |                  |              |                 |                 |                 |                 | **15,75** | **10,25** |

```
| P1 | P2 | P3 | P1 | P4 | P3 | P4 | P3 |
0    3    6    9    11   14   17   20   22
```

- Quantum 5
  
| **Proses**    | **Burst Time** | **Arrival Time** | **Priority** | **Start** | **Finish** | **Finish (P2)** | **WT**   | **TAT** |
| ------------- | -------------- | ---------------- | ------------ | --------- | ---------- | --------------- | -------- | ------- |
| **P1**        | 5              | 0                | 2            | 0         | 5          | Selesai         | 5        | 0       |
| **P2**        | 3              | 1                | 1            | 5         | 8          | Selesai         | 7        | 4       |
| **P3**        | 8              | 2                | 4            | 8         | 13         | 21              | 19       | 13      |
| **P4**        | 6              | 3                | 3            | 14        | 18         | 22              | 19       | 11      |
| **Jumlah**    |                |                  |              |           |            |                 | **50**   | **28**  |
| **Rata-rata** |                |                  |              |           |            |                 | **12,5** | **7**   |

```
| P1 | P2 | P4 | P3 |
0    5    8   14    22
```

- Tabel perbandingan efek quantum.

| **Quantum**             | **Context Switching**     | **WT (Waktu Tunggu)** | **TAT (Waktu Penyelesaian)** | **Karakteristik**                                                          |
| ----------------------- | ------------------------- | --------------------- | ---------------------------- | -------------------------------------------------------------------------- |
| **Quantum = 2 (kecil)** | Banyak (frekuensi tinggi) | Lebih tinggi          | Lebih tinggi                 | Algoritma lebih adil, tapi boros waktu karena sering berpindah proses      |
| **Quantum = 5 (besar)** | Lebih sedikit             | Lebih rendah          | Lebih rendah                 | Lebih efisien, mirip FCFS karena proses berjalan lebih lama tanpa terputus |

4. Eksperimen 4

| Algoritma                 | Avg Waiting Time | Avg Turnaround Time | Kelebihan                    | Kekurangan                               |
| ------------------------- | ---------------: | ------------------: | ---------------------------- | ---------------------------------------- |
| RR (q=2)                  |             9.75 |               15.25 | Adil terhadap semua proses   | Tidak efisien jika quantum tidak tepat   |
| Priority (non-preemptive) |             5.25 |               10.75 | Efisien untuk proses penting | Potensi starvation pada prioritas rendah |
---

## Kesimpulan
1. Round Robin dan Priority Scheduling sama-sama efektif, tetapi digunakan untuk kebutuhan berbeda: RR cocok untuk sistem time-sharing yang menuntut keadilan, sedangkan Priority Scheduling cocok untuk mengeksekusi proses penting terlebih dahulu.
2. Pemilihan quantum pada RR sangat krusial karena memengaruhi efisiensi: quantum terlalu kecil meningkatkan context switching, sedangkan quantum besar membuat RR menyerupai FCFS.
3. Priority Scheduling berisiko menyebabkan starvation, sehingga teknik aging perlu diterapkan agar proses berprioritas rendah tetap mendapat kesempatan dieksekusi.

---

## Tugas 
- Perbandingan Performa dan jelaskan pengaruh time quantum serta prioritas

| **Aspek**                | **Time Quantum**                                                                                          | **Prioritas**                                                                                                  |
| ------------------------ | --------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Parameter**            | Ukuran waktu yang dialokasikan untuk setiap proses dalam RR                                               | Nilai yang menentukan urutan eksekusi proses                                                                   |
| **Pengaruh Utama**       | Trade-off antara responsivitas dan overhead                                                               | Trade-off antara fairness dan starvation                                                                       |
| **Nilai Kecil**          | - Responsivitas tinggi<br>- Banyak context switching<br>- Overhead tinggi                                 | - Fairness tinggi<br>- Tidak ada starvation<br>- Mirip FCFS                                                    |
| **Nilai Besar**          | - Overhead rendah<br>- Responsivitas rendah<br>- Mirip FCFS                                               | - Efisiensi tinggi<br>- Potensi starvation<br>- Fairness rendah                                                |
| **Keuntungan**           | - Tidak ada starvation<br>- Fair<br>- Responsif untuk aplikasi interaktif                                 | - Throughput lebih baik<br>- Cocok untuk real-time s                                                           |


## Quiz
1. Apa perbedaan utama antara Round Robin dan Priority Scheduling?
```
   Jawaban: Perbedaan utama antara Round dan Priority Scheduling yaitu jika Round-Robin (RR) mengeksekusi proses berdasarkan kuantum waktu yang ditentukan, yaitu setiap proses dieksekusi selama jangka waktu yang tetap. Sedangkan penjadwalan Prioritas mengeksekusi proses berdasarkan prioritas, yaitu proses dengan prioritas lebih tinggi dieksekusi terlebih dahulu.
```
3. Apa pengaruh besar/kecilnya time quantum terhadap performa sistem?
```
   Jawaban: Pengaruh besar/kecilnya time quantum terhadap performa sistem adalah jika kuantum waktu terlalu besar, waktu respons proses akan terlalu lama, yang mungkin tidak dapat ditoleransi dalam lingkungan interaktif. Jika kuantum waktu terlalu kecil, hal ini menyebabkan pergantian konteks yang terlalu sering dan tidak perlu, sehingga mengakibatkan lebih banyak overhead yang mengakibatkan throughput yang lebih rendah .
```
5. Mengapa algoritma Priority dapat menyebabkan starvation?
```
   Jawaban: Algoritma Priority dapat menyebabkan starvation karena proses berprioritas rendah terus menunggu tanpa batas waktu karena proses berprioritas lebih tinggi terus-menerus mendapatkan CPU. Masalah ini muncul dalam sistem yang memiliki beban berat di mana sumber daya selalu ditempati oleh tugas-tugas berprioritas tinggi, yang menyebabkan beberapa proses kekurangan sumber daya. Jika selalu ada proses berprioritas tinggi yang tersedia, proses berprioritas rendah mungkin tidak akan pernah diizinkan untuk berjalan. Selain prioritas, ada penyebab lain seperti algoritma penjadwalan yang memilih proses secara acak dan entah bagaimana proses korban selalu terlewatkan, yang menyebabkan starvation. 
```
---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  Bagian yang paling menantang minggu ini adalah cara menjalankan atau menghitung (bingung) round robin.
- Bagaimana cara Anda mengatasinya?  
  Cara saya mengatasinya yaitu dengan mecari referensi pembelajaran.
---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
