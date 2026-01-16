
# Laporan Praktikum Minggu [10]
Topik: Manajemen Memori – Page Replacement (FIFO & LRU)
---

## Identitas
- **Nama**  : Belinda Lani Regina 
- **NIM**   : 250320576
- **Kelas** : 1DSRA

---

## Tujuan
1. Dapat mengimplementasikan algoritma page replacement FIFO dalam program.
2. Dapat mengimplementasikan algoritma page replacement LRU dalam program.
3. Dapat menjalankan simulasi page replacement dengan dataset tertentu.
4. Dapat membandingkan performa FIFO dan LRU berdasarkan jumlah *page fault*.
5. Dapat menyajikan hasil simulasi dalam laporan yang sistematis.

---

## Dasar Teori
1. Page replacement adalah komponen kritis virtual memory management.
2. FIFO mewakili pendekatan sederhana dengan keterbatasan fundamental.
3. LRU mewakili pendekatan berbasis prinsip lokalitas dengan kinerja lebih baik secara teoretis.
4. Gap antara teori dan praktik diatasi dengan algoritma aproksimasi.
5. Pemilihan algoritma merupakan trade-off antara akurasi prediksi dan overhead implementasi.
---

## Langkah Praktikum
1. **Menyiapkan Dataset**

   Gunakan *reference string* berikut sebagai contoh:
   ```
   7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2
   ```
   Jumlah frame memori: **3 frame**.

2. **Implementasi FIFO**

   - Simulasikan penggantian halaman menggunakan algoritma FIFO.
   - Catat setiap *page hit* dan *page fault*.
   - Hitung total *page fault*.

3. **Implementasi LRU**

   - Simulasikan penggantian halaman menggunakan algoritma LRU.
   - Catat setiap *page hit* dan *page fault*.
   - Hitung total *page fault*.

4. **Eksekusi & Validasi**

   - Jalankan program untuk FIFO dan LRU.
   - Pastikan hasil simulasi logis dan konsisten.
   - Simpan screenshot hasil eksekusi.

5. **Analisis Perbandingan**

   Buat tabel perbandingan seperti berikut:

   | Algoritma | Jumlah Page Fault | Keterangan |
   |:--|:--:|:--|
   | FIFO | ... | ... |
   | LRU | ... | ... |


   - Jelaskan mengapa jumlah *page fault* bisa berbeda.
   - Analisis algoritma mana yang lebih efisien dan alasannya.

6. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 10 - Page Replacement FIFO & LRU"
   git push origin main
   ```

---

## Kode / Perintah
```
reference_string = [7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2]
frames = 3


def print_table(title, steps):
    print(f"\n{title}")
    print("+--------+----------+----------+----------+----------+")
    print("| Page   | Frame 1  | Frame 2  | Frame 3  | Status   |")
    print("+--------+----------+----------+----------+----------+")
    for p, m, s in steps:
        print(f"| {p:<6} | {m[0]:<8} | {m[1]:<8} | {m[2]:<8} | {s:<8} |")
    print("+--------+----------+----------+----------+----------+")


def page_replacement(ref, frames, algo):
    memory = ['-'] * frames
    steps, fault = [], 0
    info = {}

    for t, page in enumerate(ref):
        if page in memory:
            status = "HIT"
        else:
            fault += 1
            status = "FAULT"

            if '-' in memory:
                idx = memory.index('-')
            else:
                if algo == "FIFO":
                    idx = fault % frames - 1
                else:  # LRU
                    lru = min(info, key=info.get)
                    idx = memory.index(lru)
                    del info[lru]

            memory[idx] = page

        info[page] = t
        steps.append((page, memory.copy(), status))

    return fault, steps


# ================= EKSEKUSI =================
fifo_fault, fifo_steps = page_replacement(reference_string, frames, "FIFO")
lru_fault, lru_steps = page_replacement(reference_string, frames, "LRU")

print_table("Proses FIFO", fifo_steps)
print_table("Proses LRU", lru_steps)

