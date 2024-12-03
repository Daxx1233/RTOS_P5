# Praktikum RTOS - SEMESTER 5 (3 Teknik Komputer A)
- Triyas Rahmadiyanti (3222600001)
- Duta Fithra Qolby (3222600003)
# EXERCISE 5 - Demonstrate access contention problems when using shared resources in a multitasking system.
## Deskripsi Projek
Proyek ini adalah implementasi sistem berbasis RTOS (Real-Time Operating System) yang mengontrol 
LED merah dan hijau pada sebuah mikroprosesor berbasis STM32. Sistem ini mengatur penjadwalan tugas yang menjalankan operasi nyala-mati 
untuk LED dengan menggunakan FreeRTOS.

Tujuan dari projek ini :
1. Mengelola tugas multitasking menggunakan thread dalam FreeRTOS.
2. Mengontrol LED merah dan hijau dengan pola nyala tertentu.
3. Mengimplementasikan mekanisme akses data bersama yang aman menggunakan flag untuk mencegah konflik data.

## Deskripsi Alur Kerja
1. Inisialisasi Sistem:
   - Mikroprosesor diinisialisasi dengan fungsi HAL_Init() dan SystemClock_Config().
   - GPIO diatur melalui fungsi MX_GPIO_Init() untuk mengontrol pin yang terhubung ke LED.
2. Konfigurasi RTOS:
   - Kernel FreeRTOS diinisialisasi dengan osKernelInitialize().
   - Dua thread utama didefinisikan:
      - greenLEDTask: Mengontrol LED hijau.
      - RedLEDTask: Mengontrol LED merah.
3. Penjadwalan:
   - RTOS memulai kernel menggunakan osKernelStart().
   - Tugas-tugas dijalankan secara paralel, dengan masing-masing memiliki prioritas tertentu.
4. Eksekusi Tugas:
   - Tugas Hijau (greenLEDTask):
     - LED hijau dinyalakan dan dimatikan dengan pola tertentu.
     - Fungsi accessData() digunakan untuk mengelola data bersama.
   - Tugas Merah (RedLEDTask):
     - LED merah dinyalakan dengan prioritas lebih tinggi.
     - Mengakses data bersama dengan mekanisme yang sama.
5. Akses Data Bersama: Fungsi accessData() memanfaatkan variabel flagg untuk menentukan kapan dan bagaimana data diakses,
   mencegah konflik selama tugas dijalankan secara bersamaan.

## Alur Eksekusi
1. Start Up: Mikrokontroler menginisialisasi seluruh sistem. Kemudian, kernel RTOS mulai menjalankan thread.
2. Tugas LED Hijau: LED hijau menyala selama 500 ms dan mati selama 500 ms. Fungsi accessData() memastikan akses data tidak tumpang tindih.
3. Tugas LED Merah: LED merah menyala dan mati lebih cepat (interval 100 ms). Fungsi yang sama digunakan untuk akses data.
4. RTOS Scheduler:
   - Mengatur eksekusi thread sesuai prioritas:
     - Tugas merah memiliki prioritas lebih tinggi (osPriorityAboveNormal).
     - Tugas hijau memiliki prioritas normal (osPriorityNormal).

# Gambar Hardware
![Screenshot 2024-11-20 201931](https://github.com/user-attachments/assets/98b0b153-0c16-40eb-9e1e-29ae9a9cf0a3)

# Video Hardware

https://github.com/user-attachments/assets/5d822546-0c28-4c5b-abb1-affe976bbabc

