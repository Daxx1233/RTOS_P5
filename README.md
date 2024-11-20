# Praktikum RTOS - SEMESTER 5 (3 Teknik Komputer A)
- Triyas Rahmadiyanti (3222600001)
- Duta Fithra Qolby (3222600003)
# Exercise 5 – Demonstrate access contention problems
when using shared resources in a multitasking system.- 
## Deskripsi Projek
Sistem sederhana berbasis real-time operating system (RTOS) yang menggunakan mikrokontroler STM32 untuk 
mengontrol beberapa LED (merah, hijau, kuning) dengan tugas-tugas (threads) terpisah. 
Sistem ini memanfaatkan FreeRTOS untuk mengatur manajemen tugas (task management) dengan prioritas yang berbeda-beda.

## Deskripsi Alur Kerja
1. Inisialisasi Sistem:
   - Fungsi HAL_Init() menginisialisasi sistem HAL (Hardware Abstraction Layer) untuk mengontrol perangkat keras.
   - Konfigurasi clock dilakukan di SystemClock_Config(), di mana sumber clock diatur menggunakan HSI (High-Speed Internal).
   - GPIO diinisialisasi melalui MX_GPIO_Init() untuk mengatur pin-pin LED sebagai keluaran (output).
2. Pengaturan RTOS:
   - Kernel RTOS diinisialisasi dengan osKernelInitialize().
   - Tiga tugas utama dibuat:
       - defaultTask: Tugas default dengan prioritas normal, meskipun tidak memiliki logika aktif dalam kode.
       - greenLEDTask: Tugas untuk mengontrol LED hijau.
       - RedLEDTask: Tugas untuk mengontrol LED merah.
3. Tugas Utama:
   a. Tugas Hijau (greenLEDTask):
      - Menyalakan dan mematikan LED hijau (GPIO_PIN_2) secara berkala setiap 500 ms.
      - Mengakses fungsi accessData() untuk operasi tambahan.
   b. Tugas Merah (RedLEDTask):
      - Menyalakan dan mematikan LED merah (GPIO_PIN_0) lebih cepat, dengan jeda 100 ms.
      - Juga memanggil accessData() untuk sinkronisasi data.
   c. Fungsi accessData() menulis ke GPIO_PIN_1 dengan logika tertentu menggunakan variabel flag.
4. Scheduler RTOS:
   - RTOS mengambil alih pengendalian eksekusi tugas-tugas setelah osKernelStart() dipanggil.
   - Scheduler memastikan tugas dengan prioritas lebih tinggi (seperti RedLEDTask) dijalankan lebih sering.
5. Pengendalian Waktu:
   - Fungsi osDelay() dan HAL_Delay() digunakan untuk mengatur jeda antar operasi.
   - Callback HAL_TIM_PeriodElapsedCallback() memperbarui waktu global menggunakan HAL_IncTick().
6. Error Handling: Fungsi Error_Handler() menangani kondisi error dengan menghentikan sistem.

## Deskripsi Alur Eksekusi
1. Saat sistem dinyalakan, semua inisialisasi perangkat keras dan clock dilakukan.
2. Scheduler RTOS mulai bekerja, mengatur eksekusi tugas sesuai prioritasnya:
   - RedLEDTask (prioritas lebih tinggi) akan menyalakan/mematikan LED merah lebih sering.
   - greenLEDTask (prioritas normal) akan berjalan lebih jarang.
3. Tugas-tugas tersebut saling berbagi akses ke fungsi accessData(), yang memungkinkan sinkronisasi akses ke pin GPIO lain.
4. Tugas default tetap idle tanpa fungsionalitas yang spesifik.

# Gambar Hardware
![Screenshot 2024-11-20 203131](https://github.com/user-attachments/assets/eb7b6251-8eec-4da5-b1a3-adc8dfca2206)

# Video Hardware

https://github.com/user-attachments/assets/1f737580-8acd-4859-ae02-5d6fd197427d