print("\nRINGKASAN HASIL AKHIR")
print("+------------+--------------+--------------+")
print("| Algoritma  | Jumlah Frame | Page Fault   |")
print("+------------+--------------+--------------+")
print(f"| FIFO       | {frames:^12} | {fifo_fault:^12} |")
print(f"| LRU        | {frames:^12} | {lru_fault:^12} |")
print("+------------+--------------+--------------+")
```

---

## Hasil Eksekusi
![alt text](<screenshots/week10.png>)

1. Hasil FIFO
   
![alt text](<screenshots/week10_fifo.png>)

2. Hasil LRU

![alt text](<screenshots/week10_LRU.png>)

3. Perbandingan

![alt text](<screenshots/week10_ringkasan.png>)
---

## Analisis
1. Tabel perbandingan
  
| Algoritma | Jumlah Page Fault | Keterangan                                                                        |
| :-------- | :---------------: | :-------------------------------------------------------------------------------- |
| FIFO      |       **10**      | Mengganti halaman yang pertama kali masuk dengan tidak memperhatikan frekuensi pemakaian |
| LRU       |       **9**       | Mengganti halaman yang paling lama tidak digunakan dilihat dari riwayat akses      |

2. Jelaskan mengapa jumlah *page fault* bisa berbeda.
   - FIFO hanya melihat urutan masuk halaman. Halaman yang masuk paling awal akan diganti, meskipun masih sering dipakai.
   - LRU melihat halaman mana yang paling lama tidak digunakan. Halaman yang masih sering dipakai akan dipertahankan lebih lama.
     
3. Analisis algoritma mana yang lebih efisien dan alasannya.
   - Jumlah page fault lebih sedikit (9 < 10).
   - LRU menyesuaikan keputusan dengan perilaku akses halaman.
   - FIFO berpotensi mengalami Belady’s Anomaly (penambahan frame justru menambah page fault).

---

## Kesimpulan
1. FIFO vs LRU Berbeda Prinsip Dasar
FIFO ganti halaman paling lama masuk (buta pola akses), LRU ganti halaman paling lama tak dipakai (manfaatkan lokalitas).
2. LRU Lebih Baik Secara Teori, FIFO Lebih Sederhana. LRU umumnya minim page fault karena ikuti prinsip lokalitas, tapi implementasi tepatnya mahal; FIFO sederhana dan cepat tapi kinerja sering buruk.
3. Sistem Nyata Pakai Aproksimasi, karena overhead LRU asli tinggi, OS praktis pakai algoritma pendekatan seperti clock/second-chance yang balance kinerja mirip LRU dan efisiensi seperti FIFO.

---

## Quiz
1. Apa perbedaan utama FIFO dan LRU?
   
   Jawaban: Perbedaan utama FIFO dan LRU yaitu;
   - Jika FIFO ganti halaman tertua berdasarkan waktu masuk (queue order). Sedangkan LRU Ganti halaman yang paling lama tidak diakses.
   - Jika FIFO tidak mempertimbangkan frekuensi akses, hanya urutan masuk dan juga Dianggap mudah diimplementasi tetapi kinerja sering buruk. Sedangakan LRU  algoritma yang teoritis baik karena mengikuti perilaku program (lokalisasi spasial dan temporal). Namun, implementasi tepat (true LRU) mahal secara hardware/software, sehingga sering dipakai pendekatan seperti LRU dengan bit referensi (clock algorithm).
   - Dan yang terakhir FIFO dapat menghasilkan/terjadi Balady's Anomaly, sedangkan LRU tidak menghasilkan/tidak terjadi.
   
3. Mengapa FIFO dapat menghasilkan Belady’s Anomaly?
   
   Jawaban: Balady's Anomaly adalah Fenomena di mana penambahan jumlah frame memori justru meningkatkan jumlah page fault. FIFO dapat menghasilkan Balady's Anomaly karena algoritma ini tidak memperhatikan pola akses atau frekuensi penggunaan halaman, hanya mengandalkan urutan waktu masuk. Selain itu juga dapat dikarenakan perubahan jumlah frame mengubah dinamika antrian secara tidak terduga. Anomali ini menunjukkan kelemahan fundamental FIFO sebagai algoritma page replacement.
     
4. Mengapa LRU umumnya menghasilkan performa lebih baik dibanding FIFO?
   
   Jawaban: LRU umumnya menghasilkan performa lebih baik dibanding FIFO karena dapat mempertahankan working set di memori lebih efektif, mengakomodasi prinsip lokalitas yang melekat pada program komputer, lebih resisten terhadap thrashing pada pola akses berulang, dan tidak mengalami Belady's Anomaly.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
