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

## **Hubungan Antar Task**
- **Prioritas:** FlashRedLedTask memiliki prioritas lebih tinggi daripada FlashGreenLedTask.  
- **Eksekusi:**  
  - Ketika **FlashRedLedTask** sedang berjalan, **FlashGreenLedTask** akan ditunda hingga **FlashRedLedTask** selesai.  
  - Kedua task menggunakan **critical section** untuk mengakses resource bersama, sehingga task lain tidak dapat menginterupsi akses ke resource tersebut.  
- **Konflik Resource:**  
  - Jika kedua task mencoba mengakses resource bersama secara bersamaan, task dengan prioritas lebih tinggi (FlashRedLedTask) akan mendapatkan akses terlebih dahulu.  
  - Setelah selesai, task dengan prioritas lebih rendah (FlashGreenLedTask) akan dilanjutkan.
 
  ## Foto Hardware
![foto hardware exercise 6](https://github.com/user-attachments/assets/0f3f461e-80f2-455d-bc05-d8ad68fc95de)


## Short Video Hardware
https://github.com/user-attachments/assets/6042b776-4f29-4994-93fb-6dab5e20d747

