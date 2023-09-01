# Analisis di Wireshark
## Daftar Isi

- [Analisis di Wireshark](#analisis-di-wireshark)
  - [Daftar Isi](#daftar-isi)
  - [Gambar Connection Termination Tanpa Data](#gambar-connection-termination-tanpa-data)
  - [Analisis Flow Graph dari Request HTTP](#analisis-flow-graph-dari-request-http)
  - [Penjelasan Packet Counter](#penjelasan-packet-counter)
    - [Field di Packet Counter](#field-di-packet-counter)

## Gambar Connection Termination Tanpa Data
<br>
<p align="center">
<img src="../assets/week-2/connection_termination_no_data.png" alt="Connection Termination Tanpa Data">
<br>
<i>Connection Termination Tanpa Data</i>
</p>
<br>

## Analisis Flow Graph dari Request HTTP
<br>
<p align="center">
<img src="../assets/week-2/flowgraph_tcp.png" alt="Flow Graph TCP">
<br>
<i>Flow Graph</i>
</p>
<br>
Buka Flow Graph dengan menekan Statistics -> Flow Graph di toolbar. Lalu pilih Flow type menjadi TCP Flows. Di sini, kita bisa melihat step yang dijalankan.
<br>
<p align="center">
<img src="../assets/week-2/threeway_handshake.png" alt="Three-way Handshake">
<br>
<i>Three-way Handshake</i>
</p>
<br>
Terlihat bahwa pada proses ini terjadi Three-way Handshake untuk Connection Establishment.
<br>
<p align="center">
<img src="../assets/week-2/seq_ack_info.png" alt="Sequence Acknowledgment Info">
<br>
<i>Seq Ack Information</i>
</p>
<br>
Lalu di sisi kanan juga terlihat informasi mengenai data Seq dan Ack.

## Penjelasan Packet Counter
<br>
<p align="center">
<img src="../assets/week-1/analysis-wireshark/http_packet_counter.png" alt="Wireshark Packet Counter">
<br>
<i> Packet Counter</i>
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

### Field di Packet Counter
* Count

Field ini menunjukkan jumlah paket yang termasuk dalam rentang yang dipilih.
* Average

Field ini menunjukkan rata-rata panjang paket dalam rentang yang dipilih.
* Min val

Field ini menunjukkan panjang minimum dari paket apa pun dalam rentang yang dipilih.
* Max val

Field ini menunjukkan panjang maksimum dari paket apa pun dalam rentang yang dipilih.
* Rate (ms)

Field ini menunjukkan rata-rata paket per milidetik untuk paket dalam rentang yang dipilih.
* Percent

Field ini menunjukkan persentase paket dalam rentang yang dipilih, berdasarkan jumlah.
* Burst rate

Field ini menunjukkan jumlah maksimum paket dalam satu burst. Burst adalah serangkaian paket yang diterima dalam periode waktu singkat.
* Burst start

Field ini menunjukkan waktu saat paket pertama dalam burst diterima.
