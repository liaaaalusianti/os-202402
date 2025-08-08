# Laporan Praktikum Sistem Operasi - Modul 4

*Nama*  : Lia Lusianti  
*NIM*   : 240202869 
*Modul* : Modul 4 - Copy-On-Write (COW)

## Tujuan Praktikum
Mengimplementasikan mekanisme Copy-On-Write (COW) di sistem operasi xv6, agar proses child dapat berbagi page dengan parent sampai terjadi penulisan.

## Hasil Implementasi

### a. File yang Ditambahkan / Dimodifikasi
- vm.c
- trap.c
- proc.c
- defs.h, mmu.h, sysproc.c
- Header baru yang mendukung virtual memory (jika diperlukan: vm.h, pde_t.h)

### b. Deskripsi Implementasi
- Menambahkan flag PTE_COW di mmu.h.
- Menyesuaikan fork() agar menggunakan cowuvm() untuk copy memory.
- Fungsi cowuvm() tidak melakukan copy fisik, tapi menaikkan refcount dan tandai dengan PTE_COW.
- Pada trap(), saat terjadi page fault (T_PGFLT) terhadap halaman PTE_COW, sistem akan:
  - Alokasikan page baru
  - Copy isi halaman lama ke baru
  - Update page table anak untuk menggunakan halaman baru
  - Kurangi refcount lama

### c. Kendala
- Banyak error seperti:
  - walkpgdir, decref undefined → harus include vm.h dan definisikan fungsi
  - Redefinisi fungsi cowuvm, error label bad: → harus hati-hati penempatan return dan block
  - refcount salah akses → pastikan incref dan decref sesuai alokasi memori
- Konflik pada nama shmtab, proc, atau pgdir antar modul

### d. Bukti Keberhasilan
Berhasil menjalankan sistem dengan COW aktif dan tidak terjadi duplikasi page saat fork(), sampai ada proses yang menulis.

> Bukti output: tambahkan screenshot hasil uji fork() + ptest di folder screenshots/

---

## Kesimpulan
Modul ini memperkenalkan efisiensi manajemen memori dengan teknik Copy-On-Write, yang sangat berguna untuk menghemat penggunaan page saat fork.

*Tanggal Praktikum*: 7 Agustus 2025