# Data-Engineer-Challenge-with-SQL
## Project SQL dari DQLab Academy
<hr>

### <b>Produk DQLab Mart</b>
<img src="https://cdn.dqlab.id/assets/images/mysqltest/tables.png">
Mengacu pada table ms_produk, tampilkan daftar produk yang memiliki harga antara 50.000 and 150.000.
Nama kolom yang harus ditampilkan: no_urut, kode_produk, nama_produk, dan harga.
Semua table di atas sudah tersedia, Anda tinggal menulis query Anda dalam Code Editor.

Berikut Codenya:
```
select* from ms_produk where harga > 50000 and harga < 150000
```

### <b>Thumb drive di DQLab Mart</b>
<img src="https://cdn.dqlab.id/assets/images/mysqltest/tables.png">
Tampilkan semua produk yang mengandung kata Flashdisk.
Nama kolom yang harus ditampilkan: no_urut, kode_produk, nama_produk, dan harga.
Semua table di atas sudah tersedia, Anda tinggal menulis query Anda dalam Code Editor.

Berikut Codenya:
```
SELECT* FROM ms_produk WHERE nama_produk LIKE '%Flashdisk%'
```

### <b>Pelanggan Bergelar</b>
<img src="https://cdn.dqlab.id/assets/images/mysqltest/tables.png">
Tampilkan hanya nama-nama pelanggan yang hanya memiliki gelar-gelar berikut: S.H, Ir. dan Drs.
Nama kolom yang harus ditampilkan: no_urut, kode_pelanggan, nama_pelanggan, dan alamat.
Semua table di atas sudah tersedia, Anda tinggal menulis query Anda dalam Code Editor.

Berikut Codenya:
```
SELECT* 
FROM ms_pelanggan 
WHERE nama_pelanggan LIKE '%S.H%' or nama_pelanggan LIKE '%Ir.%' or nama_pelanggan LIKE '%Drs.%'
```

### <b>Mengurutkan Nama Pelanggan</b>
<img src="https://cdn.dqlab.id/assets/images/mysqltest/tables.png">
Tampilkan nama-nama pelanggan dan urutkan hasilnya berdasarkan kolom nama_pelanggan dari yang terkecil ke yang terbesar (A ke Z).
Nama kolom yang harus ditampilkan: nama_pelanggan.
Semua table di atas sudah tersedia, Anda tinggal menulis query Anda dalam Code Editor.

Berikut Codenya:
```SELECT nama_pelanggan FROM ms_pelanggan ORDER BY nama_pelanggan```

### <b>Mengurutkan Nama Pelanggan Tanpa Gelar</b>
<img src="https://cdn.dqlab.id/assets/images/mysqltest/tables.png">
Tampilkan nama-nama pelanggan dan urutkan hasilnya berdasarkan kolom nama_pelanggan dari yang terkecil ke yang terbesar (A ke Z), namun gelar tidak boleh menjadi bagian dari urutan. Contoh: Ir. Agus Nugraha harus berada di atas Heidi Goh.
Nama kolom yang harus ditampilkan: nama_pelanggan.
Semua table di atas sudah tersedia, Anda tinggal menulis query Anda dalam Code Editor.

Berikut Codenya:
```
SELECT nama_pelanggan
FROM ms_pelanggan
ORDER BY REPLACE(nama_pelanggan,'Ir. ','') ASC
```

### <b>Nama Pelanggan yang Paling Panjang</b>
<img src="https://cdn.dqlab.id/assets/images/mysqltest/tables.png">
Tampilkan nama pelanggan yang memiliki nama paling panjang. Jika ada lebih dari 1 orang yang memiliki panjang nama yang sama, tampilkan semuanya.
Nama kolom yang harus ditampilkan: nama_pelanggan.
Semua table di atas sudah tersedia, Anda tinggal menulis query Anda dalam Code Editor.
 
Berikut Codenya:
```
SELECT nama_pelanggan
FROM ms_pelanggan
WHERE length(nama_pelanggan) IN(
  SELECT max(length(nama_pelanggan))
  FROM ms_pelanggan)
```
 
 ### <b>Nama Pelanggan yang Paling Panjang dengan Gelar</b>
<img src="https://cdn.dqlab.id/assets/images/mysqltest/tables.png">
Tampilkan nama orang yang memiliki nama paling panjang (pada row atas), dan nama orang paling pendek (pada row setelahnya). Gelar menjadi bagian dari nama. Jika ada lebih dari satu nama yang paling panjang atau paling pendek, harus ditampilkan semuanya.
Nama kolom yang harus ditampilkan: nama_pelanggan.
Semua table di atas sudah tersedia, Anda tinggal menulis query Anda dalam Code Editor.

