
# Laporan Praktikum Minggu [X]
Topik: Docker – Resource Limit (CPU & Memori)

---

## Identitas
- **Nama**  : Belinda Lani Regina
- **NIM**   : 250320576
- **Kelas** : 1DSRA

---

## Tujuan
1. Dapat menulis Dockerfile sederhana untuk sebuah aplikasi/skrip.
2. Dapat membangun image dan menjalankan container.
3. Dapat menjalankan container dengan pembatasan **CPU** dan **memori**.
4. Dapat mengamati dan menjelaskan perbedaan eksekusi container dengan dan tanpa limit resource.
5. Dapat menyusun laporan praktikum secara runtut dan sistematis.

---

## Dasar Teori
1. Docker membatasi CPU dan memori container menggunakan fitur cgroups pada Linux, sehingga penggunaan resource tiap container bisa diatur sesuai kebutuhan (Linux Kernel Docs – cgroups & namespaces).
2. Docker menerapkan virtualisasi tingkat sistem operasi, di mana container berbagi kernel yang sama tetapi tetap terisolasi dalam penggunaan resource (OSTEP – Virtualization / Resource Management).
3. Pengaturan batas CPU dan memori di Docker menjaga stabilitas sistem, agar satu container tidak menghabiskan resource dan mengganggu container lain (Docker Documentation – Resource constraints CPU/Memory).
---

## Langkah Praktikum
1. **Persiapan Lingkungan**

   - Pastikan Docker terpasang dan berjalan.
   - Verifikasi:
     ```bash
     docker version
     docker ps
     ```

2. **Membuat Aplikasi/Skrip Uji**

   Buat program sederhana di folder `code/` (bahasa bebas) yang:
   - Melakukan komputasi berulang (untuk mengamati limit CPU), dan/atau
   - Mengalokasikan memori bertahap (untuk mengamati limit memori).

3. **Membuat Dockerfile**

   - Tulis `Dockerfile` untuk menjalankan program uji.
   - Build image:
     ```bash
     docker build -t week13-resource-limit .
     ```

4. **Menjalankan Container Tanpa Limit**

   - Jalankan container normal:
     ```bash
     docker run --rm week13-resource-limit
     ```
   - Catat output/hasil pengamatan.

5. **Menjalankan Container Dengan Limit Resource**

   Jalankan container dengan batasan resource (contoh):
   ```bash
   docker run --rm --cpus="0.5" --memory="256m" week13-resource-limit
   ```
   Catat perubahan perilaku program (mis. lebih lambat, error saat memori tidak cukup, dll.).

6. **Monitoring Sederhana**

   - Jalankan container (tanpa `--rm` jika perlu) dan amati penggunaan resource:
     ```bash
     docker stats
     ```
   - Ambil screenshot output eksekusi dan/atau `docker stats`.

7. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 13 - Docker Resource Limit"
   git push origin main
   ```
---

## Kode / Perintah
-week13.py
```
import time

BLOCK_MB = 10
SAFE_LIMIT_MB = 256
data = []

def read_cgroup_mb(path):
    try:
        with open(path) as f:
            v = f.read().strip()
            return None if v == "max" else int(v) / (1024 * 1024)
    except:
        return None if "max" in path else 0

mem_limit = read_cgroup_mb("/sys/fs/cgroup/memory.max")

print(
    f"Memory limit terdeteksi: {mem_limit:.0f} MB"
    if mem_limit else
    "Tidak ada memory limit Docker"
)

i = 0
while True:
    # Bebani CPU
    x = 0
    for j in range(8_000_000):
        x += j * j

    # Alokasi memori
    data.append("X" * (BLOCK_MB * 1024 * 1024))

    mem_used = read_cgroup_mb("/sys/fs/cgroup/memory.current")
    print(f"Iterasi {i} | Memori terpakai: {mem_used:.2f} MB")

    if mem_limit and mem_used >= SAFE_LIMIT_MB:
        print("Mendekati limit memori Docker → program berhenti normal")
        break

    i += 1
    time.sleep(0.5)

print("Program selesai")

```
-dockerfile
```
FROM python:3.10-slim

WORKDIR /app
COPY week13.py .

