# AdvProgModule6
Advance Programming Module 6 2025

Nama    : Alyssa Layla Sasti </br>
NPM     : 2306152052 </br>
Kelas   : AdvProg B</br>

1. Commit 1 Reflection Notes</br>
Berdasarkan hasil pencarian dan pembelajaran yang saya dapat, fungsi `handle_connection` ditujukan untuk menangani setiap koneksi yang masuk melalui `TcpStream`. Fungsi ini menggunnakan `BufReader` untuk membaca data yang dikirim, yang mana khususnya berupa request HTTP. Kemudian pada kode yang tertera juga terdapat metode `.lines()` yang membuat data dari stream dibaca per baris, lalu diproses menggunakan `.map(|result| result.unwrap())` untuk mengambil nilai yang berhasil dibaca. Selanjutnya `.take_while(|line| !line.is_empty())` digunakan untuk memberhentikan proses reading saat ada baris kosong, sebagai tanda akhir dari header permintaan HTTP. Kemudian, semua hasilnya dikumpulkan dalam `Vect<String>` dan ditampilkan di terminal. Menurut saya, proses ini dilakukan untuk memungkinkan server guna menangani request dengan lebih terstruktur. 
---

![Commit 2 screen capture](/assets/images/commit2.jpg)

2. Commit 2 Reflection Notes</br>
Dalam pembaruan kode ini, saya memahami bahwa fungsi `handle_connection` kini tidak hanya membaca request dari klien tetapi juga meresponsnya dengan mengirimkan file HTML sederhana. Fungsi ini pertama-tama membaca request menggunakan `BufReader`, lalu diproses perbaris dengan `.lines()` dan `.take_while(|line| !line.is_empty())` untuk menangkap header HTTP. Setelah itu, server menyiapkan respons dengan `HTTP/1.1 200 OK`, membaca konten dari file `hello.html` dengan `fs::read_to_string()`, dan menghitung panjangnya untuk disertakan dalam header Content-Length. Akhirnya, respons dikirim ke klien menggunakan `stream.write_all(response.as_bytes()).unwrap();`. Dari implementasi ini, saya belajar bagaimana server HTTP sederhana bekerja dalam merespons request dengan file statis, pentingnya Content-Length dalam komunikasi HTTP, serta bagaimana Rust menangani file dan jaringan secara efisien.
---

![Commit 3 screen capture](/assets/images/commit3.jpg)

3. Commit 3 Reflection Notes</br>
Refactoring pada commit 3 ini saya perlukan untuk meningkatkan modularitas dan keterbacaan kode dengan memisahkan logika pemrosesan request dan respons ke dalam fungsi yang lebih terstruktur. Dengan membedakan antara permintaan halaman yang valid dan tidak valid, server dapat memberikan respons yang sesuai, seperti menampilkan `hello.html` untuk request yang benar dan `404.html` untuk request yang tidak dikenali. Refactoring ini juga membantu dalam menangani error secara lebih aman, menghindari panic akibat pemrosesan request yang tidak valid. Selain itu, pemisahan ini membuat kode lebih mudah diperluas dan dipelihara di masa depan, terutama jika ingin menambahkan fitur baru atau meningkatkan performa server.
---

![Commit 4 screen capture](/assets/images/commit4.jpg)

4. Commit 4 Reflection Notes</br>
Pada commit ini menunjukkan bahwa server yang berjalan pada satu thread memiliki keterbatasan dalam menangani beberapa permintaan secara bersamaan. Ketika satu permintaan membutuhkan waktu lama untuk diproses, seperti saat mengakses `/sleep` yang menyebabkan server tertunda selama 10 detik, semua permintaan lain juga akan terhambat. Hal ini terjadi karena server hanya dapat memproses satu permintaan dalam satu waktu, sehingga jika ada banyak pengguna yang mengakses secara bersamaan, respons menjadi lambat dan tidak efisien. Oleh karena itu, solusi yang lebih optimal adalah menggunakan multi-threading atau asynchronous processing agar server dapat menangani banyak permintaan tanpa harus menunggu satu per satu selesai terlebih dahulu.
---

![Commit 5 screen capture](/assets/images/commit5.jpg)

5. Commit 5 Reflection Notes</br>
Untuk memahami bagaimana ThreadPool bekerja, saya mengimplementasikan multithreading dalam server sederhana yang sebelumnya hanya berjalan dalam satu thread. Saya membuat struktur `ThreadPool` yang terdiri dari beberapa worker threads yang dapat mengeksekusi tugas secara paralel. Dalam proses ini, saya menggunakan message passing melalui channel untuk mendistribusikan tugas dari main thread ke worker threads, dengan mekanisme sinkronisasi menggunakan `Mutex` dan `Arc` agar workers dapat mengakses antrian tugas secara aman. Saat server menerima permintaan, tugas tersebut dikirim ke salah satu worker yang sedang tidak sibuk. Implementasi ini memungkinkan server menangani banyak permintaan sekaligus, mengatasi masalah blocking yang terjadi pada model single-threaded. Dalam proses pengerjaan, saya juga menghadapi error terkait tipe data yang tidak sesuai saat mendeklarasikan `JoinHandle`, yang berhasil saya selesaikan dengan membungkusnya dalam `Some()`. Dengan perubahan ini, server sekarang lebih responsif dan dapat melayani banyak klien secara bersamaan.
---

![Commit Bonus screen capture](/assets/images/commitbonus.jpg)

6. Commit Bonus Reflection Notes</br>
Dalam bonus ini, saya memodifikasi implementasi ThreadPool dengan mengganti metode new menjadi build untuk meningkatkan keamanan dan fleksibilitas dalam pembuatan pool thread. Saya menambahkan validasi agar ukuran ThreadPool tidak boleh nol, sehingga dapat mencegah error saat program berjalan. Jika ukuran yang diberikan tidak valid, metode build akan mengembalikan Err yang kemudian ditangani dengan unwrap_or_else di main.rs, memungkinkan program untuk keluar dengan pesan kesalahan yang jelas. Perubahan ini memastikan bahwa server tidak akan berjalan dengan konfigurasi yang tidak valid, sekaligus meningkatkan ketahanan sistem dalam menangani skenario yang tidak diinginkan.