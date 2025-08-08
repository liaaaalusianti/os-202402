# Laporan Praktikum Sistem Operasi - Modul 2

*Nama*  : Lia Lusianti 
*NIM*   : 240202869 
*Modul* : Modul 2 - Copy-On-Write (COW)

---

## Tujuan Praktikum
Mengimplementasikan mekanisme Copy-On-Write (COW) dalam proses fork di xv6 agar proses anak dan induk dapat berbagi halaman memori hingga salah satu melakukan penulisan.

---

## Hasil Implementasi

### a. File yang Dimodifikasi
- vm.c
- proc.c
- trap.c
- defs.h
- mmu.h

### b. Deskripsi Fitur Copy-On-Write
- Menambahkan bit PTE_COW untuk menandai page yang shared dengan mekanisme copy-on-write.
- Proses fork() akan menandai semua halaman user sebagai COW, dan menaikkan refcount.
- Ketika proses menulis ke halaman COW, terjadi page fault dan dilakukan duplikasi halaman baru.

---

### c. Langkah Implementasi
1. **Tambahkan flag PTE_COW di mmu.h**
2. **Edit cowuvm() di vm.c untuk membuat mapping COW**
3. **Tambahkan fungsi decref() dan incref() untuk refcount**
4. **Tangani page fault T_PGFLT di trap()**
5. *Handle alokasi ulang memori di saat page fault jika PTE_COW terdeteksi*
6. **Perbarui fork() di proc.c agar menggunakan cowuvm()**

---

### d. Kendala dan Solusi
1. *Page fault tidak tertangani*
   - Solusi: pastikan handler T_PGFLT mengakses proc dan walkpgdir() dengan benar.
2. *Refcount salah menyebabkan double free*
   - Solusi: gunakan fungsi incref() dan decref() secara hati-hati.
3. *Proses crash saat fork*
   - Solusi: debug dengan mencetak refcount dan validasi halaman.

---

### e. Hasil Pengujian

- Program rtest berjalan tanpa error.
- Memory usage efisien hingga proses menulis halaman sendiri.
- Tidak terjadi memory leak atau segfault.

> Bukti: Upload hasil screenshot rtest dan hasil uji ke folder screenshots/.

---

## Kesimpulan

Modul ini memperkenalkan teknik manajemen memori efisien di OS, yaitu Copy-On-Write. Fitur ini sangat penting dalam implementasi fork() modern agar lebih hemat memori.

*Tanggal Praktikum*: 7 Agustus 2025