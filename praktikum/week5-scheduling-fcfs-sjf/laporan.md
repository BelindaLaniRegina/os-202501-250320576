
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
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

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
