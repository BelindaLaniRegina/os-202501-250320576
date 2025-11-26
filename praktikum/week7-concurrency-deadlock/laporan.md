
# Laporan Praktikum Minggu [7]
Topik: Concurrency Deadlock
---

## Identitas
- **Nama**  : Belinda Lani Regina  
- **NIM**   : 250320576
- **Kelas** : 1DSRA

## Kelompok
1. R
2. Rizzca Anggreany (250320578)
3. Faizatun Khasanah (250320584)
4. Belinda Lani Regina (250320576)
---

## Tujuan
> 1. Dapat mengidentifikasi empat kondisi penyebab deadlock (mutual exclusion, hold and wait, no preemption, circular wait).
> 2. Dapat menjelaskan mekanisme sinkronisasi menggunakan semaphore atau monitor.
> 3. Dapat menganalisis dan memberikan solusi untuk kasus deadlock.
> 4. Dapat berkolaborasi dalam tim untuk menyusun laporan analisis.
> 5. Dapat menyajikan hasil studi kasus secara sistematis.
---

## Pendahuluan 
A. LATAR BELAKANG

Deadlock adalah situasi dalam sistem operasi di mana dua atau lebih proses saling menunggu sumber daya yang dikontrol oleh proses lain, sehingga tidak ada proses yang dapat melanjutkan eksekusi. Ini menghasilkan kebuntuan permanen, di mana sistem terhenti. Konsep ini pertama kali diformalkan oleh Edsger Dijkstra pada 1968. Deadlock umum terjadi dalam sistem multi-proses yang berbagi sumber daya terbatas, seperti CPU, memori, atau perangkat I/O.
 Kondisi Terjadinya Deadlock
Menurut Coffman et al. (1971), deadlock hanya bisa terjadi jika empat kondisi berikut terpenuhi secara bersamaan. Jika salah satu kondisi dihilangkan, deadlock dapat dicegah.
1. Mutual Exclusion (Eksklusivitas Mutual) : Setiap sumber daya hanya dapat digunakan oleh satu proses pada satu waktu. Misalnya, printer tidak bisa dibagi oleh dua proses sekaligus.
   
2. Hold and Wait (Pegang dan Tunggu) : Proses yang sudah memegang satu sumber daya dapat meminta sumber daya tambahan, sambil menunggu yang lain. Ini memungkinkan proses untuk "menahan" sumber daya tanpa melepaskannya.
3. No Preemption (Tidak Ada Pengambilalihan) : Sumber daya tidak dapat diambil paksa dari proses yang memegangnya. Proses harus melepaskan sumber daya secara sukarela setelah selesai.
4. Circular Wait (Tunggu Melingkar) : Ada siklus tunggu di antara proses, di mana setiap proses menunggu sumber daya yang dipegang oleh proses berikutnya dalam siklus. Ini sering divisualisasikan dengan resource allocation graph.
Contoh Klasik Deadlock
Bayangkan dua proses, P1 dan P2, dan dua sumber daya, R1 dan R2:
- P1 memegang R1 dan meminta R2.
- P2 memegang R2 dan meminta R1.
- Kedua proses saling menunggu, sehingga tidak ada yang bisa maju. Ini adalah contoh sederhana dari dining philosophers problem (Dijkstra, 1968), di mana filosof (proses) saling menunggu garpu (sumber daya).
Dalam konteks OS, deadlock bisa terjadi di database (misalnya, dua transaksi saling lock tabel) atau sistem file (proses menunggu akses file yang dikunci oleh proses lain). Tanenbaum dan Bos (2015) memberikan contoh deadlock dalam thread yang berbagi mutex.
Dampak Deadlock
Deadlock menyebabkan sistem tidak responsif, menghambat produktivitas, dan bisa berakibat fatal dalam aplikasi kritis seperti server atau sistem embedded. Sistem operasi seperti Linux atau Windows memiliki mekanisme untuk mendeteksi deadlock, tetapi tanpa intervensi, proses yang terlibat akan hang selamanya. OSTEP (2018, Bab 32) menekankan bahwa deadlock jarang terjadi dalam praktik, tetapi ketika terjadi, dampaknya signifikan.
Metode Penanganan Deadlock
Ada empat strategi utama untuk menangani deadlock, sebagaimana dijelaskan dalam Silberschatz et al. (2018):
1. Prevention (Pencegahan) : Mencegah deadlock dengan menghilangkan salah satu kondisi. Misalnya:
   - Izinkan preemption: Sistem dapat mengambil sumber daya dari proses (sulit untuk sumber daya seperti printer).
   - Hindari hold and wait: Proses harus meminta semua sumber daya sekaligus di awal.
   - Tetapkan urutan sumber daya: Proses hanya boleh meminta sumber daya dalam urutan tertentu untuk menghindari circular wait.
   - Kekurangan: Mengurangi efisiensi sistem, karena proses mungkin menunggu lebih lama.
