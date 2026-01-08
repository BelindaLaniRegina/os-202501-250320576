
# Laporan Praktikum Minggu [11]
Topik: Simulasi dan Deteksi Deadlock
---

## Identitas
- **Nama**  : Belinda Lani Regina
- **NIM**   : 250320576
- **Kelas** : 1DSRA

---

## Tujuan
1. Dapat membuat program sederhana untuk mendeteksi deadlock.  
2. Dapat menjalankan simulasi deteksi deadlock dengan dataset uji.  
3. Dapat menyajikan hasil analisis deadlock dalam bentuk tabel.  
4. Dapat memberikan interpretasi hasil uji secara logis dan sistematis.  
5. Dapat menyusun laporan praktikum sesuai format yang ditentukan.
---

## Dasar Teori
1. Deadlock adalah kondisi stagnasi akibat sekelompok proses saling menunggu sumber daya. Terjadi bila empat kondisi terpenuhi: Mutual Exclusion, Hold and Wait, No Preemption, dan Circular Wait (Silberschatz et al., 2018).
2. Dilakukan dengan memodelkan keadaan sistem menggunakan matriks (alokasi, permintaan, ketersediaan) untuk menganalisis kemungkinan deadlock tanpa mengganggu sistem nyata (Tanenbaum, 2016).
3. Menggunakan wait-for graph (untuk sumber daya tipe tunggal) atau algoritma berbasis matriks alokasi dan permintaan (mirip Banker's Algorithm) untuk sumber daya berjumlah banyak (multiple instances).

---

## Langkah Praktikum
1. **Menyiapkan Dataset**

   Gunakan dataset sederhana yang berisi:
   - Daftar proses  
   - Resource Allocation  
   - Resource Request / Need

   Contoh tabel:

   | Proses | Allocation | Request |
   |:--:|:--:|:--:|
   | P1 | R1 | R2 |
   | P2 | R2 | R3 |
   | P3 | R3 | R1 |

2. **Implementasi Algoritma Deteksi Deadlock**

   Program minimal harus:
   - Membaca data proses dan resource.  
   - Menentukan apakah sistem berada dalam kondisi deadlock.  
   - Menampilkan proses mana saja yang terlibat deadlock.

3. **Eksekusi & Validasi**

   - Jalankan program dengan dataset uji.  
   - Validasi hasil deteksi dengan analisis manual/logis.  
   - Simpan hasil eksekusi dalam bentuk screenshot.

4. **Analisis Hasil**

   - Sajikan hasil deteksi dalam tabel (proses deadlock / tidak).  
   - Jelaskan mengapa deadlock terjadi atau tidak terjadi.  
   - Kaitkan hasil dengan teori deadlock (empat kondisi).

5. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 11 - Deadlock Detection"
   git push origin main
   ```
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
1. Apa perbedaan antara deadlock prevention, avoidance, dan detection?  
   
   **Jawaban: Perbedaan antara deadlock prevention, avoidance, dan detection yaitu  Kemungkinan terjadinya kebuntuan dikesampingkan sebelum melakukan permintaan, dengan menghilangkan salah satu kondisi yang diperlukan untuk terjadinya kebuntuan. Contohnya seperti dengan hanya mengizinkan lalu lintas dari satu arah, akan menghilangkan kemungkinan terjadinya kemacetan di jalan. Kalau deadlock avoidance adalah sistem operasi menjalankan algoritma pada permintaan untuk memeriksa kondisi yang aman. Permintaan apa pun yang dapat mengakibatkan kebuntuan tidak akan dikabulkan. Contohnya seperti memeriksa setiap mobil dan tidak mengizinkan mobil apa pun yang dapat menghalangi jalan. Jika sudah ada lalu lintas di jalan, maka mobil yang datang dari arah berlawanan dapat menyebabkan kemacetan. Dan deadlock detection adalah sistem operasi yang  mendeteksi kebuntuan dengan secara teratur memeriksa status sistem, dan memulihkan diri ke keadaan aman menggunakan teknik pemulihan. Contohnya seperti membuka blokir jalan dengan memundurkan mobil dari satu sisi. Pencegahan dan penghindaran kebuntuan dilakukan sebelum kebuntuan terjadi.**
   
2. Mengapa deteksi deadlock tetap diperlukan dalam sistem operasi?  

   **Jawaban: Deteksi deadlock tetap diperlukan dalam sistem operasi karena**
     
3. Apa kelebihan dan kekurangan pendekatan deteksi deadlock?

   **Jawaban: Kelebihan pendekatan deteksi deadlock yaitu **  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