Berikut Codenya:
```
SELECT nama_pelanggan
FROM ms_pelanggan
WHERE length(nama_pelanggan) IN(
  SELECT max(length(nama_pelanggan))
  FROM ms_pelanggan
)
UNION
SELECT nama_pelanggan
FROM ms_pelanggan
WHERE length(nama_pelanggan) IN(
  SELECT min(length(nama_pelanggan))
  FROM ms_pelanggan
)
```

### <b>Kuantitas Produk yang Banyak Terjual</b>
<img src="https://cdn.dqlab.id/assets/images/mysqltest/tables.png">
Tampilkan produk yang paling banyak terjual dari segi kuantitas. Jika ada lebih dari 1 produk dengan nilai yang sama, tampilkan semua produk tersebut.
Nama kolom yang harus ditampilkan: kode_produk, nama_produk,total_qty.
Semua table di atas sudah tersedia, Anda tinggal menulis query Anda dalam Code Editor.

Berikut Codenya:
```
SELECT
  ms_produk.kode_produk,
  ms_produk.nama_produk,
  sum(tr_penjualan_detail.qty) as total_qty
FROM
  ms_produk
JOIN
  tr_penjualan_detail
ON ms_produk.kode_produk = tr_penjualan_detail.kode_produk
GROUP BY
  ms_produk.kode_produk,
  ms_produk.nama_produk
ORDER BY sum(tr_penjualan_detail.qty) desc limit 2
```

### <b>Pelanggan Paling Tinggi Nilai Belanjanya</b>
<img src="https://cdn.dqlab.id/assets/images/mysqltest/tables.png">
Siapa saja pelanggan yang paling banyak menghabiskan uangnya untuk belanja? Jika ada lebih dari 1 pelanggan dengan nilai yang sama, tampilkan semua pelanggan tersebut.
Nama kolom yang harus ditampilkan: kode_pelanggan, nama_pelanggan, total_harga.
Semua table di atas sudah tersedia, Anda tinggal menulis query Anda dalam Code Editor.
Berikut Codenya:

```
SELECT d.kode_pelanggan, d.nama_pelanggan, sum(b.qty*b.harga_satuan) as total_harga
FROM tr_penjualan a JOIN tr_penjualan_detail b
ON a.kode_transaksi = b.kode_transaksi
JOIN ms_pelanggan d
ON a.kode_pelanggan = d.kode_pelanggan
GROUP BY d.kode_pelanggan, d.nama_pelanggan
ORDER BY total_harga desc limit 1
```

### <b>Pelanggan yang Belum Pernah Berbelanja</b>
<img src="https://cdn.dqlab.id/assets/images/mysqltest/tables.png">
Tampilkan daftar pelanggan yang belum pernah melakukan transaksi.
Nama kolom yang harus ditampilkan: kode_pelanggan, nama_pelanggan, alamat.
Semua table di atas sudah tersedia, Anda tinggal menulis query Anda dalam Code Editor.
Berikut Codenya:

```
SELECT a.kode_pelanggan, a.nama_pelanggan, a.alamat
FROM ms_pelanggan a 
WHERE a.kode_pelanggan not in(
  SELECT kode_pelanggan
  FROM tr_penjualan
)
```

### <b>Transaksi Belanja dengan Daftar Belanja lebih dari 1</b>
<img src="https://cdn.dqlab.id/assets/images/mysqltest/tables.png">
Tampilkan transaksi-transaksi yang memiliki jumlah item produk lebih dari 1 jenis produk. Dengan lain kalimat, tampilkan transaksi-transaksi yang memiliki jumlah baris data pada table tr_penjualan_detail lebih dari satu.
Nama kolom yang harus ditampilkan:  kode_transaksi, kode_pelanggan, nama_pelanggan, tanggal_transaksi, jumlah_detail
Semua table di atas sudah tersedia, Anda tinggal menulis query Anda dalam Code Editor.

Berikut Codenya:

```
SELECT a.kode_transaksi, c.kode_pelanggan, c.nama_pelanggan, b.tanggal_transaksi, count(a.kode_produk) as jumlah_detail
FROM tr_penjualan_detail a 
JOIN tr_penjualan b
ON a.kode_transaksi = b.kode_transaksi
JOIN ms_pelanggan c
ON b.kode_pelanggan = c.kode_pelanggan
GROUP BY a.kode_transaksi, c.kode_pelanggan, c.nama_pelanggan, b.tanggal_transaksi
HAVING count(a.kode_produk) > 1
```
