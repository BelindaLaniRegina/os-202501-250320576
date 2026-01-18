
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

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
lsmod | head
dmesg | head
```

---

## Hasil Eksekusi
- Saat menginstal VirtualBox
![alt text](<screenshots/week12_4.png>)
![alt text](<screenshots/week12_5.png>)
![alt text](<screenshots/week12_6.png>)

- OS Guest
![alt text](<screenshots/week12_1.png>)
![alt text](<screenshots/week12_2.png>)
![alt text](<screenshots/week12_3.png>)

---

## Analisis
- Jelaskan bagaimana VM menyediakan isolasi antara host dan guest.

  Virtual Machine (VM) berjalan di atas hypervisor (VirtualBox). Hypervisor berperan sebagai lapisan perantara antara host OS dan guest OS.
  
- Kaitkan dengan konsep sandboxing dan hardening OS.  

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
