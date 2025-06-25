# Project-Data-Analysis-for-B2B-Retail-Customer-Analytics-Report
![image](https://github.com/user-attachments/assets/20793271-f65d-4e64-a35d-3891a0703f7a)

## 📌 Project Overview
Proyek ini bertujuan untuk menganalisis performa bisnis xyz.com, sebuah perusahaan rintisan B2B yang menjual produk ke sesama perusahaan. Sebagai perusahaan yang mengutamakan pengambilan keputusan berbasis data, xyz.com secara rutin mengadakan townhall untuk meninjau pencapaian tiap kuartal. Analisis ini difokuskan pada data penjualan dan pelanggan selama kuartal pertama dan kedua tahun 2004.

Melalui proyek ini, saya berupaya menjawab pertanyaan strategis berikut:

1. Bagaimana tren pertumbuhan penjualan antar kuartal?
2. Apakah jumlah pelanggan menunjukkan peningkatan?
3. Berapa banyak pelanggan yang telah melakukan transaksi?
4. Kategori produk apa saja yang paling diminati?
5. Seberapa besar tingkat retensi atau loyalitas pelanggan antarkuartal?

Proyek ini dikembangkan menggunakan bahasa SQL untuk menggali insight yang mendalam, dengan pendekatan analitis yang sistematis dan dapat direplikasi.

## 🛠️ Analysis Process
Langkah-langkah analisis yang dilakukan dalam proyek ini meliputi:

1. Data Extraction Menggunakan klausa SELECT ... FROM ... untuk mengambil data dari tabel customer, orders_1, dan orders_2.
2. Filtering Data Menerapkan klausa WHERE dan operator logika untuk menyaring data relevan, misalnya hanya transaksi pada tahun 2004.
3. Data Aggregation Menggunakan GROUP BY bersama fungsi agregat (SUM, COUNT, AVG) untuk menghitung total penjualan, jumlah pesanan, dan pelanggan aktif.
4. Sorting Data Menerapkan ORDER BY untuk mengurutkan hasil analisis berdasarkan prioritas, seperti pelanggan dengan jumlah pembelian terbanyak.
5. Combining Datasets Menggunakan UNION untuk menggabungkan data transaksi dari Q1 (orders_1) dan Q2 (orders_2) agar analisis dapat dilakukan secara menyeluruh.
6. Data Manipulation Menerapkan fungsi DATE, MONTH, serta fungsi string seperti CONCAT, LEFT, dan UPPER untuk keperluan normalisasi dan perbandingan.
7. Subquery & Temporary Calculations Memanfaatkan subquery untuk menyimpan hasil kalkulasi sementara, seperti total revenue per customer atau daftar pelanggan aktif lintas kuartal.

## 📂 Raw Dataset Link
Data yang akan digunakan pada project kali ini adalah sebagai berikut.

1. Tabel orders_1 : Berisi data terkait transaksi penjualan periode quarter 1 (Jan – Mar 2004)
   
![image](https://github.com/user-attachments/assets/969f472e-cb49-40be-b699-fde2f17d5925)

2. Tabel Orders_2 : Berisi data terkait transaksi penjualan periode quarter 2 (Apr – Jun 2004)

![image](https://github.com/user-attachments/assets/3eb8e86c-3388-4c71-8d2e-697cb0a1d373)

3. Tabel Customer : Berisi data profil customer yang mendaftar menjadi customer xyz.com
   
![image](https://github.com/user-attachments/assets/03ace26c-4bce-461c-b570-415f155652a7)

4. Diagram skema database yang menjelaskan hubungan antar tiga tabel utama:
![image](https://github.com/user-attachments/assets/9566994b-8149-4155-a3ae-d33c7ef2cffb)

## 📈 Insight & Findings

Dari hasil analisis data pelanggan dan transaksi penjualan xyz.com selama kuartal 1 (Jan–Mar 2004) dan kuartal 2 (Apr–Jun 2004), diperoleh beberapa temuan penting berikut:

1. Total Penjualan dan Revenue pada Quarter-1 (Jan, Feb, Mar) dan Quarter-2 (Apr,Mei,Jun)

- Total Penjualan dan Revenue pada Quarter-1

SELECT 
	SUM(quantity) AS total_penjualan,
	SUM(quantity * priceEach) AS revenue
FROM orders_1
WHERE status = 'Shipped';

![image](https://github.com/user-attachments/assets/2c4c8318-2cd4-4bf8-8d08-4dec0f5321f5)


- Total Penjualan dan Revenue pada Quarter-2

SELECT
	
 
 	SUM(quantity) AS total_penjualan,
	SUM(quantity * priceEach) AS revenue
FROM orders_2
WHERE status = 'Shipped';

![image](https://github.com/user-attachments/assets/4e73367d-dcdc-40d2-8754-b0f12858652e)

Pertumbuhan Penjualan & Revenue (Q1 ke Q2)
Pada kuartal kedua tahun 2004, xyz.com mencatat penurunan total penjualan sebanyak 1.977 unit dibanding kuartal pertama. Dari sisi revenue, terjadi penurunan sebesar Rp192.030.990. Penurunan ini cukup signifikan dan dapat menjadi indikator awal adanya tantangan dalam performa bisnis, seperti penurunan permintaan, perubahan strategi, atau faktor eksternal lain yang memengaruhi perilaku pelanggan.

