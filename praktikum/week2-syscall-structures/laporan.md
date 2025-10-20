
# Laporan Praktikum Minggu [X]
Topik:  "Arsitektur Sistem Operasi dan Kernel"

---

## Identitas
- **Nama**  : Belinda Lani Regina 
- **NIM**   : 250320576
- **Kelas** : 1DSRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
> 1. Dapat menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.
> 2. Dapat menjelaskan konsep dan fungsi system call dalam sistem operasi.
> 3. Dapat mengidentifikasi jenis-jenis system call dan fungsinya.
> 4. Dapat mengamati alur perpindahan mode user ke kernel saat system call terjadi.
> 5. Dapat menggunakan perintah Linux untuk menampilkan dan menganalisis system call.

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

---

## Langkah Praktikum
1. Setup Environment
Gunakan Linux (Ubuntu/WSL).
Pastikan perintah strace dan man sudah terinstal.
Konfigurasikan Git (jika belum dilakukan di minggu sebelumnya).
•Eksperimen 1 – Analisis System Call Jalankan perintah berikut:
strace ls
Catat 5–10 system call pertama yang muncul dan jelaskan fungsinya.
Simpan hasil analisis ke results/syscall_ls.txt.
•Eksperimen 2 – Menelusuri System Call File I/O Jalankan:
strace -e trace=open,read,write,close cat /etc/passwd
Analisis bagaimana file dibuka, dibaca, dan ditutup oleh kernel.
•Eksperimen 3 – Mode User vs Kernel Jalankan:
dmesg | tail -n 10
Amati log kernel yang muncul. Apa bedanya output ini dengan output dari program biasa?
2. Diagram Alur System Call
Buat diagram yang menggambarkan alur eksekusi system call dari program user hingga kernel dan kembali lagi ke user mode.
Gunakan draw.io / mermaid.
Simpan di:
praktikum/week2-syscall-structure/screenshots/syscall-diagram.png
Commit & Push
git add .
git commit -m "Minggu 2 - Struktur System Call dan Kernel Interaction"
git push origin main

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
1. **System call berperan sebagai penghubung aman antara user mode dan kernel mode.**
   System call menjadi satu-satunya mekanisme resmi bagi aplikasi untuk meminta layanan dari kernel, sehingga menjaga agar aplikasi tidak langsung mengakses instruksi berhak istimewa yang dapat mengancam stabilitas dan keamanan sistem operasi.
2. **System call memastikan pengendalian hak akses dan validasi operasi.**
   Ketika aplikasi melakukan system call, OS akan melakukan pengecekan izin dan validasi parameter sebelum mengeksekusi operasi yang diminta. Proses ini mencegah aplikasi jahat melakukan tindakan berbahaya, seperti mengakses data sensitif atau merusak sistem.
3. **Keamanan system call dijaga melalui kombinasi mekanisme perangkat keras dan perangkat lunak.**
   Perangkat keras menyediakan mode privilege dan mekanisme trap, sedangkan perangkat lunak (kernel) menangani pemeriksaan, penyimpanan state, dan eksekusi layanan secara aman. Kombinasi ini menciptakan batas keamanan yang ketat antara aplikasi dan kernel.

