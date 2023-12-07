## Dosen Pengampu
Tugas ini merupakan tugas mata kuliah Konsep Jaringan yang diampu oleh Dr. Ferry Astika Saputra ST, M.Sc ([@ferryastika](https://github.com/ferryastika)).

### Pendahuluan
Di sini kita akan menganalisa http.cap, telnet-cooked.cap, dan dns.cap yang kita dapatkan dari https://wiki.wireshark.org/SampleCaptures menggunakan Wireshark.

### HTTP
<br>
<p align="center">
<img src="../../assets/week-1/analysis-wireshark/http_packet_counter.png" alt="Wireshark Packet Counter">
<br>
<i>Wireshark Packet Counter</i>
</p>
<br>

Kita bisa melihat statistik dari file http.cap dengan mengklik Statistics -> HTTP -> Packet Counter di toolbar. Berikut adalah informasi yang ada di dalam Packet Counter:
* Total Packets: Jumlah total paket HTTP yang ditangkap.
* Requests: Jumlah total request HTTP yang ditangkap.
* Responses: Jumlah total response HTTP yang ditangkap.
* Errors: Jumlah packet error HTTP yang ditangkap.
* Most Common Request Methods: Metode Request HTTP yang paling digunakan.
* Most Common Response Codes: Response Code yang paling banyak dikembalikan.

Dari data statistik http.cap, kita bisa melihat bahwa ada 4 HTTP Packet, yaitu 2 Response Packet (Success 200 OK semua) dan 2 Request Packet (Metode GET semua).

Lalu kita juga bisa klik kanan salah satu datanya dan pilih Follow -> HTTP Stream untuk mengikuti dan menganalisis aliran data HTTP antara klien (biasanya web browser) dan server web dalam sesi HTTP tertentu. Fitur ini berguna untuk memahami bagaimana dua host saling berinteraksi dan untuk mengidentifikasi masalah dalam percakapan.
<br>
<p align="center">
<img src="../../assets/week-1/analysis-wireshark/follow_http_stream.png" alt="Follow HTTP Stream">
<br>
<i>Follow HTTP Stream</i>
</p>
<br>

Text yang berwarna merah adalah request yang dikirim oleh client. Sedangkan yang berwarna biru adalah response yang dikembalikan oleh server.

Dari situ kita bisa melihat bahwa client mengirimkan request GET dengan endpoint /download.html menggunakan HTTP 1.1. Host dari endpoint tersebut adalah www.ethereal.com. Lalu response yang dikembalikan oleh server adalah 200 OK, menandakan request sukses. Lalu body dari responsenya adalah kode HTML.

<br>
<p align="center">
<img src="../../assets/week-1/analysis-wireshark/http_info.png" alt="HTTP Info">
<br>
<i>HTTP Info</i>
</p>
<br>

Selain itu, kita juga bisa melihat informasi dari HTTP request tersebut di kiri bawah lalu expand Hypertext Transfer Protocol.

### Telnet Cooked
<br>
<p align="center">
<img src="../../assets/week-1/analysis-wireshark/telnet_detail.png" alt="Follow TCP Stream Telnet">
<br>
<i>Follow TCP Stream Telnet </i>
</p>
<br>
Ada beberapa hal yang bisa kita amati di telnet-cooked.pcap:

* Username dan password yang digunakan untuk masuk ke server Telnet.
* Perintah yang dikeluarkan ke server Telnet.
* Tanggapan dari server Telnet.
* Kesalahan apa pun yang terjadi selama sesi Telnet.

### DNS
<br>
<p align="center">
<img src="../../assets/week-1/analysis-wireshark/dns_detail.png" alt="Follow TCP Stream Telnet">
<br>
<i>Follow UDP Stream DNS </i>
</p>
<br>
Ada beberapa hal yang bisa kita amati di dns.cap:

* Domain yang di-query.
* Tipe query yang di-request.
* IP Address yang dikembalikan oleh respons.
* Kesalahan apa pun yang terjadi selama sesi query DNS.
