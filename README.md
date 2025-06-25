# Project-Data-Analysis-for-B2B-Retail-Customer-Analytics-Report
![image](https://github.com/user-attachments/assets/20793271-f65d-4e64-a35d-3891a0703f7a)

Proyek ini disusun sebagai bagian dari pengembangan portofolio saya sebagai Data Analyst, dengan tujuan menampilkan kemampuan analisis data bisnis, terutama dalam konteks B2B Customer Analytics menggunakan SQL.

## Latar Belakang
xyz.com adalah perusahan rintisan B2B yang menjual berbagai produk tidak langsung kepada end user tetapi ke bisnis/perusahaan lainnya. Sebagai data-driven company, maka setiap pengambilan keputusan di xyz.com selalu berdasarkan data. Setiap quarter xyz.com akan mengadakan townhall dimana seluruh atau perwakilan divisi akan berkumpul untuk me-review performance perusahaan selama quarter terakhir.

## Dataset
Tabel yang akan digunakan pada project kali ini adalah sebagai berikut.

1. Tabel orders_1 : Berisi data terkait transaksi penjualan periode quarter 1 (Jan – Mar 2004)
+-------------+------------+--------------+-------------+---------+------------+-------------+----------+-----------+
| orderNumber | orderDate  | requiredDate | shippedDate | status  | customerID | productCode | quantity | priceeach |
+-------------+------------+--------------+-------------+---------+------------+-------------+----------+-----------+
|       10234 | 2004-03-30 | 2004-04-05   | 2004-04-02  | Shipped |        412 | S72_1253    |       40 |     45690 |
|       10234 | 2004-03-30 | 2004-04-05   | 2004-04-02  | Shipped |        412 | S700_2047   |       29 |     83280 |
|       10234 | 2004-03-30 | 2004-04-05   | 2004-04-02  | Shipped |        412 | S24_3816    |       31 |     78830 |
|       10234 | 2004-03-30 | 2004-04-05   | 2004-04-02  | Shipped |        412 | S24_3420    |       25 |     65090 |
|       10234 | 2004-03-30 | 2004-04-05   | 2004-04-02  | Shipped |        412 | S24_2841    |       44 |     67140 |
+-------------+------------+--------------+-------------+---------+------------+-------------+----------+-----------+ 
3. Tabel Orders_2 : Berisi data terkait transaksi penjualan periode quarter 2 (Apr – Jun 2004)
+-------------+------------+--------------+-------------+---------+------------+-------------+----------+-----------+
| orderNumber | orderDate  | requiredDate | shippedDate | status  | customerID | productCode | quantity | priceeach |
+-------------+------------+--------------+-------------+---------+------------+-------------+----------+-----------+
|       10235 | 2004-04-02 | 2004-04-12   | 2004-04-06  | Shipped |        260 | S18_2581    |       24 |     81950 |
|       10235 | 2004-04-02 | 2004-04-12   | 2004-04-06  | Shipped |        260 | S24_1785    |       23 |     89720 |
|       10235 | 2004-04-02 | 2004-04-12   | 2004-04-06  | Shipped |        260 | S24_3949    |       33 |     55270 |
|       10235 | 2004-04-02 | 2004-04-12   | 2004-04-06  | Shipped |        260 | S24_4278    |       40 |     63030 |
|       10235 | 2004-04-02 | 2004-04-12   | 2004-04-06  | Shipped |        260 | S32_1374    |       41 |     90900 |
+-------------+------------+--------------+-------------+---------+------------+-------------+----------+-----------+ 
5. Tabel Customer : Berisi data profil customer yang mendaftar menjadi customer xyz.com
+------------+----------------------------+-----------------+------------------+-----------+-----------+------------+
| customerID | customerName               | contactLastName | contactFirstName | city      | country   | createDate |
+------------+----------------------------+-----------------+------------------+-----------+-----------+------------+
|        103 | Atelier graphique          | Schmitt         | Carine           | Nantes    | France    | 2004-02-05 |
|        112 | Signal Gift Stores         | King            | Jean             | Las Vegas | USA       | 2004-02-05 |
|        114 | Australian Collectors, Co. | Ferguson        | Peter            | Melbourne | Australia | 2004-02-20 |
|        119 | La Rochelle Gifts          | Labrune         | Janine           | Nantes    | France    | 2004-02-05 |
|        121 | Baane Mini Imports         | Bergulfsen      | Jonas            | Stavern   | Norway    | 2004-02-05 |
+------------+----------------------------+-----------------+------------------+-----------+-----------+------------+ 
6. Diagram skema database yang menjelaskan hubungan antar tiga tabel utama:
![image](https://github.com/user-attachments/assets/9566994b-8149-4155-a3ae-d33c7ef2cffb)