2. Avoidance (Penghindaran) : Sistem memprediksi apakah alokasi sumber daya akan menyebabkan deadlock dan menghindarinya. Algoritma utama adalah Banker's Algorithm (Dijkstra, 1965), yang menggunakan state information untuk memastikan sistem selalu dalam safe state (di mana semua proses bisa diselesaikan tanpa deadlock). Tanenbaum dan Bos (2015) menjelaskan implementasinya di OS modern, meskipun overheadnya tinggi untuk sistem besar.
3. Detection and Recovery (Deteksi dan Pemulihan) : Izinkan deadlock terjadi, lalu deteksi dan pulihkan. Deteksi menggunakan wait-for graph atau resource allocation graph. Pemulihan melibatkan:
   - Menghentikan proses (terminate) dan mengalokasikan ulang sumber daya.
   - Rollback: Mengembalikan proses ke state sebelumnya.
   - Linux Manual Pages menjelaskan tools seperti strace untuk debugging deadlock dalam thread.
4. ignorance (Pengabaian) :

---

## Langkah Praktikum
1. *Persiapan Tim*
   - Bentuk kelompok beranggotakan 3–4 orang.  
   - Tentukan ketua dan pembagian tugas (analisis, implementasi, dokumentasi).

2. *Eksperimen 1 – Simulasi Dining Philosophers (Deadlock Version)*
   - Implementasikan versi sederhana dari masalah Dining Philosophers tanpa mekanisme pencegahan deadlock.  
   - Contoh pseudocode:
     text
     while true:
       think()
       pick_left_fork()
       pick_right_fork()
       eat()
       put_left_fork()
       put_right_fork()
     
   - Jalankan simulasi atau analisis alur (boleh menggunakan pseudocode atau diagram alur).  
   - Identifikasi kapan dan mengapa deadlock terjadi.

3. *Eksperimen 2 – Versi Fixed (Menggunakan Semaphore / Monitor)*
   - Modifikasi pseudocode agar deadlock tidak terjadi, misalnya:
     - Menggunakan semaphore (mutex) untuk mengontrol akses.
     - Membatasi jumlah filosof yang dapat makan bersamaan (max 4).  
     - Mengatur urutan pengambilan garpu (misal, filosof terakhir mengambil secara terbalik).  
   - Analisis hasil modifikasi dan buktikan bahwa deadlock telah dihindari.

4. *Eksperimen 3 – Analisis Deadlock*
   - Jelaskan empat kondisi deadlock dari versi pertama dan bagaimana kondisi tersebut dipecahkan pada versi fixed.  
   - Sajikan hasil analisis dalam tabel seperti contoh berikut:

     | Kondisi Deadlock | Terjadi di Versi Deadlock | Solusi di Versi Fixed |
     |------------------|---------------------------|------------------------|
     | Mutual Exclusion | Ya (satu garpu hanya satu proses) | Gunakan semaphore untuk kontrol akses |
     | Hold and Wait | Ya | Hindari proses menahan lebih dari satu sumber daya |
     | No Preemption | Ya | Tidak ada mekanisme pelepasan paksa |
     | Circular Wait | Ya | Ubah urutan pengambilan sumber daya |

5. *Eksperimen 4 – Dokumentasi*
   - Simpan semua diagram, screenshot simulasi, dan hasil diskusi di:
     
     praktikum/week7-concurrency-deadlock/screenshots/
     
   - Tuliskan laporan kelompok di laporan.md (format IMRaD singkat: Pendahuluan, Metode, Hasil, Analisis, Diskusi).

