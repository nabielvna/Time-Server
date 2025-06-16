# Multithreaded Time Server

Sebuah server waktu sederhana berbasis TCP yang dibangun menggunakan Python. Server ini dirancang untuk menangani beberapa koneksi klien secara bersamaan (concurrent) dengan menggunakan pendekatan multithreading. Proyek ini merupakan implementasi dasar dari materi Pemrograman Jaringan.

---

## 🚀 Fitur Utama

- **Multithreaded**: Mampu melayani banyak client secara simultan tanpa saling memblokir.
- **Berbasis TCP**: Menggunakan protokol TCP untuk komunikasi yang andal dan terurut.
- **Protokol Sederhana**: Mengimplementasikan protokol aplikasi berbasis teks untuk meminta waktu dan mengakhiri sesi.
- **Logging**: Memberikan log _real-time_ di terminal untuk setiap koneksi dan permintaan yang masuk.
- **Reliable**: Menggunakan `SO_REUSEADDR` untuk memastikan server dapat di-restart dengan cepat selama pengembangan.

---

## ⚙️ Spesifikasi Teknis

- **Bahasa**: Python 3
- **Port**: 45000 (TCP)
- **Library Standar**: `socket`, `threading`, `datetime`, `logging`, `sys`

---

## 🏁 Cara Menjalankan Server

1.  **Clone Repositori (Opsional)**
    Jika Anda belum memiliki filenya, clone repositori ini terlebih dahulu.
    ```bash
    git clone [https://github.com/](https://github.com/)[Username-Anda]/[Nama-Repo-Anda].git
    cd [Nama-Repo-Anda]
    ```

2.  **Jalankan Server**
    Buka terminal dan jalankan file `server.py` menggunakan Python 3.
    ```bash
    python3 server.py
    ```

3.  **Server Aktif**
    Jika berhasil, Anda akan melihat pesan berikut di terminal, menandakan server siap menerima koneksi.
    ```
    2025-06-16 21:30:15,123 - Time server berjalan dan mendengarkan di port 45000...
    ```

---

## 🧪 Cara Menguji Server

Anda dapat menggunakan utilitas `netcat` atau `telnet` untuk terhubung ke server sebagai klien.

1.  **Buka Terminal Baru**
    Biarkan terminal server tetap berjalan. Buka jendela terminal baru.

2.  **Hubungkan ke Server**
    Gunakan `netcat` untuk terhubung ke `localhost` pada port `45000`.
    ```bash
    netcat localhost 45000
    ```
    Atau menggunakan `telnet`:
    ```bash
    telnet localhost 45000
    ```

3.  **Interaksi dengan Server**
    Setelah terhubung, Anda bisa mengirimkan perintah sesuai protokol yang ditentukan.

    - Untuk meminta waktu, ketik `TIME` lalu tekan **Enter**.
    - Untuk keluar, ketik `QUIT` lalu tekan **Enter**.

---

## 📜 Spesifikasi Protokol

Komunikasi antara client dan server mengikuti aturan sederhana berbasis teks.

| Perintah | Aksi | Respons Server |
| :------- | :--- | :--------------- |
| `TIME`   | Meminta waktu saat ini. | `JAM hh:mm:ss\r\n` |
| `QUIT`   | Meminta untuk menutup koneksi. | (Tidak ada, koneksi ditutup) |

**Catatan**: Setiap perintah dari client harus diakhiri dengan menekan tombol **Enter**, yang akan mengirimkan karakter akhir baris (`\r\n`).

---

## ✨ Contoh Sesi

Berikut adalah contoh interaksi antara client (`netcat`) dan log yang dihasilkan oleh server.

![image](https://github.com/user-attachments/assets/41fe9780-ea4b-44f1-9be7-61f247f59281)

**Tampilan Client (Terminal 2):**
```bash
# netcat localhost 45000
TIME
JAM 21:35:10
QUIT
#
```

**Tampilan Server (Terminal 1):**
```
2025-06-16 21:35:05,111 - Time server berjalan dan mendengarkan di port 45000...
2025-06-16 21:35:08,222 - Menerima koneksi baru dari ('127.0.0.1', 54321)
2025-06-16 21:35:10,333 - Menerima request 'TIME' dari ('127.0.0.1', 54321)
2025-06-16 21:35:10,333 - Mengirim waktu '21:35:10' ke ('127.0.0.1', 54321)
2025-06-16 21:35:12,444 - Menerima request 'QUIT' dari ('127.0.0.1', 54321)
2025-06-16 21:35:12,444 - Klien ('127.0.0.1', 54321) meminta untuk keluar.
2025-06-16 21:35:12,445 - Koneksi dengan ('127.0.0.1', 54321) telah ditutup.
```

---
