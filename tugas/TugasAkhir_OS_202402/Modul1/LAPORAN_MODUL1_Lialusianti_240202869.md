# Laporan Praktikum Sistem Operasi - Modul 1

*Nama*  : Lia Lusianti  
*NIM*   : 240202869 
*Modul* : Modul 1 - Menambah System Call Baru

---

## Tujuan Praktikum
Menambahkan syscall baru ke dalam kernel xv6, memahami mekanisme syscall di level kernel-user, dan memastikan syscall dapat diakses dari program user space.

---

## Hasil Implementasi

### a. File yang Dimodifikasi
- syscall.c
- syscall.h
- usys.S
- user.h
- sysproc.c
- proc.c

### b. Deskripsi Syscall Baru
#### Syscall 1: int hello(void)
- Menampilkan string “Hello from xv6!” dari kernel.
- Return value: 0

#### Syscall 2: int getppid(void)
- Mengembalikan nilai pid dari parent process.
- Return value: parent PID (int)

#### Syscall 3: int getpinfo(struct pstat *)
- Menyediakan info tentang semua proses ke user.
- Struktur pstat harus ditambahkan di user.h dan proc.h

---

### c. Langkah Implementasi
1. **Menambahkan prototipe syscall di user.h dan syscall.h**
2. **Mendaftarkan syscall number di syscall.c**
3. **Menambahkan definisi syscall di sysproc.c**
4. **Mengedit usys.S untuk expose syscall ke user-space**
5. **Menguji syscall dengan program user (misal ptest.c)**

---

### d. Kendala dan Solusi
1. *Syscall tidak dikenali*
   - Penyebab: lupa daftarkan di usys.S atau syscall.c
2. *Struct tidak dikenal di user space*
   - Solusi: Definisikan struct di user.h
3. *Nilai return salah*
   - Debug dengan mencetak di dalam kernel dan user space

---

### e. Hasil Pengujian

- Memanggil hello() sukses mencetak pesan kernel.
- getppid() mengembalikan PID parent dengan benar.
- getpinfo() dapat mengisi data statistik proses (jumlah, state, dll).

> Bukti: Upload screenshot pemanggilan syscall ke folder screenshots/.

---

## Kesimpulan

Modul ini melatih cara menambahkan syscall dari nol dan menghubungkan kernel-space dengan user-space menggunakan mekanisme syscall standar di xv6.

*Tanggal Praktikum*: 7 Agustus 2025