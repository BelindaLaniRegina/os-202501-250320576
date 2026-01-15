
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
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
