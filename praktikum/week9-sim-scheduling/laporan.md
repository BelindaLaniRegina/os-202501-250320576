
# Laporan Praktikum Minggu [9]
Topik: Simulasi Algoritma Penjadwalan CPU
---

## Identitas
- **Nama**  : Belinda Lani Regina
- **NIM**   : 250320576
- **Kelas** : 1DSRA

---

## Tujuan
> 1. Dapat membuat program simulasi algoritma penjadwalan FCFS dan/atau SJF.
> 2. Dapat menjalankan program dengan dataset uji yang diberikan atau dibuat sendiri.
> 3. Dapat menyajikan output simulasi dalam bentuk tabel atau grafik.
> 4. Dapat menjelaskan hasil simulasi secara tertulis.
> 5. Dapat mengunggah kode dan laporan ke Git repository dengan rapi dan tepat waktu.

---

## Dasar Teori
> 1. CPU Scheduling bertujuan mengatur urutan eksekusi proses agar penggunaan CPU menjadi efisien dan waktu tunggu proses dapat diminimalkan.
> 2. FCFS (First Come First Served) mengeksekusi proses berdasarkan urutan kedatangan tanpa mempertimbangkan lama waktu eksekusi.
> 3. SJF (Shortest Job First) memilih proses dengan burst time paling kecil sehingga secara teori menghasilkan rata-rata waiting time paling minimum.
> 4. Waiting Time dan Turnaround Time merupakan metrik utama untuk mengevaluasi kinerja algoritma penjadwalan CPU.
> 5. Algoritma non-preemptive mengeksekusi proses hingga selesai sebelum berpindah ke proses lain, seperti yang diterapkan pada simulasi FCFS dan SJF.

---

## Langkah Praktikum
1. **Menyiapkan Dataset**

   Buat dataset proses minimal berisi:

   | Proses | Arrival Time | Burst Time |
   |:--:|:--:|:--:|
   | P1 | 0 | 6 |
   | P2 | 1 | 8 |
   | P3 | 2 | 7 |
   | P4 | 3 | 3 |

2. **Implementasi Algoritma**

   Program harus:
   - Menghitung *waiting time* dan *turnaround time*.  
   - Mendukung minimal **1 algoritma (FCFS atau SJF non-preemptive)**.  
   - Menampilkan hasil dalam tabel.

3. **Eksekusi & Validasi**

   - Jalankan program menggunakan dataset uji.  
   - Pastikan hasil sesuai dengan perhitungan manual minggu sebelumnya.  
   - Simpan hasil eksekusi (screenshot).

4. **Analisis**

   - Jelaskan alur program.  
   - Bandingkan hasil simulasi dengan perhitungan manual.  
   - Jelaskan kelebihan dan keterbatasan simulasi.

5. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 9 - Simulasi Scheduling CPU"
   git push origin main


## Kode / Perintah
1. Menghitung waiting time dan turnaround time FCFS
```
def main():
    proses_list = [
        {'id': 'P1', 'arrival': 0, 'burst': 6},
        {'id': 'P2', 'arrival': 1, 'burst': 8},
        {'id': 'P3', 'arrival': 2, 'burst': 7},
        {'id': 'P4', 'arrival': 3, 'burst': 3},
    ]

    proses_list.sort(key=lambda x: x['arrival'])

    waktu_sekarang = 0
    total_waiting = 0
    total_turnaround = 0

    print("\n=== SIMULASI CPU SCHEDULING (FCFS) ===")
    print(f"{'Proses':<8} {'Arrival':<8} {'Burst':<8} {'Waiting':<8} {'Turnaround':<10}")
    print("-" * 50)

    for p in proses_list:
        if waktu_sekarang < p['arrival']:
            waktu_sekarang = p['arrival']

        start_time = waktu_sekarang
        finish_time = start_time + p['burst']

        turnaround = finish_time - p['arrival']
        waiting = turnaround - p['burst']

        total_waiting += waiting
        total_turnaround += turnaround
        
        waktu_sekarang = finish_time

        print(f"{p['id']:<8} {p['arrival']:<8} {p['burst']:<8} {waiting:<8} {turnaround:<10}")

    rata_waiting = total_waiting / len(proses_list)
    rata_turnaround = total_turnaround / len(proses_list)

    print("-" * 50)
    print(f"Rata-rata Waiting Time    : {rata_waiting:.2f} ms")
    print(f"Rata-rata Turnaround Time : {rata_turnaround:.2f} ms")
    print("=" * 50 + "\n")

if __name__ == "__main__":
    main()
   
```
2.  Menghitung waiting time dan turnaround time SJF
```
#Menghitung waiting time dan turnaround time SJF
def main():
    proses_list = [
        {'id': 'P1', 'arrival': 0, 'burst': 6},
        {'id': 'P2', 'arrival': 1, 'burst': 8},
        {'id': 'P3', 'arrival': 2, 'burst': 7},
        {'id': 'P4', 'arrival': 3, 'burst': 3},
    ]

    waktu_sekarang = 0
    total_waiting = 0
    total_turnaround = 0
    selesai = []

    print("\n=== SIMULASI CPU SCHEDULING (SJF) ===")
    print("-" * 80)
    print(f"{'Proses':<8} {'Arrival':<8} {'Burst':<8} {'Waiting':<8} {'Turnaround':<10}")
    print("-" * 80)

    while len(selesai) < len(proses_list):
        siap = []
        for p in proses_list:
            if p['arrival'] <= waktu_sekarang and p not in selesai:
                siap.append(p)

        if not siap:
            waktu_sekarang += 1
            continue

        p = min(siap, key=lambda x: x['burst'])

        start_time = waktu_sekarang
        finish_time = start_time + p["burst"]

        turnaround = finish_time - p['arrival']
        waiting = turnaround - p['burst']

        total_waiting += waiting
        total_turnaround += turnaround
        
        waktu_sekarang = finish_time
        selesai.append(p)

        print(f"{p['id']:<8} {p['arrival']:<8} {p['burst']:<8} {waiting:<8} {turnaround:<10}")

    rata_waiting = total_waiting / len(proses_list)
    rata_turnaround = total_turnaround / len(proses_list)

    print("-" * 80)
    print(f"Rata-rata Waiting Time    : {rata_waiting:.2f} ms")
    print(f"Rata-rata Turnaround Time : {rata_turnaround:.2f} ms")

if __name__ == "__main__":
    main()
```

