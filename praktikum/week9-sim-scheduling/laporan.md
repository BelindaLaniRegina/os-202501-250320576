
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
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

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
  ```
```

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
lsmod | head
dmesg | head
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
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
