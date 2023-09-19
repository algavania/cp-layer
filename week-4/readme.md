## Daftar Isi

- [Daftar Isi](#daftar-isi)
- [Connection Termination](#connection-termination)
- [Letak Half-Closed pada Kode](#letak-half-closed-pada-kode)



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

* Server Side (Kode Server): Saat server menerima pesan "close" dari client, server akan menangani permintaan tersebut dengan menutup soket yang terkait dengan koneksi client tersebut menggunakan close(). Ini berarti server tidak akan mengirim data lebih lanjut kepada client. Namun, server masih dapat menerima pesan dari client jika client memutuskan untuk mengirim pesan lebih lanjut sebelum server menutup koneksi secara aktif.

Dengan demikian, server menghentikan pengiriman data kepada client setelah menerima pesan "close" dari client, tetapi server masih dapat menerima data dari client hingga koneksi benar-benar ditutup oleh server. Hal ini sesuai dengan definisi half-closed, di mana salah satu sisi koneksi telah menghentikan pengiriman data tetapi masih dapat menerima data.