6. *Commit & Push*
   bash
   git add .
   git commit -m "Minggu 7 - Sinkronisasi Proses & Deadlock"
   git push origin main
   
---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
 while true:
       think()
       pick_left_fork()
       pick_right_fork()
       eat()
       put_left_fork()
       put_right_fork()
```

---

## Hasil Eksekusi
- Ekesperimen 1
![alt text](<screenshots/week7_eksperimen1.png>)
- Eksperimen 2
  1. Semaphore (mutex)
![alt text](<screenshots/wee7_eksperimen2_semaphore(mutex).png>)
  2. Maksimal 4 Filsuf
![alt text](<screenshots/week7_eksperimen2_max4filsuf.png>)
---

## Analisis
- Eksperimen 1
```
import threading
import time
import random

N = 5
forks = [threading.Lock() for _ in range(N)]

def philosopher(i):
    left = forks[i]
    right = forks[(i + 1) % N]

    while True:
        # thinking
        print(f"Philosopher {i} is thinking.")
        time.sleep(random.uniform(0.5, 1.5))

        # ambil garpu kiri
        left.acquire()
        print(f"Philosopher {i} ambil garpu KIRI.")

        # ambil garpu kanan
        right.acquire()
        print(f"Philosopher {i} ambil garpu KANAN.")

        # makan
        print(f"Philosopher {i} is makan.")
        time.sleep(random.uniform(0.5, 1.0))

        # ambil garpu
        left.release()
        right.release()
        print(f"Philosopher {i} ambil garpu.\n")

threads = []
for i in range(N):
    t = threading.Thread(target=philosopher, args=(i,))
    t.start()
    threads.append(t)

time.sleep(3)
print("Selesai")
```
- Ekeperimen 2
1. Semaphore (mutex)
```
import threading
import time
import random

N = 5
forks = [threading.Semaphore(1) for _ in range(N)]

def philosopher(i):
    left = forks[i]
    right = forks[(i + 1) % N]

    while True:
        # Thinking
        print(f"Philosopher {i} is thinking.")
        time.sleep(random.uniform(0.5, 1.5))

        # ambil garpu kiri
        left.acquire()
        print(f"Philosopher {i} ambil garpu KIRI.")

        # ambil garpu kanan
        right.acquire()
        print(f"Philosopher {i} ambil garpu KANAN.")

        # makan
        print(f"Philosopher {i} is makan.")
        time.sleep(random.uniform(0.5, 1.0))

        # Put down forks
        left.release()
        right.release()
        print(f"Philosopher {i} put down forks.\n")

threads = []
for i in range(N):
    t = threading.Thread(target=philosopher, args=(i,))
    t.start()
    threads.append(t)
```
2. Maksimal 4 Filsuf
```
import threading
import time
import random

N = 5

# 5 garpu, masing-masing semaphore biner
forks = [threading.Semaphore(1) for _ in range(N)]

# Hanya maksimal 4 filosof boleh mencoba makan sekaligus
room = threading.Semaphore(4)

def philosopher(i):
    left = forks[i]
    right = forks[(i + 1) % N]

    while True:
        # Thinking
        print(f"Philosopher {i} is thinking.")
        time.sleep(random.uniform(0.5, 1.5))

        # Limit concurrency: hanya 4 boleh masuk
        room.acquire()

        # Ambil kedua garpu
        left.acquire()
        print(f"Philosopher {i} ambil garpu KIRI.")

        right.acquire()
        print(f"Philosopher {i} ambil garpu KANAN.")

        # makan
        print(f"Philosopher {i} is makan.")
        time.sleep(random.uniform(0.5, 1.0))

        # Letakkan garpu
        left.release()
        right.release()
        print(f"Philosopher {i} put down forks.")

        # Keluar dari ruang makan
        room.release()
        print(f"Philosopher {i} leaves eating room.\n")

threads = []
for i in range(N):
    t = threading.Thread(target=philosopher, args=(i,))
    t.start()
    threads.append(t)
