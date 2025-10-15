
# Laporan Praktikum Minggu [X]
Topik: "Arsitektur Sistem Operasi dan Kernel"

---

## Identitas
- **Nama**  : Belinda Lani Regina  
- **NIM**   : 250320576
- **Kelas** : 1DSRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
> Dapat menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.
> Mengidentifikasi komponen utama OS (kernel, system call, device driver, file system).
> Membandingkan model arsitektur OS (monolithic, layered, microkernel).
> Menggambarkan diagram sederhana arsitektur OS menggunakan alat bantu digital (draw.io / mermaid).

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.
> Pengertian Sistem Operasi dan Kernel, sistem operasi (OS) adalah perangkat lunak inti yang mengelola perangkat keras dan menyediakan layanan untuk program aplikasi.
Kernel adalah komponen inti dari sistem operasi yang berperan sebagai perantara antara perangkat keras dan perangkat lunak.
> Konsep Sistem Operasi dan Kernel, sistem operasi mengatur dan mengelola perangkat keras serta sumber daya sistem. Di Linux, komponen utama dari sistem operasi adalah kernel, yang bertanggung jawab atas manajemen memori, proses, sistem file, dan perangkat keras.
> Jenis-Jenis Arsitektur Kernel, Monolithic Kernel: Seluruh layanan sistem berjalan dalam mode kernel. Contoh: Linux.
Microkernel: Hanya fungsi dasar yang berjalan di kernel, layanan lainnya berjalan di ruang pengguna. Contoh: Minix, QNX.
Hybrid Kernel: Gabungan monolithic dan microkernel. Contoh: Windows NT, macOS.

---

## Langkah Praktikum
1. Setup Environment
Pastikan Linux (Ubuntu/WSL) sudah terinstal.
Pastikan Git sudah dikonfigurasi dengan benar:
git config --global user.name "Nama Anda"
git config --global user.email "email@contoh.com"
Diskusi Konsep
Baca materi pengantar tentang komponen OS.
Identifikasi komponen yang ada pada Linux/Windows/Android.
Eksperimen Dasar Jalankan perintah berikut di terminal:
uname -a
whoami
lsmod | head
dmesg | head
Catat dan analisis modul kernel yang tampil.
Membuat Diagram Arsitektur
Buat diagram hubungan antara User → System Call → Kernel → Hardware.
Gunakan draw.io atau Mermaid.
Simpan hasilnya di:
praktikum/week1-intro-arsitektur-os/screenshots/diagram-os.png
Penulisan Laporan
Tuliskan hasil pengamatan, analisis, dan kesimpulan ke dalam laporan.md.
Tambahkan screenshot hasil terminal ke folder screenshots/.
Commit & Push
git add .
git commit -m "Minggu 1 - Arsitektur Sistem Operasi dan Kernel"
git push origin main
2. Perintah yang dijalankan adalah
uname -a
lsmod | head
dmesg | head
4. File dan kode yang dibuat.  
5. Commit message yang digunakan.

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
![atl text](screenshots/example.png)

---

## Analisis
- Perintah uname -a, menampilkan versi kernel dan pld  form Anda — menunjukkan bahwa ini adalah sistem 64-bit, berjalan dalam WSL2.
Perintah whoami, menunjukkan bahwa Anda saat ini login sebagai root.
Perintah lsmod | head, Deteksi CPU menunjukkan Intel dan AMD — ini umum di lingkungan virtualisasi atau jika CPU memiliki teknologi campuran.
Perintah dmesg | head, untuk melihat ringkasan awal dari log kernel  
- Hubungan hasil dengan teori (fungsi kernel, system call, arsitektur OS) yaitu:
* Dengan adanya fungsi kernel Kernel memulai sistem, mendeteksi CPU & memori
* System call digunakan untuk akses hardware & konfigurasi sistem awal
* Dengan adanya arsitektur OS, Menunjukkan kernel Linux berjalan di atas Windows (arsitektur hybrid).
-Perbedaan hasil di lingkungan OS berbeda (Linux vs Windows) yaitu WSL2 (Linux di atas Windows)
•Cocok untuk pengembangan, scripting, dan testing Linux tools di Windows.
•Tidak cocok untuk operasi kernel-level atau akses hardware langsung.
Linux Asli (native)
•Cocok untuk penggunaan penuh: server, embedded system, konfigurasi kernel, dll

