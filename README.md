# Praktikum RTOS - SEMESTER 5 (3 Teknik Komputer A)

- **Diva Sakananda (3222600013)**
- **Billy Lukito Danuharja (3222600027)**


# Task 6 Exercise	7	–	Demonstrate	that	the	sharing	of	resources in	a	multitasking	design	can	lead	to	a	deterioration	in system	performance

Proyek ini bertujuan untuk mendemonstrasikan cara mengeliminasi **resource contention** dalam sistem multitasking berbasis RTOS (Real-Time Operating System) pada mikrokontroler STM32. Teknik yang digunakan adalah **critical section**, yang memastikan hanya satu task dapat mengakses resource bersama pada satu waktu dengan menonaktifkan interrupt.

## **Fitur Utama**
1. **FlashGreenLedTask**  
   - Mengendalikan LED hijau secara periodik.  
   - Menggunakan critical section untuk melindungi resource bersama.  
   - Memiliki prioritas **Normal**, sehingga akan menunggu task dengan prioritas lebih tinggi selesai sebelum dijalankan.

2. **FlashRedLedTask**  
   - Mengendalikan LED merah dengan waktu periodik lebih singkat.  
   - Menggunakan critical section untuk melindungi resource bersama.  
   - Memiliki prioritas **Above Normal**, sehingga lebih sering mengakses resource bersama.  

## **Fungsi Utama**
- **taskENTER_CRITICAL()**  
  Menonaktifkan semua interrupt (kecuali Non-Maskable Interrupt/NMI) selama eksekusi critical section untuk memastikan akses resource bersama aman dari gangguan.

- **taskEXIT_CRITICAL()**  
  Mengaktifkan kembali interrupt setelah critical section selesai, memungkinkan multitasking dan interrupt berjalan normal.

- **SimulateReadWriteOperation()**  
  Mensimulasikan akses resource bersama dengan delay berbasis loop menggunakan instruksi no-operation (`__asm("nop")`). Teknik ini menghindari konflik pada fungsi delay berbasis interrupt.

## **Spesifikasi Task**
### FlashGreenLedTask  
- **Prioritas:** Normal  
- **Perilaku:**  
  - Menyalakan LED hijau selama 0,5 detik setiap periode tertentu.  
  - Menggunakan critical section untuk mengakses resource bersama.  

### FlashRedLedTask  
- **Prioritas:** Above Normal  
- **Perilaku:**  
  - Menyalakan LED merah selama 0,1 detik dengan periode lebih singkat.  
  - Menggunakan critical section untuk mengakses resource bersama.  

## **Tujuan Proyek**
1. Menunjukkan bagaimana sistem RTOS menangani resource contention.  
2. Meningkatkan pemahaman tentang penggunaan **critical section** untuk stabilitas multitasking.  
3. Mengoptimalkan performa multitasking pada mikrokontroler STM32.
