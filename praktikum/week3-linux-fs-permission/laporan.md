
# Laporan Praktikum Minggu [3]
Topik: Manajemen File dan Permission di Linux

---

## Identitas
- **Nama**  : Belinda Lani Regina
- **NIM**   : 2503202576
- **Kelas** : 1DSRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
> 1. Dapat menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.
> 2. Dapat menggunakan perintah ls, pwd, cd, cat untuk navigasi file dan direktori.
> 3. Dapat menggunakan chmod dan chown untuk manajemen hak akses file.
> 4. Dapat menjelaskan hasil output dari perintah Linux dasar.
> 5. Dapat menyusun laporan praktikum dengan struktur yang benar.
> 6. Dapat mengunggah dokumentasi hasil ke Git Repository tepat waktu.

---

## Dasar Teori
1. Model Permission dan Keamanan Akses
Sistem operasi Unix/Linux menggunakan model permission discretionary access control dengan notasi rwx (read, write, execute) yang diterapkan untuk tiga entitas: owner, group, dan others. Setiap file dan direktori memiliki metadata permission yang menentukan hak akses pengguna secara granular.
2. Arsitektur Layered Sistem Operasi
Sistem operasi modern dirancang dengan arsitektur berlapis: user space (aplikasi dan shell) terisolasi dari kernel space. Komunikasi antara keduanya hanya dapat dilakukan melalui system call interface, yang berfungsi sebagai gateway terproteksi untuk mengakses resource sistem.
3. Kernel sebagai Resource Manager
Kernel bertindak sebagai privileged mediator yang mengelola semua resource hardware (storage, memory, CPU) dan menerapkan kebijakan keamanan. Kernel memvalidasi setiap request akses resource melalui mekanisme authentication dan authorization sebelum mengizinkan operasi.
4. Abstraksi Sistem Berkas
Sistem operasi menyediakan virtual file system (VFS) yang mengabstraksikan detail implementasi filesystem fisik (ext4, NTFS, dll). Abstraksi ini memungkinkan interface yang konsisten untuk operasi file terlepas dari underlying storage technology.
5. Isolasi Process dan User Space
Setiap proses berjalan dalam isolated execution environment dengan privilege terbatas. Sistem operasi menerapkan principle of least privilege dimana proses hanya dapat mengakses resource yang secara eksplisit diizinkan, mencegah konflik dan meningkatkan keamanan sistem.



---

## Langkah Praktikum
1. Setup Environment
Gunakan Linux (Ubuntu/WSL).
Pastikan folder kerja berada di dalam direktori repositori Git praktikum:
praktikum/week3-linux-fs-permission/

2. Eksperimen 1 – Navigasi Sistem File Jalankan perintah berikut:
pwd
ls -l
cd /tmp
ls -a
Jelaskan hasil tiap perintah.
Catat direktori aktif, isi folder, dan file tersembunyi (jika ada).

3. Eksperimen 2 – Membaca File Jalankan perintah:
cat /etc/passwd | head -n 5
Jelaskan isi file dan struktur barisnya (user, UID, GID, home, shell).

4. Eksperimen 3 – Permission & Ownership Buat file baru:
echo "Hello <NAME><NIM>" > percobaan.txt
ls -l percobaan.txt
chmod 600 percobaan.txt
ls -l percobaan.txt
Analisis perbedaan sebelum dan sesudah chmod.
Ubah pemilik file (jika memiliki izin sudo):
sudo chown root percobaan.txt
ls -l percobaan.txt
Catat hasilnya.

5. Eksperimen 4 – Dokumentasi
Ambil screenshot hasil terminal dan simpan di:
praktikum/week3-linux-fs-permission/screenshots/
Tambahkan analisis hasil pada laporan.md.

