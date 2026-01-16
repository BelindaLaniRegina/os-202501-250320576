
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
```
processes = ["P1", "P2", "P3"]
wait_for = {"P1": "P2", "P2": "P3", "P3": "P1"}


def cek_deadlock(processes, wait_for):
    for p in processes:
        visited = {p}
        current = wait_for.get(p)
        
        while current and current not in visited:
            visited.add(current)
            current = wait_for.get(current)
        
        if current in visited:
            return True
    return False

def tampilkan_hasil(processes, wait_for, deadlock):
    print("DETEKSI DEADLOCK")
    print("-" * 40)
    for p in processes:
        print(f"{p} menunggu {wait_for[p]}")
    print("-" * 40)
    print(f"Status: {'DEADLOCK' if deadlock else 'AMAN'}")

deadlock = cek_deadlock(processes, wait_for)
tampilkan_hasil(processes, wait_for, deadlock)
```

---

## Hasil Eksekusi
![alt text](<screenshots/week11.png>)

---

## Analisis
1. Sajikan hasil deteksi dalam tabel (proses deadlock / tidak).  

| Proses                | Menunggu Proses Lain | Status            |
| :-------------------- | :------------------- | :---------------- |
| P1                    | P2                   | Terlibat deadlock |
| P2                    | P3                   | Terlibat deadlock |
| P3                    | P1                   | Terlibat deadlock |

**Kesimpulan Sistem: DEADLOCK**      

2. Jelaskan mengapa deadlock terjadi atau tidak terjadi.

Deadlock terjadi karena setiap proses saling menunggu proses lain kayak bentuk lingkaran.
- P1 menunggu P2
- P2 menunggu P3
- P3 menunggu P1

Hal tersebut mengakibatkan beberapa hal seperti tidak ada proses yang bisa berjalan, semua proses berhenti selamanya, dan sistem mendeteksi kondisi deadlock.

3. Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

Deadlock terjadi jika keempat kondisi berikut terpenuhi, dan pada kasus ini semuanya terpenuhi:
- Mutual Exclusion, sumber daya hanya bisa digunakan satu proses dalam satu waktu.
- Hold and Wait, setiap proses memegang satu sumber daya sambil menunggu sumber daya lain.
- No Preemption, sumber daya tidak bisa direbut paksa, harus dilepas secara sukarela.
- Circular Wait, terjadi rantai melingkar karena saling menunggu.
---

## Kesimpulan
1. Deadlock bisa diketahui dengan melihat apakah proses saling menunggu satu sama lain.
2. Deadlock terjadi jika proses membentuk lingkaran tunggu, sehingga semua proses berhenti dan tidak bisa berjalan.
3. Jika syarat-syarat deadlock terpenuhi, maka sistem pasti mengalami deadlock

---

## Quiz
1. Apa perbedaan antara deadlock prevention, avoidance, dan detection?  
   
   Jawaban: Perbedaan antara deadlock prevention, avoidance, dan detection yaitu  Kemungkinan terjadinya kebuntuan dikesampingkan sebelum melakukan permintaan, dengan menghilangkan salah satu kondisi yang diperlukan untuk terjadinya kebuntuan. Contohnya seperti dengan hanya mengizinkan lalu lintas dari satu arah, akan menghilangkan kemungkinan terjadinya kemacetan di jalan. Kalau deadlock avoidance adalah sistem operasi menjalankan algoritma pada permintaan untuk memeriksa kondisi yang aman. Permintaan apa pun yang dapat mengakibatkan kebuntuan tidak akan dikabulkan. Contohnya seperti memeriksa setiap mobil dan tidak mengizinkan mobil apa pun yang dapat menghalangi jalan. Jika sudah ada lalu lintas di jalan, maka mobil yang datang dari arah berlawanan dapat menyebabkan kemacetan. Dan deadlock detection adalah sistem operasi yang  mendeteksi kebuntuan dengan secara teratur memeriksa status sistem, dan memulihkan diri ke keadaan aman menggunakan teknik pemulihan. Contohnya seperti membuka blokir jalan dengan memundurkan mobil dari satu sisi. Pencegahan dan penghindaran kebuntuan dilakukan sebelum kebuntuan terjadi.
   
2. Mengapa deteksi deadlock tetap diperlukan dalam sistem operasi?  

   Jawaban: Deteksi deadlock tetap diperlukan dalam sistem operasi karena pada sistem yang kompleks pencegahan atau penghindaran deadlock sering tidak efisien atau membatasi kinerja sistem. Tanpa deteksi deadlock, deadlock dapat membuat CPU, memori, atau I/O terkunci permanen oleh proses yang saling menunggu, sehingga sistem menjadi tidak responsif. Maka dari itu, eteksi deadlock adalah komponen penting dalam manajemen sumber daya OS karena memberikan solusi yang praktis dan fleksibel. Deteksi memungkinkan sistem beroperasi dengan efisiensi dan utilitas yang tinggi (tanpa batasan pencegahan), sambil tetap memiliki kemampuan untuk secara otomatis mengidentifikasi dan memulihkan diri dari kebuntuan yang mengancam ketersediaan sistem, terutama pada lapisan kernel dan dalam lingkungan virtual yang kompleks.
     
3. Apa kelebihan dan kekurangan pendekatan deteksi deadlock?

   Jawaban:
   Kelebihan pendekatan deteksi deadlock yaitu;
   - Fleksibilitas tinggi dalam alokasi sumber daya
   - Overhead yang Dapat Dikontrol
   - Memungkinkan Pemulihan Otomatis (Automatic Recovery)
     
   Kekurangan pendekatan deteksi deadlock yaitu;
   - Biaya dan Kompleksitas Pemulihan yang Tinggi
   - Keterlambatan Identifikasi (Detection Lag)
   - Kesulitan dalam Sistem Terdistribusi  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  
  Yang paling menantang minggu ini adalah tentang bagaimana cara untuk membuat program deadlock.
  
- Bagaimana cara Anda mengatasinya?

  Cara saya mengatasinya yaitu dengan mencari tahu lebih dalam dan juga dengan meminta bantuan teman bahkan tekonologi saat ini.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
