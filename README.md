# AdvProgModule6
Advance Programming Module 6 2025

Nama    : Alyssa Layla Sasti </br>
NPM     : 2306152052 </br>
Kelas   : AdvProg B</br>

1. Commit 1 Reflection Notes
Berdasarkan hasil pencarian dan pembelajaran yang saya dapat, fungsi `handle_connection` ditujukan untuk menangani setiap koneksi yang masuk melalui `TcpStream`. Fungsi ini menggunnakan `BufReader` untuk membaca data yang dikirim, yang mana khususnya berupa request HTTP. Kemudian pada kode yang tertera juga terdapat metode `.lines()` yang membuat data dari stream dibaca per baris, lalu diproses menggunakan `.map(|result| result.unwrap())` untuk mengambil nilai yang berhasil dibaca. Selanjutnya `.take_while(|line| !line.is_empty())` digunakan untuk memberhentikan proses reading saat ada baris kosong, sebagai tanda akhir dari header permintaan HTTP. Kemudian, semua hasilnya dikumpulkan dalam `Vect<String>` dan ditampilkan di terminal. Menurut saya, proses ini dilakukan untuk memungkinkan server guna menangano request dengan lebih terstruktur. 