---

## Kesimpulan
kesimpulan dari praktikum ini, yaitu:
1. Perintah uname -a dan whoami menunjukkan bahwa sistem yang digunakan adalah Linux 64-bit yang berjalan di lingkungan WSL2 dengan akses root, menandakan penggunaan Linux virtual di atas Windows.
2. Deteksi modul kernel (lsmod | head) dan log awal kernel (dmesg | head) mengonfirmasi fungsi kernel dalam mendeteksi perangkat keras (CPU Intel dan AMD) dan memulai sistem menggunakan system call untuk konfigurasi awal, sesuai dengan teori arsitektur dan fungsi kernel.
3. Perbedaan lingkungan OS terlihat dari WSL2 yang cocok untuk pengembangan dan pengujian Linux di Windows dengan keterbatasan akses hardware langsung, sedangkan Linux native lebih optimal untuk penggunaan penuh seperti server dan pengelolaan kernel.


---
## Tugas
Perbedaan monolithic kernel, microkernel, dan layered architecture dapat dilihat dari arti tiap model itu sendiri. Seperti menurut rifqimulyawan.com, monoholic karnel adalah kerangka perangkat lunak sistem operasi yang menyimpan semua hak istimewa untuk mengakses perangkat input/output (I/O), memori, interupsi perangkat keras, dan tumpukan CPU. Kernel monolitik cenderung lebih besar dari kernel lain karena mereka berurusan dengan begitu banyak aspek pemrosesan komputer di level terendah, dan karenanya harus memasukkan kode yang berinteraksi dengan banyak perangkat, I/O dan saluran interupsi, dan operator perangkat keras lainnya. Contoh nyata dari implementasi Monolithic karnel adalah karnel linux dan karnel-karnel unix tradisional seperti BSD, yang memvalidasi definisi arsitektur. 

Lalu jika menurut geeksforgeeks.com Mikrokernel adalah jenis Sistem Operasi yang menyediakan beberapa layanan dasar untuk sistem operasi. Layanan ini meliputi manajemen memori, penjadwalan proses, dll. Beberapa layanan lain seperti Driver Perangkat, Sistem Berkas, dll. dikelola oleh proses tingkat pengguna. Proses Tingkat Pengguna berkomunikasi dengan Microkernel melalui pengiriman pesan. Cara penanganan proses ini membuat mikrokernel lebih modular dan lebih fleksibel dibandingkan kernel monolitik tradisional. Keuntungan utama arsitektur microkernel adalah menyediakan sistem operasi yang lebih aman dan stabil. Karena hanya layanan-layanan terpenting yang berjalan di ruang kernel, permukaan serangan sistem operasi berkurang, sehingga menyulitkan penyerang untuk mengeksploitasi kerentanan. Kerugian utama mikrokernel adalah pengiriman pesan antar proses tingkat pengguna bisa lebih lambat daripada panggilan sistem langsung dalam kernel monolitik. Hal ini dapat mempengaruhi kinerja sistem operasi, terutama pada aplikasi-aplikasi berkinerja tinggi. Secara keseluruhan, arsitektur microkernel dapat menyediakan sistem operasi yang lebih aman dan fleksibel, tetapi juga dapat menimbulkan beberapa kompromi antara kinerja dan kompleksitas. 

