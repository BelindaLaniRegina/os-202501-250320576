
# Laporan Praktikum Minggu [14]
Topik: Penyusunan Laporan Praktikum Format IMRAD
---

## Identitas
- **Nama**: Belinda Lani Regina
- **NIM**: 250320576
- **Kelas**: 1DSRA

---
# Perbandingan Algoritma Page Replacement FIFO dan LRU dalam Manajemen Memori Virtual

## 1. Pendahuluan

### 1.1 Latar Belakang
Manajemen memori merupakan salah satu fungsi kritis dalam sistem operasi modern. Dengan meningkatnya kebutuhan aplikasi terhadap ruang memori yang lebih besar daripada kapasitas RAM fisik yang tersedia, sistem operasi menggunakan teknik memori virtual untuk memberikan ilusi ruang memori yang lebih besar. Ketika memori fisik penuh dan diperlukan halaman baru, sistem operasi harus memutuskan halaman mana yang akan diganti, proses ini disebut page replacement.

Algoritma page replacement yang efisien sangat penting untuk meminimalkan page fault, yaitu kondisi ketika halaman yang dibutuhkan tidak ada di memori utama dan harus diambil dari disk. Page fault yang tinggi dapat menyebabkan penurunan performa sistem secara signifikan karena akses disk jauh lebih lambat dibanding akses RAM.

### 1.2 Rumusan Masalah
1. Bagaimana cara kerja algoritma FIFO dan LRU dalam menangani page replacement?
2. Algoritma mana yang menghasilkan jumlah page fault lebih sedikit pada reference string tertentu?
3. Apa kelebihan dan kekurangan masing-masing algoritma dalam konteks implementasi praktis?

### 1.3 Tujuan Penelitian
1. Dapat engimplementasikan algoritma page replacement FIFO dan LRU dalam program simulasi
2. Dapat membandingkan performa kedua algoritma berdasarkan jumlah page fault yang dihasilkan
3. Dapat menganalisis karakteristik dan trade-off antara kesederhanaan implementasi dan efisiensi performa

---

## 2. Metode 

### 2.1 Lingkungan Uji
- **Bahasa Pemrograman**: Python
- **Platform**: Sistem operasi dengan Python 
- **Tools**: Visual Studio Code

### 2.2 Dataset Uji
Reference string yang digunakan dalam eksperimen ini adalah:
```
7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2
```
Total 13 referensi halaman dengan jumlah frame memori yang tersedia sebanyak **3 frame**.

### 2.3 Parameter Eksperimen
- **Jumlah Frame**: 3 frame memori fisik
- **Panjang Reference String**: 13 akses halaman
- **Algoritma yang Diuji**: FIFO (First-In-First-Out) dan LRU (Least Recently Used)

### 2.4 Langkah Eksperimen
1. **Inisialisasi**: Membuat array frame dengan ukuran 3, diisi dengan '-' (kosong)
2. **Iterasi Reference String**: Untuk setiap halaman dalam reference string:
   - Cek apakah halaman ada di memori (hit) atau tidak (fault)
   - Jika fault dan ada slot kosong, masukkan halaman ke slot kosong
   - Jika fault dan tidak ada slot kosong, pilih halaman yang akan diganti berdasarkan algoritma:
     - **FIFO**: Ganti halaman yang paling lama masuk (oldest)
     - **LRU**: Ganti halaman yang paling lama tidak diakses
3. **Pencatatan**: Catat setiap langkah simulasi dan hitung total page fault
4. **Analisis**: Bandingkan hasil kedua algoritma

### 2.5 Cara Pengukuran
Metrik yang digunakan adalah **jumlah page fault**, yaitu berapa kali sistem harus mengambil halaman dari disk karena tidak tersedia di memori. Semakin rendah jumlah page fault, semakin baik performa algoritma.

---

## 3. Hasil 

### 3.1 Hasil Simulasi FIFO

Tabel di bawah menunjukkan proses page replacement menggunakan algoritma FIFO:

| Page | Frame 1 | Frame 2 | Frame 3 | Status |
|:----:|:-------:|:-------:|:-------:|:------:|
| 7    | 7       | -       | -       | FAULT  |
| 0    | 7       | 0       | -       | FAULT  |
| 1    | 7       | 0       | 1       | FAULT  |
| 2    | 2       | 0       | 1       | FAULT  |
| 0    | 2       | 0       | 1       | HIT    |
| 3    | 2       | 3       | 1       | FAULT  |
| 0    | 2       | 3       | 0       | FAULT  |
| 4    | 4       | 3       | 0       | FAULT  |
| 2    | 4       | 2       | 0       | FAULT  |
| 3    | 4       | 2       | 3       | FAULT  |
| 0    | 4       | 2       | 3       | FAULT  |
| 3    | 4       | 2       | 3       | HIT    |
| 2    | 4       | 2       | 3       | HIT    |

**Total Page Fault (FIFO): 10**

### 3.2 Hasil Simulasi LRU

Tabel di bawah menunjukkan proses page replacement menggunakan algoritma LRU:

| Page | Frame 1 | Frame 2 | Frame 3 | Status |
|:----:|:-------:|:-------:|:-------:|:------:|
| 7    | 7       | -       | -       | FAULT  |
| 0    | 7       | 0       | -       | FAULT  |
| 1    | 7       | 0       | 1       | FAULT  |
| 2    | 2       | 0       | 1       | FAULT  |
| 0    | 2       | 0       | 1       | HIT    |
| 3    | 2       | 0       | 3       | FAULT  |
| 0    | 2       | 0       | 3       | HIT    |
| 4    | 4       | 0       | 3       | FAULT  |
| 2    | 4       | 0       | 2       | FAULT  |
| 3    | 4       | 0       | 3       | FAULT  |
| 0    | 4       | 0       | 3       | HIT    |
| 3    | 4       | 0       | 3       | HIT    |
| 2    | 4       | 2       | 3       | FAULT  |

**Total Page Fault (LRU): 9**

### 3.3 Perbandingan Hasil

| Algoritma | Jumlah Frame | Jumlah Page Fault | 
|:---------:|:------------:|:-----------------:|
| FIFO      | 3            | 10                |
| LRU       | 3            | 9                 |

### 3.4 Visualisasi Hasil

![alt text](<screenshots/Page Replacement FIFO dan LRU.png>)
---

## 4. Pembahasan

### 4.1 Analisis Hasil

Pada langkah ke-7 reference string (akses halaman 0), terjadi perbedaan signifikan:
- **FIFO**: Mengalami fault karena halaman 0 sudah diganti oleh halaman 3
- **LRU**: Mengalami hit karena halaman 0 masih ada di memori (baru saja diakses di langkah ke-5)

Perbedaan ini menunjukkan bahwa LRU lebih baik dalam menangani pola akses berulang yang sering terjadi pada program nyata.


### 4.2 Interpretasi Hasil

Berdasarkan hasil eksperimen yang sudah dilakukan, algoritma LRU menghasilkan jumlah page fault yang lebih sedikit (9 fault) dibandingkan FIFO (10 fault) pada reference string yang sama dengan 3 frame memori. Perbedaan ini terjadi karena perbedaan fundamental dalam strategi pemilihan halaman yang akan diganti.

**FIFO** menggunakan prinsip antrian sederhana dimana halaman yang paling lama berada di memori akan diganti terlebih dahulu, tanpa mempertimbangkan apakah halaman tersebut masih sering digunakan atau tidak. Pada kasus reference string yang diuji, pendekatan ini kurang optimal karena kadang mengganti halaman yang sebenarnya masih akan diakses dalam waktu dekat.

**LRU** menggunakan prinsip lokalitas temporal, yaitu asumsi bahwa halaman yang baru saja diakses cenderung akan diakses lagi dalam waktu dekat. Dengan mengganti halaman yang paling lama tidak diakses, LRU mempertahankan working set yang lebih baik di memori, sehingga mengurangi kemungkinan page fault.

### 4.3 Kelebihan dan Kekurangan