CMD ["python", "week13.py"]
```

---

## Hasil Eksekusi & Analisis
1. Membuat Dockerfile

![alt text](<screenshots/docker1.jpeg>)

2. Menjalankan Container Tanpa Limit

![alt text](<screenshots/docker2.png>)

**Analisis: Bisa diliat kalau penggunaan memori container terus meningkat di setiap iterasinya, dari sekitar 41 MB sampai lebih dari 150 MB. Kenaikan ini terjadi karena program secara bertahap menambahkan alokasi memori, dan Docker tidak berhenti atau membatasi proses tersebut. Hal itu menunjukkan kalau container dijalankan tanpa memory limit, sehingga container bebas menggunakan memori sebanyak yang dibutuhkan selama memori host masih tersedia. Akibatnya, tidak ada mekanisme perlindungan otomatis ketika penggunaan memori terus bertambah. Jadi, menjalankan container tanpa limit memori berisiko bagi sistem, karena container dapat menghabiskan RAM host dan menyebabkan sistem melambat atau crash.**

3. Menjalankan Container Dengan Limit Resource

![alt text](<screenshots/docker3.jpeg>)

**Analisis: Bisa diliat bahwa Docker berhasil mendeteksi memory limit sebesar 256 MB. Selama program berjalan, penggunaan memori meningkat secara bertahap di setiap iterasi, sesuai dengan proses alokasi memori yang dilakukan oleh aplikasi di dalam container. Bede dengan kondisi tanpa limit, pada saat penggunaan memori mendekati batas yang ditentukan, program berhenti secara normal dengan pesan “Mendekati limit memori Docker → program berhenti normal”. Itu menunjukkan bahwa pembatasan memori bekerja dengan baik, dan container tidak dibiarkan terus mengambil memori dari host.**

4. Monitoring Sederhana

![alt text](<screenshots/docker4.jpeg>)

---

## Kesimpulan
1. Menjalankan container Docker tanpa resource limit menyebabkan penggunaan memori meningkat terus tanpa pembatasan, sehingga berpotensi mengganggu stabilitas sistem host.
2. Penerapan memory limit pada Docker terbukti efektif membatasi penggunaan memori, karena container dapat berhenti secara terkontrol saat mendekati batas yang ditentukan.
3. Praktikum ini menunjukkan bahwa pengaturan resource limit (CPU dan memori) sangat penting untuk menjaga keamanan, stabilitas, dan isolasi antar container dalam lingkungan Docker.
---

## Quiz
1. Mengapa container perlu dibatasi CPU dan memori?
   
   Jawab: Container perlu dibatasi CPU dan memori yaitu karena beberapa alasan seperti;
   - Resource planning yang lebih baik juga terkontrol
   - Mencegah satu container menghabiskan resource
   - Menjaga kestabilan sistem host
   - Redictability dan stabilitas.
     
3. Apa perbedaan VM dan container dalam konteks isolasi resource?

   Jawaban: Perbedaan VM dan container dalam konteks isolasi resource yaitu;
   - Dalam tingkat isolasi, VM memberikan isolasi yang jauh lebih kuat karena setiap VM punya kernel OS sendiri yang terpisah. Jika satu VM crash atau ter-compromise, VM lain tidak terpengaruh sama sekali. Sedangkan container berbagi kernel yang sama dengan host dan container lain. Isolasi dicapai melalui fitur kernel Linux seperti namespaces (untuk process, network, filesystem) dan cgroups (untuk membatasi CPU, memory, I/O). Ini lebih ringan tapi juga berarti jika ada vulnerability di kernel, bisa berdampak ke semua container.
   - Dalam aspek keamanan, VM memberikan security boundary yang lebih kuat. Karena escape dari VM ke host sangat sulit karena harus menembus hypervisor. Sedangkan container  punya attack surface lebih besar karena berbagi kernel. Meskipun ada teknologi seperti seccomp, AppArmor, dan SELinux untuk hardening, container escape tetap lebih mungkin terjadi dibanding VM escape.
   - Dari segi overheadnya, VM lebih berat karena setiap VM menjalankan OS lengkap. Sedangkan conntainer jauh lebih efisien karena hanya menjalankan aplikasi dan dependensinya, berbagi kernel host.
     
5. Apa dampak limit memori terhadap aplikasi yang boros memori?

    Jawaban: Dampak limit memori terhadap aplikasi yang boros memori yaitu akan besar kemungkinan adanya risiko error atau gagal memproses data, aplikasi bisa dihentikan paksa, beberapa fitur aplikasi tidak berjalan, respons aplikasi menjadi sangat lambat, dan sebenarnya masih banyak lagi dampak dari limit memori terhadap aplikasi yang boros memori tersebut.  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  
Bagian paling menantang minggu ini adalah memahami perilaku penggunaan memori container Docker, terutama membedakan dampak menjalankan container dengan dan tanpa resource limit serta membaca hasil output penggunaan memori.

- Bagaimana cara Anda mengatasinya?  

Cara mengatasinya adalah dengan melakukan eksperimen langsung menggunakan Docker, mengamati output secara bertahap, serta membandingkan hasil eksekusi container tanpa limit dan dengan limit agar konsep resource limiting lebih mudah dipahami. Dan juga meminta bantuan dari teman dan teknologi yang berkembang saat ini.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