## Tugas
     System call sangat penting untuk keamanan OS. Karena dapat kita lihat jika, system call adalah interface yang disediakan oleh sistem operasi bagi aplikasi software untuk meminta layanan dari kernel. Dari perspektif keamanan, system call adalah gerbang utama dan penjaga keamanan antara user mode dan kernel mode.
     System call adalah satu-satunya mekanisme yang sah bagi sebuah aplikasi untuk beralih dari user mode ke kernel mode. Ketika aplikasi membutuhkan layanan yang memerlukan hak akses tinggi (misalnya, membaca file, mengalokasikan memori, atau membuat proses baru), aplikasi harus melakukan system call. Proses ini memicu interrupt (software interrupt) yang menyebabkan CPU beralih ke kernel mode, dan kontrol dialihkan ke kode kernel yang terpercaya. Tanpa adanya system call, aplikasi dapat secara semena-mena menjalankan instruksi privileged di kernel mode, yang akan menghancurkan stabilitas dan keamanan sistem. Aplikasi jahat dapat dengan mudah mematikan proses lain, mengubah data sensitif, atau mengambil alih seluruh sistem.
     Jika dari Operating Systems: Three Easy Pieces oleh Remzi H. Arpaci-Dusseau dan Andrea C. Arpaci-Dusseau terdapat kutipan seperti "Without protection, any application could do anything it wanted to the system. Thus, we arrive at the principle of limited direct execution: when an application wants to perform some kind of restricted operation, it must cross the privilege boundary by making a system call. The OS, now running in kernel mode, can then check to see if the operation is allowed, and if so, perform it on behalf of the application.”. Jadi, dari kutipan tersebut dapat disimpulkan bahwa system call adalah mekanisme untuk "menyeberangi batas privilege" (cross the privilege boundary). Proses "pengecekan" (check) oleh OS inilah yang menjadi inti dari fungsi keamanan system call.
     Cara OS memastikan transisi user-kernel yang aman melalui sebuah protokol yang ketat yang ditegakkan oleh perangkat keras dan perangkat lunak. Perangkat Keras menyediakan fondasi dengan mode privilege dan instruksi trap. OS memanfaatkannya dengan mengonfigurasi handler yang terpercaya, beralih ke stack kernel, dan yang paling penting, tidak pernah mempercayai pengguna dengan selalu memvalidasi semua input. Kombinasi ini memastikan bahwa meskipun aplikasi jahat sekalipun, hanya dapat mengakses layanan kernel melalui pintu yang dijaga ketat dan sesuai dengan aturan yang ditetapkan oleh kernel.
      Jika dilihat dari "Modern Operating Systems" (edisi ke-4) oleh Andrew S. Tanenbaum dan Herbert Bos terdapat sebuah kutipan yang berisi "When a system call is made, the calling process is trapped into the kernel mode and the kernel starts executing. The kernel first saves the current registers so they can be restored later. Then it indexes into a table, the system call table, to find the pointer to the corresponding service routine. The kernel also checks the parameters for validity. This checking is crucial for security." Di situ Tanenbaum menekankan urutan kejadian trap, penyimpanan state, pencarian handler melalui tabel yang dikendalikan kernel, dan langkah kunci pemeriksaan parameter.
      Contoh system call yang sering digunakan di Linux adalah open(), read(), write(), close(), fork(), dan exit(). open() digunakan untuk membuka file, read() dan write() untuk membaca dan menulis data dari/ke file, close() untuk menutup file, fork() untuk membuat proses baru, dan exit() untuk mengakhiri program.

---

## Quiz
1. Apa fungsi utama system call dalam sistem operasi?
   **Jawaban: Fungsi utama system call dalam sistem operasi, yaitu: 
Interface: Menyediakan antarmuka terstandarisasi antara aplikasi dan OS.
Abstraksi: Menyembunyikan kompleksitas perangkat keras dari programmer.
Pengamanan (Security): Melindungi sistem dengan menjalankan kode privileged hanya di kernel mode dan memvalidasi setiap permintaan.
Manajemen Sumber Daya: Memungkinkan kernel mengelola dan mengalokasikan semua sumber daya sistem secara terpusat dan terkendali.
Portabilitas: Memudahkan porting aplikasi antar sistem operasi yang berbeda.**  
2. Sebutkan 4 kategori system call yang umum digunakan!
   **Jawaban: 4 kategori umum system call adalah manajemen proses, manajemen berkas, manajemen perangkat, dan manajemen komunikasi.**  
3. Mengapa system call tidak bisa dipanggil langsung oleh user program?
   **Jawaban: System call tidak bisa dipanggil langsung oleh user program karena alasan utamanya adalah pemisahan antara ruang pengguna dan ruang kernel. Dalam sistem operasi yang menerapkan ruang kernel terlindungi, kode tingkat pengguna tidak dapat mengakses kode kernel atau struktur data secara langsung. Hal ini mencegah kode tingkat pengguna merusak struktur data kernel dan memanggil rutin yang tidak tersedia untuk umum. Isolasi ini penting untuk mencegah kode pengguna merusak sistem.**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  Yang paling menantang minggu ini yaitu pada bagian praktikumnya.
- Bagaimana cara Anda mengatasinya?
  Cara saya mengatasinya yaitu berdikusi dengan teman saya.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