```


---

## Kesimpulan
1. Mekanisme sinkronisasi seperti semaphore dan mutex sangat penting untuk menghindari race condition ketika beberapa proses/threads mengakses sumber daya bersama secara bersamaan.
2. Masalah Dining Philosophers menunjukkan bahwa strategi penguncian yang salah dapat menyebabkan deadlock, terutama jika semua proses menunggu sumber daya satu sama lain dalam pola melingkar.
3. Modifikasi seperti Odd–Even Fork Picking Rule terbukti mampu menghilangkan kondisi circular wait, sehingga deadlock dapat dihindari tanpa mengurangi paralelisme proses secara signifikan.
---

## Quiz
1. Sebutkan empat kondisi utama penyebab deeadlock! 

   Jawaban: Kondisi Utama terjadinya deadlock yaitu:
   - Pengecualian Bersama, Dalam kondisi ini, kita tidak dapat berbagi sumber daya di antara berbagai proses secara bersamaan. Contohnya yaitu, jika dua orang ingin mencetak kertas secara bersamaan, proses ini tidak dapat dilakukan. Salah satu dari mereka harus menunggu hingga sistem merilis cetakan (sumber daya). Dengan demikian, kita hanya dapat menetapkan sumber daya ke satu proses pada satu waktu.
   - Hold and wait atau penahanan sumber daya, dalam kondisi ini suatu proses secara bersamaan menahan setidaknya satu sumber daya dan menunggu sumber daya lain pada suatu waktu. Proses tersebut tidak berada dalam status berjalan melainkan proses tersebut berada dalam status menunggu .
   - Tidak adanya preemption, jika suatu proses memegang sumber daya maka sumber daya tersebut tidak dapat diambil paksa dari proses tersebut hingga proses tersebut melepaskannya. Pernyataan ini juga berlaku ketika proses berada dalam status menunggu.
   - Menunggu melingkar (Circular Wait), jika kita asumsikan proses P1 sedang menunggu sumber daya R2. Sumber daya R2 tersebut sudah dipegang oleh proses P2. Proses P2 sedang menunggu sumber daya yang dipegang oleh proses berikutnya. Hal ini akan berlanjut hingga proses terakhir menunggu sumber daya yang dipegang oleh proses pertama. Kondisi tunggu melingkar menciptakan rantai melingkar dan menempatkan semua proses dalam keadaan menunggu.

2. Mengapa sinkronisasi diperlukan dalam sistem operasi?
   
   Jawaban: Sinkronisasi diperlukan dalam sistem operasi karena sinkronisasi merupakan aspek penting dalam Sistem Operasi yang memastikan eksekusi beberapa proses bersamaan yang harmonis dan terprediksi. Sinkronisasi berfokus pada pencegahan konflik dan kondisi balapan ketika proses mengakses sumber daya bersama atau bagian kode yang penting. Panggilan Sistem dalam Sistem Operasi memainkan peran penting dalam mengelola mekanisme sinkronisasi, memastikan koordinasi proses yang lancar. Karena itu, jika sistem operasi tidak memiliki sinkronisasi maka akan terjadi ketidakonsistenan data, kerusakan data, dan kondisi balapan (race condition) karena proses-proses yang berjalan bersamaan tidak dapat berkoordinasi dalam mengakses sumber daya Bersama.
    
3. Jelaskan perbedaan antara semaphore dan monitor!  

   Jawaban: Perbedaan antara semaphore dan monitor yaitu:
   - Jika semaphore adalah objek sinkronisasi yang digunakan untuk mengontrol akses ke sumber daya bersama dalam lingkungan multi-utas atau multi-proses dan juga mekanisme pensinyalan yang memungkinkan utas atau proses berkomunikasi satu sama lain dan menghindari kondisi balapan. Sedangkan monitor adalah mekanisme sinkronisasi yang digunakan untuk mengontrol akses ke sumber daya bersama dalam lingkungan multi-utas, konstruksi tingkat tinggi daripada semafor dan juga menyediakan cara yang lebih terstruktur untuk menyinkronkan utas.
   - Jika Semaphore yang mengontrol locking dan unlolocking adalah Programmer. Sedangkan jika monitor dalah sistem/runtime yang mengatur locking dan unlocking.
   - Jika Semaphore lebih sulit digunakan karena mudah salah (misalnya lupa signal, double wait). Sedangkan jika monitor ebih mudah dan aman karena sistem mengatur locking.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