**Algoritma FIFO:**
- Kelebihan: Implementasi sangat sederhana, overhead rendah, hanya memerlukan queue sederhana
- Kekurangan: Tidak mempertimbangkan frekuensi akses, rentan terhadap Belady's Anomaly (penambahan frame justru bisa meningkatkan page fault), performa suboptimal pada banyak kasus

**Algoritma LRU:**
- Kelebihan: Performa lebih baik karena mengikuti prinsip lokalitas, tidak mengalami Belady's Anomaly, mendekati solusi optimal
- Kekurangan: Implementasi lebih kompleks, memerlukan struktur data tambahan untuk tracking akses, overhead lebih tinggi dalam sistem nyata

### 4.4 Keterbatasan Penelitian

1. Dataset terbatas, eksperimen hanya menggunakan satu reference string dengan panjang 13 akses. Pola akses yang berbeda mungkin menghasilkan hasil yang berbeda pula
2. Jumlah frame konstan, karena hanya menguji dengan 3 frame, padahal variasi jumlah frame dapat mempengaruhi perbedaan performa
3. Perbedaan Simulasi dan Implementasi Real terlihat, karena eksperimen ini adalah simulasi sederhana yang tidak memperhitungkan overhead implementasi aktual dalam sistem operasi

### 4.5 Perbandingan dengan Teori

Hasil eksperimen sesuai dengan teori yang menyatakan bahwa LRU umumnya menghasilkan performa lebih baik daripada FIFO. Namun, dalam sistem operasi nyata, implementasi LRU yang sempurna (true LRU) jarang digunakan karena overhead yang tinggi. Sebagai gantinya, sistem operasi menggunakan algoritma aproksimasi LRU seperti Clock Algorithm atau Second-Chance Algorithm yang menyeimbangkan antara performa dan kompleksitas.

---

## 5. Kesimpulan

1. LRU lebih efektif dibandingkan FIFO dalam mengurangi page fault. Pada pengujian dengan 3 frame memori, LRU menghasilkan lebih sedikit page fault daripada FIFO.
2. Perbedaan mekanisme algoritma memengaruhi kinerja. FIFO hanya berdasarkan urutan masuk halaman, sedangkan LRU mempertimbangkan riwayat penggunaan sehingga lebih sesuai dengan pola akses berulang.
3. Pemilihan algoritma perlu disesuaikan dengan kebutuhan sistem. LRU menawarkan efisiensi lebih baik tetapi lebih kompleks, sementara FIFO lebih sederhana dan cocok untuk sistem dengan sumber daya terbatas.

---

## Quiz

### 1. Mengapa format IMRAD membantu membuat laporan praktikum lebih ilmiah dan mudah dievaluasi?

**IMRAD** sendiri merupakan sebuah singkatan dari **I**ntroduction, **M**ethod, **R**esults, and **D**iscussion. Jadi, format IMRAD membantu membuat laporan praktikum lebih ilmiah dan mudah dievaluasi yaitu karena;

- **Membuat Tulisan Ilmiah Lebih Terstruktur**: IMRAD menyediakan kerangka kerja yang jelas untuk menyajikan penelitian atau eksperimen, memudahkan pembaca untuk menemukan informasi spesifik yang mereka butuhkan tanpa harus membaca seluruh dokumen.
- **Mengikuti standar ilmiah internasional**: Format ini telah menjadi standar dalam publikasi ilmiah di seluruh dunia, sehingga laporan praktikum yang menggunakan format ini dapat dengan mudah dipahami oleh akademisi dan praktisi dari berbagai negara.
- **Memisahkan fakta dari interpretasi**: Bagian Results menyajikan data objektif, sementara Discussion menyajikan interpretasi dan analisis. Pemisahan ini membuat laporan lebih objektif dan memungkinkan pembaca untuk membuat interpretasi sendiri berdasarkan data yang disajikan.
- **Memfasilitasi replikasi**: Dengan bagian Methods yang detail, peneliti lain dapat mereplikasi eksperimen untuk memverifikasi hasil, yang merupakan prinsip fundamental dalam metode ilmiah.
- **Memudahkan evaluasi**: Reviewer atau penilai dapat dengan mudah mengevaluasi validitas penelitian dengan memeriksa setiap bagian secara terpisah, seperti apakah metode sudah tepat, apakah hasil sudah akurat, dan apakah kesimpulan didukung oleh data.

