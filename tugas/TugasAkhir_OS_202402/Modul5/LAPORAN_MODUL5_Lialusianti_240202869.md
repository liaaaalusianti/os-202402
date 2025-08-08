# Laporan Praktikum Sistem Operasi - Modul 5

*Nama*  : Lia Lusianti 
*NIM*   : 240202869 
*Modul* : Modul 5 - Read-Only File (Mode)

---

## Tujuan Praktikum
Menambahkan fitur mode file "read-only" ke dalam sistem operasi xv6, sehingga file tertentu tidak bisa ditulis jika telah diset ke mode tersebut.

---

## Hasil Implementasi

### a. File yang Dimodifikasi
- file.c
- file.h
- fs.c
- fs.h
- user.h
- syscall.c
- sysproc.c
- usys.S

### b. Deskripsi Perubahan
1. **Menambah field mode di struct inode**  
   → short mode; // 0 = read-write (default), 1 = read-only)

2. *Menambahkan syscall baru:*
   - int chmod(int fd, int mode); untuk mengganti mode file.

3. **Modifikasi fungsi filewrite()**
   - Tambah pengecekan:  
     c
     if(f->ip && f->ip->mode == 1) {
       return -1; // Tidak bisa menulis jika read-only
     }
     

4. **Registrasi syscall chmod() di kernel**
   - Tambahkan ke syscall.c, usys.S, dan user.h

---

### c. Kendala dan Error yang Dihadapi

1. **Error: struct inode has no member named 'mode'**
   - Solusi: Tambahkan field mode di fs.h dan pastikan tidak mendefinisikan ulang struct inode di tempat lain (hindari file.h buat struct baru).

2. **Error karena redefinisi struct inode**
   - Solusi: Hapus definisi duplikat inode di file.h agar tidak konflik dengan fs.h

3. **Kesalahan pointer ->mode tidak dikenali**
   - Penyebabnya karena salah include atau duplikat definisi.

4. *Perlu encode/decode mode ke dalam inode di disk (opsional)*
   - Jika mau permanen, tambahkan serialisasi mode di readi() dan writei(), tapi untuk sementara hanya di memory.

---

### d. Bukti Keberhasilan

- File dengan mode read-only tidak bisa ditulis, dan syscall chmod() berfungsi.
- Output dari program uji menunjukkan penulisan gagal saat file di-read-only-kan.

> Bukti: Upload screenshot uji chmod, tulis file, gagal write ke folder screenshots/.

---

## Kesimpulan

Dengan menambahkan fitur file mode, kita belajar bagaimana menangani izin akses dasar dalam file system xv6, serta bagaimana membuat syscall sendiri dan menyesuaikan kernel.

*Tanggal Praktikum*: 7 Agustus 2025