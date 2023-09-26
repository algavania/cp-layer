## Daftar Isi

- [Daftar Isi](#daftar-isi)
- [Connection Termination](#connection-termination)
- [Letak Half-Closed pada Kode](#letak-half-closed-pada-kode)
- [Telnet, SSH, dan DNS](#telnet-ssh-dan-dns)
  - [Telnet](#telnet)
    - [Penjelasan](#penjelasan)
    - [RFC](#rfc)
    - [Karateristik](#karateristik)
  - [SSH](#ssh)
    - [Penjelasan](#penjelasan-1)
    - [RFC](#rfc-1)
    - [Karateristik](#karateristik-1)
  - [DNS](#dns)
    - [Penjelasan](#penjelasan-2)
    - [Karateristik](#karateristik-2)



## Connection Termination
Proses terminasi koneksi pada kode sebelumnya dapat diklasifikasikan sebagai half-closed. Hal ini disebabkan oleh perilaku di kedua sisi, yaitu client dan server, yang memungkinkan satu sisi untuk menghentikan pengiriman data sementara yang lainnya dapat tetap menerima data.

Dalam terminologi jaringan, istilah "half-closed" (setengah tertutup) mengacu pada situasi di mana salah satu sisi koneksi telah menghentikan pengiriman data, tetapi sisi lainnya masih dapat menerima data. Dalam konteks kode yang diberikan:

Jika client mengirim pesan "close" ke server, maka client telah menghentikan pengiriman data, tetapi masih dapat menerima respons dari server.
Sebaliknya, jika server mengirim pesan "close" ke client, maka server telah menghentikan pengiriman data kepada client, tetapi masih dapat menerima pesan dari client.
Koneksi ini tidak sepenuhnya ditutup hingga kedua sisi mengonfirmasi bahwa mereka telah menyelesaikan semua operasi mereka yang tertunda dan telah mengirimkan pesan "close" ke sisi lainnya. Dengan kata lain, terminasi koneksi dalam kode ini hanya setengah tertutup karena satu sisi menghentikan pengiriman data tetapi masih dapat menerima, sementara sisi lainnya masih dapat mengirim dan menerima data hingga menerima pesan "close" dari sisi yang telah menghentikan pengiriman data.

## Letak Half-Closed pada Kode
Dalam kode yang diberikan, yang menandakan situasi half-closed adalah ketika server menerima pesan "close" dari client. Saat server menerima pesan "close" dari client, itu menunjukkan bahwa client telah menghentikan pengiriman data kepada server, tetapi server masih dapat mengirim pesan ke client.

Ini dapat dijelaskan lebih rinci:

* Client Side (Kode Client): Saat client mengirim pesan "close" ke server, itu hanya menandakan bahwa client ingin mengakhiri koneksi. Client tidak akan mengirim data lebih lanjut setelah ini. Ini merupakan bagian dari proses terminasi.

* Server Side (Kode Server): Saat server menerima pesan "close" dari client, server akan menangani permintaan tersebut dengan menutup soket yang terkait dengan koneksi client tersebut menggunakan close(). Ini berarti server tidak akan mengirim data lebih lanjut kepada client. Namun, server asih dapat menerima pesan dari client jika client memutuskan untuk mengirim pesan lebih lanjut sebelum server menutup koneksi secara aktif.

Dengan demikian, server menghentikan pengiriman data kepada client setelah menerima pesan "close" dari client, tetapi server masih dapat menerima data dari client hingga koneksi benar-benar ditutup oleh server. Hal ini sesuai dengan definisi half-closed, di mana salah satu sisi koneksi telah menghentikan pengiriman data tetapi masih dapat menerima data.

## Telnet, SSH, dan DNS
### Telnet
#### Penjelasan
Telnet adalah protokol yang digunakan untuk menghubungkan dan mengakses perangkat jarak jauh atau server melalui jaringan. Ini memungkinkan pengguna untuk mengendalikan perangkat jarak jauh dan menjalankan perintah pada perangkat tersebut.

#### RFC
Telnet didokumentasikan dalam RFC 854. Meskipun RFC 854 adalah standar awal, banyak RFC lain yang mengembangkan Telnet lebih lanjut, seperti RFC 855, RFC 856, dan lainnya.

#### Karateristik
* Protokol Akses Jarak Jauh: Telnet adalah protokol yang digunakan untuk mengakses dan mengendalikan perangkat jarak jauh melalui jaringan. Ini digunakan untuk menghubungkan ke perangkat seperti server, router, atau switch melalui terminal jarak jauh.
* Berbasis teks: Telnet mengirim data dalam bentuk teks, yang berarti bahwa semua yang dikirim melalui koneksi Telnet adalah teks, termasuk perintah dan respons.
* Tidak Aman: Salah satu kelemahan utama Telnet adalah bahwa data yang dikirim tidak dienkripsi. Ini berarti bahwa informasi sensitif, seperti kata sandi, dapat dengan mudah dicuri oleh pihak yang tidak berwenang jika mereka dapat memantau lalu lintas jaringan.
* Port Standar: Telnet biasanya menggunakan port 23 pada protokol TCP.

### SSH
#### Penjelasan
SSH adalah protokol yang digunakan untuk mengakses perangkat jarak jauh atau server dengan aman melalui jaringan. Ini adalah versi yang lebih aman daripada Telnet dan dirancang untuk melindungi informasi sensitif dan privasi pengguna.

#### RFC
SSH didokumentasikan dalam berbagai RFC, yang paling terkenal adalah RFC 4251, RFC 4252, RFC 4253, dan RFC 4254.

#### Karateristik
* Protokol Keamanan: SSH dirancang untuk menyediakan akses jarak jauh yang aman ke perangkat dan server melalui enkripsi data. Ini menjadikannya lebih aman daripada Telnet.
* Enkripsi: SSH mengenkripsi semua data yang dikirim antara klien dan server, termasuk perintah, respons, dan data sensitif seperti kata sandi.
Autentikasi yang Kuat: SSH mendukung berbagai metode autentikasi, termasuk kata sandi, kunci publik, dan sertifikat, sehingga memungkinkan tingkat keamanan yang tinggi.
* Port Standar: SSH biasanya menggunakan port 22 pada protokol TCP.
* Kemampuan Port Forwarding: SSH memungkinkan pengguna untuk melakukan port forwarding, yang berguna untuk mengakses layanan di belakang firewall atau NAT.
* Sesi Interaktif dan Non-Interaktif: SSH dapat digunakan untuk sesi interaktif, seperti mengelola server jarak jauh, atau sesi non-interaktif untuk mentransfer file atau menjalankan perintah tunggal.

### DNS
#### Penjelasan
DNS adalah sistem yang digunakan untuk mengaitkan nama domain (contohnya, www.example.com) dengan alamat IP yang sesuai. Ini memungkinkan kita untuk menggunakan nama yang mudah diingat daripada harus mengingat alamat IP numerik yang rumit.

#### Karateristik
* Resolusi Nama: DNS digunakan untuk mengonversi nama domain menjadi alamat IP. Ini dilakukan oleh server DNS yang memiliki catatan mengenai nama domain dan alamat IP yang sesuai.
* Hierarki Domain: DNS memiliki struktur hierarki yang terdiri dari zona-zona domain, subdomain, dan nama domain tingkat atas (TLD) seperti .com, .org, .net, dan lainnya.
* Caching: Server DNS dan perangkat antara dapat menyimpan hasil resolusi DNS dalam cache untuk mengurangi latensi dan beban jaringan.
* Dinamis dan Statis: DNS dapat diatur secara statis dengan catatan manual atau secara dinamis melalui protokol seperti Dynamic Host Configuration Protocol (DHCP).
* Port Standar: DNS menggunakan port 53 pada protokol UDP (dan juga TCP dalam situasi tertentu).
Distributed and Redundant: DNS dirancang untuk menjadi sistem terdistribusi dan redundant, dengan banyak server DNS tersebar di seluruh dunia untuk memastikan ketersediaan dan keandalan.
* Hierarki Authoritative: Server DNS authoritative bertanggung jawab atas zona tertentu dan memiliki wewenang untuk memberikan informasi resolusi DNS untuk zona tersebut.
