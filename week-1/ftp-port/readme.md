### Kenapa FTP bisa menggunakan UDP atau TCP?
FTP (File Transfer Protocol) pada dasarnya menggunakan TCP (Transmission Control Protocol) untuk transfer datanya. Namun, FTP juga teoretis dapat menggunakan UDP (User Datagram Protocol), tetapi hal ini jarang terjadi dan bukan praktik umum.

Alasan mengapa FTP bisa menggunakan UDP atau TCP adalah karena desain protokol FTP. Protokol FTP (File Transfer Protocol) dirancang sedemikian rupa sehingga memungkinkannya untuk menggunakan baik UDP (User Datagram Protocol) maupun TCP (Transmission Control Protocol) untuk transfer data. Hal ini memungkinkan fleksibilitas dalam penggunaan protokol tergantung pada kebutuhan dan kondisi jaringan.

* TCP untuk Koneksi Kontrol

FTP menggunakan TCP untuk koneksi kontrolnya. Koneksi kontrol dibentuk pada port 21, dan digunakan untuk mengatur perintah dan respons antara klien dan server. TCP dipilih untuk tujuan ini karena memberikan komunikasi yang andal dan berorientasi pada koneksi, dengan fitur seperti deteksi kesalahan, pengendalian aliran, dan pengiriman paket yang terjamin.

* TCP untuk Koneksi Data

FTP juga menggunakan TCP untuk koneksi datanya saat menggunakan "mode aktif" bawaan. Dalam mode aktif, server memulai koneksi ke klien untuk mentransfer data. Hal ini memastikan bahwa konfigurasi firewall klien jarang mengganggu pembentukan koneksi data. Karena transfer data membutuhkan kehandalan, TCP adalah pilihan yang paling tepat.

* UDP untuk Koneksi Data (Mode Pasif)

Meskipun jarang terjadi, FTP dalam teori bisa menggunakan UDP untuk koneksi datanya saat beroperasi dalam mode pasif. Dalam mode pasif, klien memulai koneksi kontrol dan data. Mode pasif sering digunakan untuk mengatasi masalah dengan konfigurasi firewall dan NAT. Dalam mode ini, server memberikan alamat IP dan port agar klien dapat terhubung untuk transfer data. Beberapa implementasi mungkin menggunakan UDP untuk transfer data dalam mode pasif, tetapi hal ini kurang umum karena kurangnya mekanisme kehandalan bawaan pada UDP. Menggunakan UDP di sini bisa menyebabkan potensi kehilangan data atau kesalahan urutan.

Kunci desain yang memungkinkan FTP untuk menggunakan baik UDP maupun TCP adalah fleksibilitas yang diizinkan oleh spesifikasi protokol FTP itu sendiri. FTP tidak secara ketat mengikat penggunaan satu jenis protokol transportasi tertentu. Sebagai gantinya, spesifikasi FTP menyediakan kerangka kerja yang memungkinkan implementasi untuk memilih jenis koneksi yang sesuai dengan kebutuhan.

Dalam praktiknya, menggunakan UDP untuk transfer data FTP bukanlah pendekatan yang direkomendasikan karena sifat yang tidak andal dibandingkan dengan TCP. Integritas dan kehandalan data penting dalam transfer file, dan TCP menawarkan jaminan yang lebih baik untuk aspek-aspek tersebut. Meskipun FTP memiliki ketentuan untuk mendukung baik TCP maupun UDP, sebagian besar implementasi FTP dan kasus penggunaannya mengandalkan hanya TCP untuk memastikan transfer file yang stabil dan aman.