
# Laporan Praktikum Minggu [12]
Topik:Virtualisasi Menggunakan Virtual Machine

---

## Identitas
- **Nama**  : Belinda Lani Regina
- **NIM**   : 250320576
- **Kelas** : 1DSRA

---

## Tujuan
1. Dapat menginstal perangkat lunak virtualisasi (VirtualBox/VMware).  
2. Dapat membuat dan menjalankan sistem operasi guest di dalam VM.  
3. Dapat mengatur konfigurasi resource VM (CPU, RAM, storage).  
4. Dapat menjelaskan mekanisme proteksi OS melalui virtualisasi.  
5. Dapat menyusun laporan praktikum instalasi dan konfigurasi VM secara sistematis.
---

## Dasar Teori
1. Virtualisasi adalah teknik untuk membuat abstraksi perangkat keras sehingga satu komputer fisik dapat menjalankan beberapa sistem operasi secara bersamaan dalam lingkungan yang terisolasi (Virtual Machine). (Silberschatz; OSTEP)
2. Hypervisor bertugas mengelola dan membagi sumber daya fisik seperti CPU, memori, dan I/O ke setiap VM, serta memastikan isolasi dan keamanan antar VM. Hypervisor dapat berjalan langsung di atas hardware atau di atas sistem operasi host. (Tanenbaum; Silberschatz)
3. Isolasi dan Efisiensi Sumber Daya, setiap VM berjalan secara independen sehingga kegagalan pada satu VM tidak memengaruhi VM lain. Virtualisasi meningkatkan efisiensi pemanfaatan hardware dan mendukung pengujian sistem tanpa risiko pada host. (OSTEP)
4. VirtualBox adalah contoh platform virtualisasi yang menyediakan virtual hardware lengkap, memungkinkan instalasi berbagai sistem operasi tamu pada satu host dengan konfigurasi yang fleksibel. (Oracle VirtualBox Documentation)

---

## Langkah Praktikum
1. **Instalasi Virtual Machine**
   - Instal VirtualBox atau VMware pada komputer host.  
   - Pastikan fitur virtualisasi (VT-x / AMD-V) aktif di BIOS.

2. **Pembuatan OS Guest**
   - Buat VM baru dan pilih OS guest (misal: Ubuntu Linux).  
   - Atur resource awal:
     - CPU: 1–2 core  
     - RAM: 2–4 GB  
     - Storage: ≥ 20 GB

3. **Instalasi Sistem Operasi**
   - Jalankan proses instalasi OS guest sampai selesai.  
   - Pastikan OS guest dapat login dan berjalan normal.

4. **Konfigurasi Resource**
   - Ubah konfigurasi CPU dan RAM.  
   - Amati perbedaan performa sebelum dan sesudah perubahan resource.

5. **Analisis Proteksi OS**
   - Jelaskan bagaimana VM menyediakan isolasi antara host dan guest.  
   - Kaitkan dengan konsep *sandboxing* dan *hardening* OS.

6. **Dokumentasi**
   - Ambil screenshot setiap tahap penting.  
   - Simpan di folder `screenshots/`.

7. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 12 - Virtual Machine"
   git push origin main
   ```

---

---

## Hasil Eksekusi
- Saat menginstal VirtualBox
![alt text](<screenshots/week12_4.png>)
![alt text](<screenshots/week12_5.png>)
![alt text](<screenshots/week12_6.png>)

- Mengecek fitur virtualisasi (VT-x / AMD-V) aktif di BIOS.
![alt text](<screenshots/week12_7.png>)
  
- OS Guest
![alt text](<screenshots/week12_1.png>)
![alt text](<screenshots/week12_2.png>)
![alt text](<screenshots/week12_3.png>)

---

## Analisis
- Ubah konfigurasi CPU dan RAM ke-1
![alt text](<screenshots/Ubah konfigurasi CPU dan RAM ke-1.jpeg>)
  - **CPU : 2**
  - **Base Memory : 4000mb**
- Ubah konfigurasi CPU dan RAM ke-2
![alt text](<screenshots/Ubah konfigurasi CPU dan RAM ke-2.jpeg>)
  - **CPU : 1**
  - **Base Memory : 2000mb**
  
1. Jelaskan bagaimana VM menyediakan isolasi antara host dan guest.
   
VM menyediakan isolasi antara host dan guest melalui hypervisor yang menjadi perantara akses ke hardware, sehingga guest OS tidak berinteraksi langsung dengan sistem host. Alokasi CPU dan RAM dibatasi sesuai konfigurasi VM, seperti terlihat pada gambar, di mana setiap VM hanya dapat menggunakan resource yang telah ditentukan. Dengan mekanisme ini, gangguan atau error yang terjadi di dalam guest tidak berdampak langsung pada host. Oleh karena itu, VM berfungsi sebagai sandbox pada level sistem operasi yang efektif dalam mendukung keamanan dan stabilitas sistem.
  
2. Kaitkan dengan konsep sandboxing dan hardening OS.
- Hardening pada Level VM:
  - Konfigurasi minimal sesuai kebutuhan: Ubah konfigurasi CPU dan RAM ke-1 hanya butuh 1 CPU dan 2 GB RAM, tidak berlebih.
  - Swap terbatas: Ubah konfigurasi CPU dan RAM ke-2 sudah pakai swap 18,2%, bisa jadi indikasi untuk penyesuaian memori.
  - Jaringan dikontrol: Jika tidak butuh jaringan, bisa dimatikan (seperti VM16 yang tampak tidak ada aktivitas jaringan).
- Hardening pada Level Host:
  - Hypervisor sebagai lapisan keamanan tambahan.
  - Host bisa di-hardening dengan mematikan layanan yang tidak perlu, mengamankan hypervisor, dan memisahkan jaringan VM dari host.
- Pemisahan Fungsi:
  - Ubah konfigurasi CPU dan RAM ke-1 (4 GB/2 CPU) mungkin untuk beban kerja lebih berat.
  - Ubah konfigurasi CPU dan RAM ke-2 (2 GB/1 CPU) mungkin untuk layanan ringan atau testing.
  - Pemisahan ini mencegah satu VM mengganggu performa atau keamanan VM lain.
Jadi kaitannya dengan konsep sandboxing dan hardening OS VM adalah bentuk sandboxing tingkat sistem, mengisolasi aplikasi dan OS di dalam lingkungan terpisah.


---

## Kesimpulan
1. Hypervisor Berhasil Menciptakan dan Mengisolasi Lingkungan Virtual Secara Efektif.
2. Virtualisasi Memungkinkan Fleksibilitas dan Efisiensi dalam Pengelolaan Sumber Daya.
3. Penggunaan Virtual Machine memudahkan proses pengujian, pembelajaran, dan simulasi sistem operasi tanpa risiko terhadap sistem utama.

---

## Quiz
1. Apa perbedaan antara host OS dan guest OS?

   Jawaban: Perbedaan antara host OS dan guest OS yaitu;
   - Sistem operasi host adalah perangkat lunak yang diinstal pada sistem komputer yang berkomunikasi dengan perangkat keras yang mendasarinya. Sedangkan sistem operasi tamu adalah perangkat lunak yang diinstal pada mesin virtual.
   - Sistem operasi host berjalan langsung pada perangkat keras, sedangkan sistem operasi guest berjalan pada mesin virtual.
   - Sistem operasi host dapat berdiri sendiri, namun sistem operasi guest dapat berupa tunggal atau ganda.
     
2. Apa peran hypervisor dalam virtualisasi?

   Jawaban: Peran hypervisor dalam virtualisasi yaitu untuk Hypervisor berfungsi mengelola dan membagi sumber daya hardware ke beberapa Virtual Machine, menyediakan abstraksi perangkat keras, serta menjaga isolasi dan keamanan antar VM agar dapat berjalan bersamaan secara efisien. Ibaratnya Hypervisor seperti konduktor orkestra dan manajer gedung teater sekaligus. Dimana Hypervisor harus mengalokasikan waktu (CPU) dan bagian (sumber daya) ke setiap pemain (VM) seperti konduktor dan juga enyediakan panggung terpisah yang terisolasi (memori, I/O) untuk setiap pertunjukan, memastikan tidak saling ganggu, dan mengatur akses ke fasilitas fisik (listrik, jaringan), sebagai manajeer gedung.

     
3. Mengapa virtualisasi meningkatkan keamanan sistem?
 
   Jawaban: Virtualisasi meningkatkan keamanan sistem karena;
   - Setiap Virtual Machine terpisah, sehingga serangan atau error pada satu VM tidak menyebar ke VM lain atau host.
   - Hypervisor mengontrol akses CPU, memori, dan I/O, mencegah penyalahgunaan hardware.
   - Aplikasi-aplikasi yang berisiko dapat dijalankan di VM tanpa membahayakan sistem utama.
   - Snapshot dan cloning memudahkan rollback sistem setelah terjadi kegagalan atau serangan.
---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?

  Bagian yang paling menantang minngu ini yaitu tentang menganalisis praktikum.
   
- Bagaimana cara Anda mengatasinya?

  Cara saya mengatasinya yaitu dengan mencoba lebih dalam saat menganalisis, juga dengan dibantu oleh teman maupun teknologi saat ini.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
