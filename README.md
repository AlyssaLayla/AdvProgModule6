# AdvProgModule6
Advance Programming Module 6 2025

Nama    : Alyssa Layla Sasti </br>
NPM     : 2306152052 </br>
Kelas   : AdvProg B</br>

1. Commit 1 Reflection Notes
Berdasarkan hasil pencarian dan pembelajaran yang saya dapat, fungsi `handle_connection` ditujukan untuk menangani setiap koneksi yang masuk melalui `TcpStream`. Fungsi ini menggunnakan `BufReader` untuk membaca data yang dikirim, yang mana khususnya berupa request HTTP. Kemudian pada kode yang tertera juga terdapat metode `.lines()` yang membuat data dari stream dibaca per baris, lalu diproses menggunakan `.map(|result| result.unwrap())` untuk mengambil nilai yang berhasil dibaca. Selanjutnya `.take_while(|line| !line.is_empty())` digunakan untuk memberhentikan proses reading saat ada baris kosong, sebagai tanda akhir dari header permintaan HTTP. Kemudian, semua hasilnya dikumpulkan dalam `Vect<String>` dan ditampilkan di terminal. Menurut saya, proses ini dilakukan untuk memungkinkan server guna menangano request dengan lebih terstruktur. 

![Commit 2 screen capture](/assets/images/commit2.jpg)
2. Commit 2 Reflection Notes
Dalam pembaruan kode ini, saya memahami bahwa fungsi `handle_connection` kini tidak hanya membaca request dari klien tetapi juga meresponsnya dengan mengirimkan file HTML sederhana. Fungsi ini pertama-tama membaca request menggunakan `BufReader`, lalu diproses perbaris dengan `.lines()` dan `.take_while(|line| !line.is_empty())` untuk menangkap header HTTP. Setelah itu, server menyiapkan respons dengan `HTTP/1.1 200 OK`, membaca konten dari file `hello.html` dengan `fs::read_to_string()`, dan menghitung panjangnya untuk disertakan dalam header Content-Length. Akhirnya, respons dikirim ke klien menggunakan `stream.write_all(response.as_bytes()).unwrap();`. Dari implementasi ini, saya belajar bagaimana server HTTP sederhana bekerja dalam merespons request dengan file statis, pentingnya Content-Length dalam komunikasi HTTP, serta bagaimana Rust menangani file dan jaringan secara efisien.