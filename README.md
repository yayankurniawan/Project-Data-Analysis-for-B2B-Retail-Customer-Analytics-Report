# Project-Data-Analysis-for-B2B-Retail-Customer-Analytics-Report
![image](https://github.com/user-attachments/assets/20793271-f65d-4e64-a35d-3891a0703f7a)

## ✨ Indentitas 
- Nama		: Yayan Kurniawan
- Linkedin	: linkedin.com/in/yayan-kurniawan
- Judul Project	: Project Data Analysis for B2B Retail Customer Analytics Report
  
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

1. Bagaimana tren pertumbuhan penjualan antar kuartal?

Dari hasil analisis data pelanggan dan transaksi penjualan xyz.com selama kuartal 1 (Jan–Mar 2004) dan kuartal 2 (Apr–Jun 2004), diperoleh beberapa temuan penting berikut:

**Total Penjualan dan Revenue pada Quarter-1 (Jan, Feb, Mar) dan Quarter-2 (Apr,Mei,Jun)**

- Total Penjualan dan Revenue pada Quarter-1
<pre lang="markdown">
SELECT 
	SUM(quantity) AS total_penjualan,
	SUM(quantity * priceEach) AS revenue
FROM orders_1
WHERE status = 'Shipped';
</pre>

![image](https://github.com/user-attachments/assets/2c4c8318-2cd4-4bf8-8d08-4dec0f5321f5)


- Total Penjualan dan Revenue pada Quarter-2
<pre lang="markdown">
SELECT
 	SUM(quantity) AS total_penjualan,
	SUM(quantity * priceEach) AS revenue
FROM orders_2
WHERE status = 'Shipped';
</pre>

![image](https://github.com/user-attachments/assets/4e73367d-dcdc-40d2-8754-b0f12858652e)

**Menghitung persentasi keseluruhan penjualan**
<pre lang="markdown">
SELECT
	quarter,
	SUM(quantity) AS total_penjualan,
	SUM(quantity * priceEach) AS revenue
FROM 
(SELECT 1 AS quarter, orderNumber, status, quantity, priceEach FROM orders_1 
 UNION
SELECT 2 AS quarter, orderNumber, status, quantity, priceEach FROM orders_2)
AS table_1 WHERE status = 'Shipped'
GROUP BY quarter;
</pre>
![image](https://github.com/user-attachments/assets/0c359027-1041-44a4-b065-af3470b10e37)

**Perhitungan Growth Penjualan dan Revenue**

- %Growth Penjualan = (6717 – 8694)/8694 = -22%
- %Growth Revenue = (607548320 – 799579310)/ 799579310 = -24%

**Insight: tren pertumbuhan penjualan antar kuartal**

Penjualan dan pendapatan xyz.com mengalami penurunan signifikan di kuartal kedua tahun 2004, yaitu sekitar 22% untuk jumlah unit terjual dan 24% dari sisi revenue. Hal ini bisa menjadi sinyal awal bahwa diperlukan evaluasi terhadap strategi penjualan, promosi, atau kepuasan pelanggan.

2. Apakah jumlah pelanggan menunjukkan peningkatan?
<pre lang="markdown">
SELECT
	QUARTER(createDate) AS quarter,
	COUNT(DISTINCT(customerID)) AS total_customers
FROM
(SELECT
	customerID,
	createDate,
	QUARTER(createDate) AS quarter
FROM customer 
WHERE createDate BETWEEN '2004-01-01' AND '2004-06-30') AS table_b
GROUP BY QUARTER(createDate);
</pre>

 ![image](https://github.com/user-attachments/assets/712a7750-67c1-4e42-bb4c-7be6edb25e78)

**Insight: Perubahan Jumlah Pelanggan**

Alih-alih meningkat, jumlah pelanggan yang tercatat pada kuartal kedua justru mengalami penurunan sebanyak 8 pelanggan dibandingkan kuartal pertama.
Penurunan dari 43 menjadi 35 ini menunjukkan bahwa selama Q2 tidak hanya tidak ada pertumbuhan jumlah pelanggan, tetapi juga kemungkinan terjadi penurunan akuisisi pelanggan baru atau adanya pelanggan yang tidak melanjutkan keterlibatannya.

3.  Berapa banyak pelanggan yang telah melakukan transaksi?
<pre lang="markdown">
SELECT
	quarter,
	COUNT(DISTINCT(customerID)) AS total_customers
FROM
(SELECT
	customerID,
	createDate,
	QUARTER(createDate) AS quarter
FROM customer
WHERE createDate BETWEEN '2004-01-01' AND '2004-06-30') AS tabel_b
WHERE customerID IN(
SELECT
	DISTINCT(customerID)
FROM orders_1 
UNION
SELECT 
	DISTINCT(customerID)
FROM orders_2) 
GROUP BY quarter;
</pre>
![image](https://github.com/user-attachments/assets/a8a3c3c4-470e-455c-a2ea-5f110769768a)

**Insight: Jumlah Pelanggan yang Melakukan Transaksi**

Selama periode Januari hingga Juni 2004, jumlah pelanggan xyz.com yang sudah melakukan transaksi tercatat sebanyak:

- 25 pelanggan pada kuartal pertama
- 19 pelanggan pada kuartal kedua

Ini menunjukkan adanya penurunan aktivitas pelanggan yang cukup mencolok di Q2. Meski sudah mendaftar, tidak semua pelanggan melanjutkan hingga tahap transaksi—dan tren tersebut sedikit menurun dari Q1 ke Q2. 

4. Kategori produk apa saja yang paling diminati?
<pre lang="markdown">
SELECT *
FROM
	(SELECT
		categoryID,
		COUNT(DISTINCT(orderNumber)) AS total_order,
		SUM(quantity) AS total_penjualan
	FROM
		(SELECT
			productCode, 
			orderNumber,
			quantity,
			status,
			LEFT(productCode,3) AS categoryID
		FROM orders_2
		WHERE status = 'Shipped') AS tabel_c
	GROUP BY categoryID) AS A
ORDER BY total_order DESC;
</pre>
![image](https://github.com/user-attachments/assets/ad4c951d-1301-4998-bea2-ddeb3798fc66)

**Insight: Kategori Produk yang Paling Diminati**

Dari analisis transaksi pada kuartal kedua tahun 2004 (status Shipped), diperoleh bahwa:
- Kategori S18 merupakan yang paling diminati, dengan 25 pesanan dan total penjualan 2.264 unit.
- Diikuti oleh Kategori S24 sebanyak 21 pesanan dengan total penjualan 1.826 unit.
- Kategori S32 dan S70 menunjukkan rasio pembelian yang cukup tinggi dibanding pesanan yang relatif lebih sedikit, menandakan potensi produk dengan volume besar per transaksi.

Temuan ini mengindikasikan bahwa S18 dan S24 adalah kategori produk utama yang mendorong penjualan selama periode tersebut. 

5. Seberapa besar tingkat retensi atau loyalitas pelanggan antarkuartal?
<pre lang="markdown">
#Menghitung total unik customers yang transaksi di quarter_1
SELECT COUNT(DISTINCT customerID) as total_customers FROM orders_1;
#output = 25
SELECT
	'1' AS quarter,
	COUNT(DISTINCT(customerID)) * 100/25 AS Q2
FROM orders_1
WHERE customerID IN(
		SELECT
			DISTINCT(customerID)
		FROM orders_2);
</pre>

![image](https://github.com/user-attachments/assets/fdece51a-aefb-4336-b2a1-4f8971527440)

**Insight: Retensi Pelanggan dan Dampaknya terhadap Penjualan**

Berdasarkan data yang dianalisis, hanya 24% pelanggan dari kuartal pertama yang melakukan repeat order pada kuartal kedua. Dengan kata lain, 76% pelanggan tidak kembali bertransaksi, yang berkontribusi langsung terhadap penurunan volume penjualan pada Q2.

Rendahnya tingkat repeat order ini mengindikasikan perlunya evaluasi strategi retensi pelanggan—baik dari sisi pemasaran, pengelolaan relasi pelanggan, maupun keunggulan produk yang ditawarkan. Perusahaan xyz.com disarankan untuk meninjau ulang pendekatan yang digunakan dalam mempertahankan pelanggan agar dapat meningkatkan loyalitas dan performa bisnis di kuartal berikutnya.

## ✅ Kesimpulan
Berdasarkan data yang telah kita peroleh melalui query SQL, Kita dapat menarik kesimpulan bahwa :

1. Performance xyz.com menurun signifikan di quarter ke-2, terlihat dari nilai penjualan dan revenue yang drop hingga 20% dan 24%,
2. Perolehan customer baru juga tidak terlalu baik, dan sedikit menurun dibandingkan quarter sebelumnya.
3. Ketertarikan customer baru untuk berbelanja di xyz.com masih kurang, hanya sekitar 56% saja yang sudah bertransaksi. 4. Disarankan tim Produk untuk perlu mempelajari behaviour customer dan melakukan product improvement, sehingga conversion rate (register to transaction) dapat meningkat.
5. Produk kategori S18 dan S24 berkontribusi sekitar 50% dari total order dan 60% dari total penjualan, sehingga xyz.com sebaiknya fokus untuk pengembangan category S18 dan S24.
6. Retention rate customer xyz.com juga sangat rendah yaitu hanya 24%, artinya banyak customer yang sudah bertransaksi di quarter-1 tidak kembali melakukan order di quarter ke-2 (no repeat order).
7. xyz.com mengalami pertumbuhan negatif di quarter ke-2 dan perlu melakukan banyak improvement baik itu di sisi produk dan bisnis marketing, jika ingin mencapai target dan positif growth di quarter ke-3. Rendahnya retention rate dan conversion rate bisa menjadi diagnosa awal bahwa customer tidak tertarik/kurang puas/kecewa berbelanja di xyz.com.