---

## Hasil Eksekusi
1. FCFS
![alt text](<screenshots/week9_1.png>)
2. SJF
![alt text](<screenshots/week9_3.png>)

---

## Analisis
1. Alur Program
```
1. Datasetnya dibuat terlebih dahulu,
2. Setelah itu jika FCFS data proses diurutkan berdasarkan arrival time, sedangkan SJF pilih proses berdasarkan burst time terpendek,
3. Jika sudah CPU akan mengeksekusi proses,
4. Lalu hitung waiting & turnaround time tiap proses,
5. Setelah itu hitung rata-rata waktu,
6. Jika sudah semua yang terkhir adalah mempilkan hasil simulasi.
```
2. Perbandingan hasil simulasi dengan perhitungan manual
- FCFS
  - Perhitungan Manual
    
    ![alt text](<screenshots/week9_2.png>)
  - Hasil simulasi
    
    ![alt text](<screenshots/week9_5.png>)
- SJF
  - Perhitungan Manual
  
     ![alt text](<screenshots/week9_4.png>)
  - Hasil simulasi
    
    ![alt text](<screenshots/week9_6.png>)

3.  Kelebihan dan keterbatasan simulasi.
```
- Kelebihan
    1. Perhitungan waiting time dan turnaround time jelas
    2. Memudahkan perbandingan algoritma FCFS dan SJF.
    3. Mudah dimodifikasi ke algoritma penjadwalan lain.
- Keterbatasan
    1. SJF berpotensi menimbulkan starvation pada proses dengan burst time besar.
    2. Hanya menggunakan metode non-preemptive (tidak Menangani Kasus Preemptive).
    3. Output hanya berupa tabel numerik, tanpa visualisasi garis waktu (timeline) eksekusi proses, yang penting untuk pemahaman visual alur penjadwalan.
```
---

## Kesimpulan
1. FCFS dan SJF memiliki alur perhitungan yang sama, perbedaannya terletak pada cara pemilihan proses, yaitu berdasarkan urutan kedatangan (FCFS) dan burst time terpendek (SJF).
2. SJF lebih efisien dibanding FCFS dalam menurunkan waiting time dan turnaround time, tetapi memiliki risiko starvation pada proses dengan burst time besar.
3. Simulasi pemrograman membantu memahami konsep CPU scheduling, meskipun masih memiliki keterbatasan karena belum sepenuhnya mencerminkan kondisi sistem operasi nyata.
---

## Quiz
1. Mengapa simulasi diperlukan untuk menguji algoritma scheduling?

   **Jawaban: Simulasi diperlukan untuk menguji algoritma scheduling karena tidak membahayakan sistem produksi, bisa test banyak skenario, kontrol varibel, minim noise, hasil dapat diproduksi dan diverifikasi.**  
2. Apa perbedaan hasil simulasi dengan perhitungan manual jika dataset besar?

   **Jawaban: Perbedaan hasil antara simulasi dan perhitungan manual pada dataset besar yaitu jika perhitungan manual sering terjadi rounding error, human error, kapasitas terbatas. Sedangkan simulasi pergitungan memungkinkan kita untuk mempelajari algoritma penjadwalan dengan jejak beban kerja nyata yang berisi ribuan proses, yang tidak mungkin dianalisis secara manual, update priority tiap unit secara akurat,dll.**  
3. Algoritma mana yang lebih mudah diimplementasikan? Jelaskan.

   **Jawaban: Algoritma yang lebih mudah diimplementasikan yaitu algoritma FCFS (First-Come, First_Served. Karena tidak memiliki prioritas atau perhitungan yang kompleks, hanya perlu melacak urutan kedatangan, tidak perlu waktu sisa, riwayat penggunaan CPU, dll**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  - Bagian yang paling menantang minggu ini yaitu dalam mencari kelebihan dan keterbatasan simulasi.

- Bagaimana cara Anda mengatasinya?  
  - Cara saya mengatasinya yaitu dengan berusaha lebih keras menyelesaikan tantangan tersebut juga dengan dibantu oleh sumber sumber yang ada.
---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
