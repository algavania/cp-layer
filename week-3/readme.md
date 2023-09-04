# TCP Flow di HTTP
## Daftar Isi

- [TCP Flow di HTTP](#tcp-flow-di-http)
  - [Daftar Isi](#daftar-isi)
  - [Perbandingan](#perbandingan)
  - [TCP Flow pada HTTP 0.9, 1.0, dan 1.1](#tcp-flow-pada-http-09-10-dan-11)
    - [HTTP 0.9](#http-09)
    - [HTTP 1.0](#http-10)
    - [HTTP 1.1](#http-11)
      - [Koneksi persisten](#koneksi-persisten)
      - [Chunked transfer encoding](#chunked-transfer-encoding)
      - [Request pipelining](#request-pipelining)
      - [Range-based resource request](#range-based-resource-request)
      - [Caching](#caching)
      - [SPDY](#spdy)
  - [HTTP 2.0](#http-20)
    - [Binary framing layer](#binary-framing-layer)
    - [Stream](#stream)
    - [Frame](#frame)
    - [Message](#message)
    - [Multiplexing](#multiplexing)
    - [Header compression](#header-compression)
    - [Prioritization](#prioritization)
    - [Flow Control](#flow-control)
    - [Server push](#server-push)



## Perbandingan
<br>
<p align="center">
<img src="../assets/week-3/tcp-comparison-in-http.png" alt="Perbandingan Tiap Versi HTTP">
<br>
<i>Perbandingan Tiap Versi HTTP</i>
</p>
<br>

## TCP Flow pada HTTP 0.9, 1.0, dan 1.1
<br>
<p align="center">
<img src="../assets/week-3/tcp-flow-1.png" alt="TCP Flow pada HTTP 0.9, 1.0, dan 1.1">
<br>
<i>TCP Flow pada HTTP 0.9, 1.0, dan 1.1</i>
</p>
<br>

### HTTP 0.9
HTTP/0.9 adalah versi pertama dari protokol HTTP yang mengadopsi model request-response di mana klien memulai koneksi melalui jabat tangan TCP dan mengirimkan data untuk direspon oleh server.

Berikut adalah beberapa fitur penting dari HTTP/0.9:

* Setiap request dari klien melibatkan pembuatan koneksi baru dengan 3-way TCP handshake dengan server. Antarmukanya terutama berdasarkan telnet.
Request klien adalah satu baris yang terdiri dari karakter ASCII yang dibatasi oleh carriage return, dan hanya request GET yang didukung dengan format GET http://{host}:{port}.
* Respon hanya terdiri dari dokumen HTML. Koneksi ditutup segera setelah setiap respons.
* Header request dan respons tidak didukung. Ini berarti bahwa tidak mungkin untuk membedakan antara respons yang berhasil dan respons yang gagal.

### HTTP 1.0
HTTP/1.0 adalah perkembangan dari HTTP/0.9. HTTP/1.0 juga beroperasi dengan model request-response seperti HTTP/0.9.

Berikut adalah beberapa fitur penting dari HTTP/1.0:

* Setiap request dari klien melibatkan pembuatan koneksi baru dengan 3-way TCP handshake dengan server. Antarmukanya berkembang dari yang berbasis telnet menjadi berbasis browser.
* Penggunaan header dalam request dan respons dengan dukungan untuk versi HTTP dan kode status; Dukungan untuk metode HTTP POST, GET, dan HEAD.
* Dukungan untuk Content-Type yang kaya dalam header respons yang memungkinkan respons non-HTML untuk dikembalikan. Koneksi masih ditutup setelah setiap respons, seperti pada HTTP/0.9.
* HTTP/0.9 dan HTTP/1.0 memerlukan 3-way TCP handshake untuk setiap request karena koneksi ditutup setelah respons. Hal ini memperkenalkan latensi yang signifikan pada setiap request.

### HTTP 1.1
HTTP/1.1 merupakan kemajuan terpenting dalam protokol HTTP yang memperkenalkan beberapa optimasi dan fitur penting.

HTTP/1.1 memperkenalkan dukungan untuk metode POST, GET, PUT, DELETE, TRACE, OPTIONS.

#### Koneksi persisten
Salah satu perbaikan inti dalam HTTP/1.1 adalah pengenalan koneksi persisten atau koneksi keep-alive.

Versi-versi sebelumnya dari HTTP memerlukan 3-way handshake untuk setiap request HTTP. Total waktu eksekusi setiap request HTTP adalah jumlah dari waktu eksekusi TCP handshake dan pemrosesan request sebenarnya.

Dengan diperkenalkannya koneksi keep-alive, TCP handshake hanya dilakukan sekali, dan koneksi yang sama digunakan kembali untuk beberapa request HTTP. Total waktu eksekusi yang diselamatkan untuk N request adalah (N-1) * RTT (Round Trip Time).

#### Chunked transfer encoding
Chunked transfer encoding adalah fitur penting lainnya dari HTTP/1.1. Dalam chunked transfer encoding, request dan respons dibagi menjadi potongan-potongan kecil yang tidak tumpang tindih, dan setiap potongan dapat dikirim dan diterima secara independen oleh klien dan server.

Setiap potongan termasuk header ukuran yang menunjukkan ukuran, dan transmisi berhenti ketika potongan terakhir memiliki panjang nol. Chunked transfer encoding berguna ketika ukuran request atau respons tidak diketahui sebelumnya. Contohnya: pengunggahan dan pengunduhan file.

Tanpa fitur ini, klien atau server harus mem-buffer dan menunggu semua konten sebelum transmisi, yang meningkatkan penggunaan memori klien/server dan latensi transmisi.

#### Request pipelining
Dengan koneksi persisten, sebuah aplikasi dapat menjalankan beberapa request HTTP melalui satu koneksi tetapi secara berurutan. request pertama dikirimkan ke server, dan request berikutnya hanya dikirimkan setelah server mengembalikan respons.

Request pipelining adalah fitur yang diperkenalkan dalam HTTP/1.1 yang memungkinkan klien untuk mengirimkan beberapa request ke server sebelum mendapatkan respons mereka yang sesuai. Karena server tidak aktif selama pengiriman request dan respons, server dapat memproses request tambahan. Selain itu, server dapat menggunakan beberapa utas untuk memproses request secara paralel.

Namun, HTTP/1.1 tidak mengizinkan beberapa objek respons multipel di multiplexing pada koneksi yang sama. Ini memaksa setiap respons untuk dikembalikan secara berurutan sebelum respons berikutnya dapat ditransfer.

Respons yang terakhir harus dibuffer hingga yang sebelumnya dikembalikan ke klien. Fenomena ini disebut sebagai Head-of-Line blocking (HOL).

Dukungan untuk request pipelining kemudian dihapus dari HTTP/1.1 karena kurangnya dukungan untuk multiplexing.

#### Range-based resource request
HTTP/1.1 memperkenalkan range-based request for resources di mana klien meminta server untuk mengirim hanya sebagian dari pesan HTTP kembali. Ini sangat berguna untuk klien seperti pemutar media yang memerlukan akses acak.

Jika respons HTTP mencakup Accept-Header dan nilainya adalah apa pun selain none, maka itu mendukung akses berbasis rentang ke resource.

* Single part range: Menentukan bagian mana dari resource yang diperlukan dari server dengan mengirimkan header Range dalam format bytes:0-50.
* Multi-part range: Memungkinkan beberapa rentang resource diakses dalam satu request dengan mengirimkan header Range dalam format bytes:0-50,60-100.

#### Caching
HTTP 1.1 memperkenalkan dukungan penyimpanan cache melalui beberapa direktif penyimpanan cache.

Cache-Control adalah header HTTP yang menentukan kebijakan penyimpanan cache pada request klien dan respons server. Header ini dibagi menjadi beberapa direktif.

* Max Age: Direktif yang menentukan waktu kedaluwarsa salinan cache, setelahnya kita harus menyegarkan data.
* No-Cache: Cache harus memvalidasi ulang request dari server asli sebelum menyimpan respons.
* No-Store: Browser tidak diizinkan untuk menyimpan respons.
* Public: Menunjukkan bahwa respons dapat disimpan oleh cache mana pun.
* Private: Tidak boleh disimpan oleh cache bersama karena ditujukan untuk data khusus pengguna.

Expires adalah header cache lain yang menentukan tanggal/waktu tetap untuk kedaluwarsa resource yang di-cache.

Etag adalah header cache lainnya, tetapi dari sisi respons, yang menunjukkan pengenal yang diberikan oleh server untuk versi tertentu dari resource. Jika resource berubah, Etag baru diberikan. Jika versi tetap tidak berubah, browser menggunakan versi yang di-cache secara lokal.

#### SPDY
SPDY (dibaca speedy) adalah protokol eksperimental yang dikembangkan oleh Google pada tahun 2009 yang tujuan utamanya adalah mengurangi waktu pemuatan halaman web dan mengatasi keterbatasan HTTP/1.1.

SPDY memperkenalkan binary framing layer baru untuk mengaktifkan multiplexing dan prioritas request dan respons. SPDY berperan sebagai katalisator dan membuka jalan bagi standar HTTP 2.0.

## HTTP 2.0
HTTP/2 adalah rilis yang signifikan dalam protokol HTTP setelah HTTP/1.1, terinspirasi oleh protokol SPDY.

### Binary framing layer
HTTP/2 tidak mengubah semantik dari HTTP/1.1. Semua kontrak dan semantik pada metode HTTP, kode status, header, dll., tetap sama seperti HTTP/1.1. Namun, HTTP/2 memperkenalkan lapisan biner baru yang mengatur bagaimana pesan dikapsulasi dan ditransportasikan antara klien dan server.

Pengenalan binary framing layer baru ini tidak kompatibel ke belakang, yang berarti baik klien maupun server harus ditingkatkan ke HTTP/2 untuk memanfaatkan fitur-fiturnya.

Berikut adalah komponen-komponen binary framing layer:

### Stream

Sebuah stream adalah saluran virtual dalam koneksi TCP yang memungkinkan bi-directional flow antara klien dan server. Setiap stream memiliki pengidentifikasi unik yang mengidentifikasinya untuk mengurutkannya di sisi lain.

### Frame

Frame adalah unit komunikasi terkecil dalam HTTP/2. Setiap frame mencakup jenis, pengidentifikasi stream, dan payload opsional. Setiap jenis frame membawa informasi yang berbeda dan memiliki fungsionalitas yang berbeda.

Berikut adalah jenis-jenis frame yang berbeda:

* DATA: Frame yang membawa data aktual.
* HEADERS: Frame yang membawa header yang berisi metadata.
* PRIORITY: Frame yang membawa informasi prioritas resource.
* SETTINGS: Frame yang mengonfigurasi cara dua endpoint harus berkomunikasi.
* RST_STREAM: Frame yang menandakan terminasi abnormal dari stream.
* PING: Frame yang digunakan untuk mengukur RTT dan berfungsi sebagai health check.
* GOAWAY: Frame yang memberi tahu peer untuk menghentikan pembuatan stream untuk koneksi saat ini.
* WINDOW_UPDATE: Frame yang mengimplementasikan flow control per stream dan koneksi.
* PUSH_PROMISE: Frame yang digunakan untuk memberi tahu peer sebelumnya tentang stream yang sender ingin inisiasi.

### Message

Sebuah message sesuai dengan request dan respons HTTP yang logis. Setiap message terdiri dari satu atau lebih frame.

### Multiplexing
HTTP/1.1 mengatasi keterbatasan HTTP/1.0 dengan memperkenalkan koneksi persisten. Tetapi request masih diurutkan dalam koneksi yang sama yang menyebabkan Head-of-Line blocking.
<br>
<p align="center">
<img src="../assets/week-3/http_2_multiplexing.png" alt="HTTP 2 Multiplexing">
<br>
<i>HTTP 2 Multiplexing</i>
</p>
<br>

HTTP/2 mengaktifkan multiplexing request dan respons penuh dalam satu koneksi TCP tunggal.

* Untuk setiap request HTTP, logical pipeline stream dibuat dalam koneksi TCP tunggal yang sama. Setiap stream memungkinkan bi-directional flow antara klien dan server.
* Setelah stream dibuat, request dan respons dibagi menjadi potongan-potongan kecil yang disebut frame dan ditransportasikan antara klien dan server dalam stream.

Oleh karena itu, stream memungkinkan beberapa request dan respons digabungkan dalam satu koneksi TCP tunggal, meningkatkan throughput dan mengurangi TCP handshake.

### Header compression
HTTP/1.1 mengirimkan header antara klien dan server dalam format teks biasa. Ini juga mengirimkan banyak header yang sering digunakan dalam setiap request, yang menyebabkan overhead beberapa kilobyte pada setiap request.

HTTP/2 mengatasi masalah ini dengan menggunakan algoritma kompresi header, HPACK.

HPACK menggunakan dictionary data structure baik di sisi klien maupun server untuk menghindari pengiriman header yang redundan dan mengompresi header yang dikirimkan melalui wire. Setiap entri dalam kamus memiliki indeks, header key, dan header value. Setiap dictionary mencakup dua komponen:
<br>
<p align="center">
<img src="../assets/week-3/hpack.png" alt="HPACK">
<br>
<i>HPACK</i>
</p>
<br>

* Static Table: Sebuah set dictionary yang telah ditentukan sebelumnya terdiri dari 61 header statis beserta nilai-nilai yang telah ditentukan sebelumnya disimpan.
* Dynamic Table: List tambahan dari custom key-value header field yang dapat disimpan dan sebelumnya ditemui dalam koneksi TCP yang sama dalam dynamic dictionary.

The index in the table is computed using either a Huffman encoding or ASCII encoding for every header key-value pair.

Indeks di dalam tabel dihitung menggunakan Huffman encoding atau ASCII encoding untuk tiap-tiap pasangan header key-valuenya.

Ketika HPACK perlu mengompres pasangan key-value, dia akan mencari di static dan dynamic table.

* Jika key dan value cocok dengan entri di dictionary, pasangan key-valuenya akan di-replace dengan indeks yang ada di dalam frame.
* Jika hanya keynya saja yang cocok dengan entri di dictionary, keynya akan di-replace dengan indeks, dan valuenya akan tetap sebagai plain text di dalam frame.
* Jika tidak, pasangan key-value tersebut tetap diteruskan apa adanya dalam frame dalam format plain text.

Seiring berjalannya waktu, klien dan server akan belajar mengenai header yang akan masuk dan meng-update dynamic table sesuai dengan datanya. Request dan response berikutnya akan memanfaatkan indeks yang telah dienkripsi apabila pasangan key-value header yang sama dilewatkan.

Dengan cara ini, dengan menggantikan key-value dengan indeks yang lightweight encoded, HPACK mengurangi overhead dari field header dalam request dan respons HTTP.

### Prioritization
HTTP/2 introduced the concept of stream priorities, allowing clients to hint at the relative importance of a particular stream. The server can use these priorities to prioritize processing the corresponding frames from that stream. These priority values act as a hint to the server, and the server can decide to ignore the priority and process the frames in the order it thinks is most appropriate.

HTTP/2 memperkenalkan konsep dari prioritas stream, memungkinkan klien untuk memberi petunjuk terhadap relative importance dari stream tertentu. Server juga bisa menggunakan prioritas tersebut untuk memprioritaskan pemrosesan frame-frame yang sesuai dari stream tersebut. Nilai-nilai prioritas ini bertindak sebagai petunjuk bagi server, dan server dapat memutuskan untuk mengabaikan prioritas tersebut dan memproses frame sesuai dengan urutan yang menurutnya paling sesuai.

Ada dua mekanisme untuk mengimplementasikan prioritization:
* Dependecy: Satu stream dapat bergantung pada stream lain sehingga yang pertama dapat mengirimkan frame hanya jika yang terakhir tidak perlu menggunakan koneksi.
* Weight: Setiap stream dapat memiliki bobot relatif yang digunakan untuk menyelesaikan prioritas dari dua stream yang memiliki stream induk yang sama.

### Flow Control
Memultiplex request dan respons stream secara bersamaan melalui satu koneksi TCP tunggal menyebabkan bandwith yang terbagi-bagi dan akan ada contention/persaingan.

Flow control adalah teknik untuk mengatur transmisi data antara sender dan receiver untuk mencegah sender yang lebih cepat overwhelming sender yang lebih lambat.

HTTP/2 memperkenalkan flow control pada stream level dan connection level. Ketika koneksi HTTP/2 dibuat, klien dan server bertukar frame SETTINGS untuk mengatur pengaturan flow baik pada stream level maupun connection level untuk mengatur traffic.

### Server push
Server push adalah fitur paling menarik dari HTTP/2, yang memungkinkan server untuk push konten ke klien sebelum klien memintanya.

Server tidak dapat memulai push request secara sewenang-wenang. Sebaliknya, server mengikuti siklus request-response dan mengirimkan push resource hanya sebagai respons terhadap suatu request.

Server mengirimkan frame PUSH_PROMISE yang menunjukkan intensi server untuk push resource ke klien, yang hanya berisi header HTTP. Klien dapat memutuskan untuk menolak push stream sepenuhnya. Setelah klien menerima frame PUSH_PROMISE, server push resource ke klien dalam frame DATA.

Karena baik klien maupun server dapat membuat stream, stream yang diinisiasi oleh klien memiliki ID stream yang berangka genap, dan stream yang diinisiasi oleh server memiliki ID stream yang berangka ganjil.