Dan sedangkan menurut baeldung.com layerd architecture disebut-sebut sebagai kerangka kerja arsitektur yang paling umum dan banyak digunakan dalam pengembangan perangkat lunak. Arsitektur ini juga dikenal sebagai arsitektur n-tier dan menggambarkan pola arsitektur yang terdiri dari beberapa lapisan horizontal terpisah yang berfungsi bersama sebagai satu unit perangkat lunak, lalu lapisan itu juga merupakan pemisahan logis dari komponen atau kode. Karakteristik utama kerangka kerja ini adalah lapisan-lapisan hanya terhubung ke lapisan-lapisan tepat di bawahnya. Pada ilustrasi sebelumnya, lapisan 1 hanya terhubung ke lapisan 2, lapisan 2 terhubung ke lapisan 3, dan lapisan 1 terhubung ke lapisan 3 hanya melalui lapisan 2. Jumlah lapisan dalam layerd architecture tidak ditetapkan pada angka tertentu dan biasanya tergantung pada pengembang atau arsitek perangkat lunak. Perlu dicatat bahwa kerangka kerja ini biasanya selalu memiliki lapisan interaksi pengguna, lapisan untuk pemrosesan, dan lapisan yang menangani pemrosesan data. Keuntungan dari layerd architecture adalah kerangka kerjanya sederhana dan mudah dipelajari serta diterapkan, ketergantungan berkurang karena fungsi setiap lapisan terpisah dari lapisan lainnya, pengujian lebih mudah karena komponen-komponennya terpisah, setiap komponen dapat diuji secara individual, biaya overhead cukup rendah. Lalu adapun kekurangan dari layers architecture sendiri yaitu skalabilitas sulit karena struktur kerangka kerjanya tidak memungkinkan pertumbuhan, sistem ini sulit dirawat, perubahan pada satu lapisan saja dapat mempengaruhi keseluruhan sistem karena sistem tersebut beroperasi sebagai satu kesatuan, terdapat saling ketergantungan antara lapisan karena suatu lapisan bergantung pada lapisan di atasnya untuk menerima data, dan pemrosesan paralel tidak dimungkinkan.

Contoh OS yang menerapkan tiap model yaitu:
1.	Monolithic Karnel, Linux dan karnel-karnel unix tradisional seperti BSD.
2.	Microkarnel, Minix dan QNX.
3.	Layerd architecture seperti yang digunakan pada TCP/IP stack di kebanyakan OS modern. 

Menurut saya dan sumber sumber yang saya cari, yang paling relevan untuk sistem modern adalah Hybrid Kernel (gabungan dari monolithic karnel dan microkarnel) adalah yang paling relevan untuk sistem modern. Karena Hybrid Kernel menggabungkan kelebihan dari Monolithic Kernel dan Microkernel. Seperti contohnya Kecepatan Monolithic (Kinerja Tinggi), layanan OS yang paling sering digunakan dan sensitif terhadap waktu (seperti thread scheduling dan manajemen memori dasar) ditempatkan di ruang kernel. Ini memungkinkan eksekusi cepat karena tidak ada overhead komunikasi antar proses (Inter-Process Communication / IPC) yang intensif. Dan Stabilitas Microkernel (Keandalan), layanan yang lebih besar atau rentan terhadap bug (seperti device driver atau file system tertentu) dipindahkan ke ruang pengguna atau diisolasi sebagai modul. Jika modul ini crash, kernel inti tetap berjalan, sehingga sistem tidak langsung hang atau crash total (Blue Screen). Juga saat ini sistem modern seperti Microsoft Windows dan MacOS menggunakan Hybrid Karnel. Maka dari itu yang paling relavan untuk sistem modern adalah Hybrid Karnel (gabungan dari monolithic karnel dan microkarnel).


## Quiz
1. Sebutkan tiga fungsi utama sistem operasi
   **Jawaban:Fungsi utama sistem operasi  
•Manajemen Proses
•Manajemen Memori
•Manajemen I/O
•Manajemen Sistem Berkas**  
2.Jelaskan perbedaan antara kernel mode dan user mode.
   **Jawaban:perbedaan antara kernel mode dan user mode yaitu jika user mode menjalankan aplikasi standar dengan akses terbatas ke sumber daya sistem, sementara kernel mode menjalankan OS inti dengan kendali penuh atas perangkat keras.**  
3. Sebutkan contoh OS dengan arsitektur monolithic dan microkernel.
   **Jawaban: Contoh OS dengan arsitektur monolithic adalah Linux, DOS, Microsoft Windows, Solaris, dan OpenVMS. Sedangkan microkernel adalah MINIX, QNX, Symbian OS, dan L4.**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  Yanng paling menantang minggu ini yaitu tentang kebingungan dalam bagaimana cara yang benar untuk melakukan pratikum yang di perintahkan  
- Bagaimana cara Anda mengatasinya?
  Cara saya mengatasi hal tersebut ya itu dengan bertanya kepada teman, chatgpt, dan juga referensi dari internet.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