### 2. Apa perbedaan antara bagian Hasil dan Pembahasan?

Perbedaan utama antara bagian Hasil dan Pembahasan adalah:

**Bagian Hasil:**
- Menyajikan data mentah dan fakta objektif dari eksperimen tanpa interpretasi
- Berisi angka, tabel, dan screenshot yang menunjukkan apa yang terjadi selama eksperimen
- Bersifat deskriptif dan netral, hanya melaporkan temuan
- Tidak memberikan opini atau analisis mendalam
- Contoh: "Algoritma LRU menghasilkan 9 page fault, sedangkan FIFO menghasilkan 10 page fault"

**Bagian Pembahasan:**
- Memberikan interpretasi dan analisis terhadap data yang disajikan di bagian Hasil
- Menjelaskan mengapa hasil tersebut terjadi dan apa artinya dalam konteks yang lebih luas
- Membandingkan hasil dengan teori, ekspektasi, atau penelitian sebelumnya
- Membahas keterbatasan, implikasi, dan rekomendasi
- Bersifat analitis dan evaluatif
- Contoh: "LRU menghasilkan page fault lebih sedikit karena mempertimbangkan riwayat akses halaman, sehingga lebih baik dalam menangani pola akses berulang yang umum terjadi pada program nyata"


### 3. Mengapa sitasi dan daftar pustaka penting, bahkan untuk laporan praktikum?

Sitasi dan daftar pustaka penting dalam laporan praktikum, yaitu karena;
- **Memberikan kredibilitas**, karena menunjukkan bahwa laporan didasarkan pada sumber terpercaya dan penelitian yang sudah ada, bukan hanya opini atau asumsi pribadi.
- **Menghindari plagiarisme**, karena mengakui kontribusi orang lain terhadap ide, teori, atau metode yang digunakan dalam praktikum adalah kewajiban etis akademik.
- **Memfasilitasi verifikasi**, karena pembaca dapat memeriksa sumber asli untuk memverifikasi klaim atau mempelajari topik lebih dalam.
- **Menunjukkan riset yang telah dilakukan**, karena daftar pustaka yang baik menunjukkan bahwa mahasiswa telah melakukan riset literatur yang memadai sebelum melakukan praktikum.
- **Membangun konteks akademik**, karena sitasi menghubungkan praktikum dengan body of knowledge yang lebih luas, menunjukkan bagaimana praktikum ini berhubungan dengan teori dan penelitian yang sudah ada.
- **Melatih praktik akademik yang baik**, karena membiasakan diri dengan sitasi sejak praktikum akan mempersiapkan mahasiswa untuk menulis karya ilmiah yang lebih kompleks di masa depan, seperti skripsi atau paper penelitian.
- **Menghormati hak intelektual**, dimana mengakui karya orang lain adalah bentuk penghargaan terhadap kontribusi mereka dalam pengembangan ilmu pengetahuan.

---

## Daftar Pustaka

1. Silberschatz, A., Galvin, P. B., & Gagne, G. (2018). *Operating System Concepts* (10th ed.). John Wiley & Sons.
2. Tanenbaum, A. S., & Bos, H. (2014). *Modern Operating Systems* (4th ed.). Pearson Education.
3. Arpaci-Dusseau, R. H., & Arpaci-Dusseau, A. C. (2018). *Operating Systems: Three Easy Pieces*. Arpaci-Dusseau Books. Chapter 22: Beyond Physical Memory: Policies.
4. Stallings, W. (2018). *Operating Systems: Internals and Design Principles* (9th ed.). Pearson Education.
5. https://parafraseindonesia.com/format-imrad/


## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?

Bagian yang paling menantang minggu ini yaitu tentang bagaimana cara membuat laporan dengan format IMRAD dengan baik dan benar.

- Bagaimana cara Anda mengatasinya?  

Cara saya mengatasinya yaitu dengan mencari beberapa referensi laporan praktikum dengan format IMRAD.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