6.Commit & Push
git add .
git commit -m "Minggu 3 - Linux File System & Permission"
git push origin main

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
pwd
ls -l
cd /tmp
ls -a
cat /etc/passwd | head -n 5
echo "Hello <NAME><NIM>" > percobaan.txt
ls -l percobaan.txt
chmod 600 percobaan.txt
ls -l percobaan.txt
sudo chown root percobaan.txt
ls -l percobaan.txt
```
---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![alt text](<screenshots/praktikum week 3.png>)

---

## Analisis
- Makna dari hasil percobaan yang dilakukan, yaitu:
1. pwd → Menampilkan direktori kerja saat ini.
cd /tmp → Berpindah ke direktori sementara (/tmp), tempat file percobaan akan dibuat.
ls -a → Menampilkan semua file (termasuk yang tersembunyi) di /tmp.
2. cat /etc/passwd | head -n 5
Perintah ini menampilkan 5 baris pertama dari file /etc/passwd, yang berisi informasi akun-akun pengguna sistem, tujuannya hanya untuk melihat format dan isi dasar file sistem Linux.
3. echo "Hello <BELINDA LANI REGINA<250320576>>" > percobaan.txt
Perintah ini membuat file bernama percobaan.txt di dalam /tmp dan menuliskan teks "Hello <BELINDA LANI REGINA<250320576>>" ke dalamnya.
Operator > berarti menulis ulang (overwrite) isi file.
4. ls -l percobaan.txt
outpur awalnya -rw-r--r-- 1 root root ...
rw- → Pemilik (root) bisa membaca dan menulis file.
r-- → Grup dan pengguna lain hanya bisa membaca.
Pemilik dan grup file: root.
5. chmod 600 percobaan.txt
Mengatur izin menjadi rw-------, artinya:
Pemilik (root): bisa membaca dan menulis.
Grup dan pengguna lain: tidak memiliki akses sama sekali.
6. -rw-------
Pas dicek lagu hasilnya berhasil hanya root yang dapat mengakses file tersebut.
7. sudo chown root percobaan.txt
Mengubah pemilik file menjadi root.
Karena kamu sudah menjalankan terminal sebagai root, perintah ini sebenarnya tidak mengubah apa pun (pemiliknya memang sudah root).
8. Pas dicek lagi ls -l percobaan.txt
Hasilnya tetap -rw------- 1 root root ...

- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).
  -Hubungannya dengan fungsi karnel adalah Kernel adalah inti dari sistem operasi yang berfungsi sebagai penghubung antara perangkat keras dan perangkat lunak. Dalam percobaan ini, hampir semua perintah yang kamu jalankan bekerja melalui kernel.
Contohnya Ketika menjalankan echo "Hello..." > percobaan.txt, kernel:
Membuat file baru di sistem berkas (/tmp/percobaan.txt).
Menulis data ke dalam blok disk.
Saat menjalankan chmod 600 percobaan.txt atau chown root percobaan.txt, kernel:
Mengubah metadata file di struktur data inode (menyimpan informasi izin dan kepemilikan file).
Semua proses ini tidak dilakukan langsung oleh shell, tetapi shell mengirim permintaan ke kernel melalui system call seperti open(), write(), chmod(), dan chown().
Jadi, Kernel bertugas mengatur akses file, izin, serta mengelola keamanan dan isolasi antar pengguna di sistem.
   -Hubungannya dengan system call adalah System call adalah mekanisme agar program user space (seperti bash atau perintah echo, chmod, chown) dapat meminta layanan dari kernel.
Contohnya yaitu:
1. Perintah Linux: echo "..." > percobaan.txt
System Call yang Terlibat: open(), write(), close()
Fungsinya: Membuka file, menulis isi, lalu menutup file.
2. Perintah Linux: ls -l percobaan.txt
System Call: stat()
Fungsinya: Mengambil metadata file (izin, ukuran, waktu modifikasi).
Dengan kata lain, setiap perintah di shell tidak langsung mengubah hardware, melainkan meminta kernel melakukannya melalui system call.
3. Perintah Linux: chmod 600 percobaan.txt
System Call: chmod()
Fungsinya: Mengubah izin file di tabel inode.
4. Perintah Linux chown root percobaan.txt
System Call: chown()
Fungsinya: Mengubah kepemilikan file (UID dan GID).
  -Hubungannya Arsitektur OS
1. User space → Kamu menjalankan perintah di terminal (bash shell).
2. System call interface → Menjadi pintu masuk agar perintah dapat berinteraksi dengan kernel.
3. Kernel space → Kernel mengelola sistem berkas (ext4 atau lainnya) dan memperbarui atribut file sesuai permintaan.

- Perbedaan hasil di lingkungan OS berbeda (Linux vs Windows), yaitu:
1. Dalam Sistem File
Linux: Menggunakan sistem file seperti ext4, yang mendukung permission model rwx dan kepemilikan file (user:group).
Windows: Menggunakan NTFS, yang tidak memakai model rwx Unix-style; hak akses diatur lewat ACL (Access Control List).
2. Perintah chmod, chown
Linux: Bekerja penuh, mengubah izin dan kepemilikan secara langsung di sistem file.
Windows: Tidak ada secara asli (Windows pakai icacls untuk izin file).
3. Path dan Direktori
Linux: Menggunakan /home, /etc, /tmp, dll.
Windows: Menggunakan C:\Users\.
4.Pemilik File (root, user)
Linux: User real di Linux (root, non-root) dengan izin nyata.
Windows: User Windows (Administrator, dll).
5.Output ls -l
Linux: Menunjukkan izin nyata sistem Linux.
Windows: Tidak berlaku.

---

## Kesimpulan
Berdasarkan praktikum yang dilakukan, berikut adalah **2-3 poin kesimpulan utama**:
1. Permission Model Unix Efektif Mengatur Akses File
Percobaan `chmod 600` berhasil membuktikan bahwa model permission `rwx` di Linux memberikan kontrol akses yang granular dan efektif. Perubahan dari `rw-r--r--` (644) ke `rw-------` (600) secara instan mengisolasi akses file sehingga hanya pemilik (root) yang dapat membaca dan menulis, sementara user lain kehilangan semua akses.
2. Kernel Bertindak sebagai Mediator Sentral melalui System Call
Setiap operasi yang dilakukan (`echo`, `chmod`, `chown`, `ls`) tidak mengakses hardware secara langsung, tetapi melalui system call yang diteruskan ke kernel. Ini membuktikan arsitektur layered OS dimana kernel berfungsi sebagai jembatan terproteksi antara aplikasi user space dan resource sistem.
3. Perbedaan Fundamental Arsitektur Linux vs Windows
Percobaan mengungkap perbedaan mendasar dalam manajemen akses file: Linux menggunakan model permission Unix sederhana berbasis `rwx`, sedangkan Windows mengandalkan ACL yang lebih kompleks. Hal ini menunjukkan bagaimana desain arsitektur OS yang berbeda menghasilkan mekanisme keamanan yang berbeda pula.

---

## Quiz
1. Apa fungsi dari perintah chmod?
   **Jawaban: Menurut Abraham Silberschatz, Peter Baer Galvin, dan Greg Gagne, Operating System Concepts, 10th Edition, Wiley, 2018, fungsi dari perintah chmod adalah untuk mengubah izin akses (permissions) pada sebuah file atau direktori dalam sistem operasi yang mirip Unix (seperti Linux). chmod merupakan perintah dasar yang mengimplementasikan kebijakan kontrol akses sistem operasi dengan mengizinkan pengguna untuk mengatur siapa yang dapat melakukan apa terhadap file dan direktori mereka, sehingga memastikan keamanan dan integritas data.**  
2. Apa arti dari kode permission rwxr-xr--?
   **Jawaban:Berdasarkan penjelasan dalam OSTEP (Operating Systems: Three Easy Pieces), kode permission rwxr-xr-- memiliki arti sebagai berikut:
Interpretasi dari rwxr-xr--
Kode ini mewakili tiga kelompok permission yang berbeda, dibaca dari kiri ke kanan:
  -Tiga karakter pertama (rwx): User (Pemilik file)
r = read (baca) - diizinkan
w = write (tulis) - diizinkan
x = execute (eksekusi) - diizinkan, pemilik file memiliki akses penuh.
  -Tiga karakter berikutnya (r-x): Group (Grup pengguna)
r = read (baca) - diizinkan
w = write (tulis) - tidak diizinkan (ditandai dengan -)
x = execute (eksekusi) - diizinkan, anggota grup hanya bisa membaca dan mengeksekusi file, tetapi tidak bisa mengubahnya.
  -Tiga karakter terakhir (r--): Other (Pengguna lain)
r = read (baca) - diizinkan
w = write (tulis) - tidak diizinkan
x = execute (eksekusi) - tidak diizinkan, pengguna lain hanya bisa membaca file saja.**
3.Jelaskan perbedaan antara chown dan chmod 
   **Jawaban: Di "Operating System Concepts, 10th Edition" (Silberschatz et al., 2018) terdapat sebuah kutipan yang berbunyi "The chown command changes the owner of a file. Only the superuser can change the owner of a file to prevent users from giving away their files to avoid quota restrictions. The chmod command changes the protection mode of a file. The owner of a file can change the permissions to grant or deny access to the file." (Chapter 11, File-System Interface)
Jadi, dapat disimpulkan bahwa perbedaan dari chown dan chmod adalah jika chown berfungsi untuk mengubah kepemilikan/identitas pemilik dan ssdangkan chmod berfungsi untuk mengubah perlindungan sebuah akses.**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
Bagian yang paling menantang minggu ini adalah cara memahami materi
- Bagaimana cara Anda mengatasinya?
cara saya mengatasinya adalah dengan mencoba memahaminya

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
