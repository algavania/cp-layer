# Analisis di Wireshark
## Daftar Isi

- [Analisis di Wireshark](#analisis-di-wireshark)
  - [Daftar Isi](#daftar-isi)
  - [Gambar Connection Termination Tanpa Data](#gambar-connection-termination-tanpa-data)
  - [Analisis Flow Graph dari Request HTTP](#analisis-flow-graph-dari-request-http)

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