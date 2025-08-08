# Laporan Praktikum Sistem Operasi - Modul 3

**Nama**  : Lia Lusianti
**NIM**   : 240202869  
**Modul** : Modul 3 - Shared Memory (shmget & shmrelease)

## Tujuan Praktikum
Memahami dan mengimplementasikan fitur shared memory antar proses di dalam sistem operasi xv6.

## Hasil Implementasi

### a. File yang Ditambahkan / Dimodifikasi
- `shm.h` (baru)
- `vm.c`
- `sysproc.c`
- `usys.S`
- `syscall.h`, `syscall.c`
- `proc.c`, `proc.h`
- `defs.h`
- `user.h`

### b. Deskripsi Implementasi
- Menambahkan definisi `struct shmentry`, `shmtab`, dan `MAX_SHM`.
- Menambahkan syscall `shmget` dan `shmrelease`.
- Mengatur mapping ke alamat virtual `USERTOP - (i+1)*PGSIZE`.
- Menyesuaikan manajemen refcount shared memory.
- Menggunakan `mappages` dan `decref` untuk pengaturan virtual memory.

### c. Kendala
- Banyak error seperti:
  - `undefined reference to 'mappages'`
  - `struct shmentry has no member named 'refcount'`
  - `proc undeclared`
- Error karena lupa meng-include header `types.h`, `mmu.h`, `vm.h`.
- Typo pada nama fungsi atau field struct (`refcount` vs `refcnt`).
- Solusi: pastikan semua file saling terhubung dengan benar dan tidak mendefinisikan struct dua kali.

### d. Bukti Keberhasilan
Berhasil kompilasi dan menambahkan sistem shared memory.

> Bukti output: lampirkan screenshot di folder `screenshots/`

---

## Kesimpulan
Modul ini mengajarkan konsep shared memory sebagai metode komunikasi antar proses dan pentingnya manajemen virtual memory dalam sistem operasi xv6.

**Tanggal Praktikum**: 7 Agustus 2025