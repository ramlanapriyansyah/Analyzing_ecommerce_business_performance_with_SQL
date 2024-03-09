# Overview
Dalam suatu perusahaan mengukur performa bisnis sangatlah penting untuk melacak, memantau, dan menilai keberhasilan atau kegagalan dari berbagai proses bisnis. Oleh karena itu, dalam paper ini akan menganalisa performa bisnis untuk sebuah perusahan eCommerce,  dengan memperhitungkan beberapa metrik bisnis yaitu pertumbuhan pelanggan, kualitas produk, dan tipe pembayaran.

# Tools dan Dataset
Dataset: dapat dilihat pada folder `dataset` </br>
Tools: PostgreSQL melalui DBeaver

# Data Preparation
Hal-hal yang dilakukan pada tahap Data Preparation adalah sebagai berikut:
1. **Import Dataset**. Melakukan import dataset yang terdiri dari tabel customers, geolocation, order_items, order_payments, order_reviews, orders, products, dan sellers, ke dalam RDBMS.
2. **Menambahkan Constraint**, berupa Primary Key dan Foreign Key sehingga menghasilkan Entity Relationship Diagram (ERD) seperti yang terlihat pada gambar berikut.
![ERD (1)](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/assets/135192484/1c7c2192-e884-4634-92d8-749b31e442ef)

Syntax query untuk menambahkan Primary Key dan Foreign Key dapat dilihat pada file `data_preparation`

# Annual Customer Activity Growth Analysis
Pada tahap ini dilakukan analisis terhadap customer activity tahunan melalui pembuatan table master yang terdiri dari beberapa metric, yaitu:
- monthly_active_user : Rata-rata jumlah pengguna aktif bulanan per tahun.
- customer_baru : Jumlah customer baru per tahun.
- customer_dengan_repeat_order : Jumlah customer yang melakukan order lebih dari 1 kali untuk masing-masing tahun.
- rata-rata order : Rata-rata jumlah order setiap customer per tahun.
  
![customer_activity_table](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/assets/135192484/a6ca84da-30a0-491e-a1b9-371595ad049e)

Tabel Annual Customer Activiy Growth merupakan hasil ekstraksi dari beberapa tabel menggunakan query seperti yang terlampir pada file `annual_customer_activity_growth`
### Temuan Hasil
1. Rata-rata jumlah pelanggan aktif bulanan (Monthly Active User) mengalami peningkatan dari tahun ke tahun. Dimulai dari 109 pelanggan pada tahun 2016, meningkat pesat menjadi 3,758 pada tahun 2017, kemudian terus meningkat menjadi total 5,401 pelanggan pada tahun 2018.
2. Pertumbuhan customer cukup signifikan dari tahun ke tahun. Jumlah customer baru meningkat pesat dari yang hanya berjumlah 329 customer pada tahun 2016 menjadi 45,101 pada tahun 2017. Dan angka tersebut terus meningkat hingga mencapai 54,011 customer baru pada tahun 2018.
3. Jumlah customer yang melakukan order lebih dari 1 kali (repeat order) meningkat pesat dari hanya 3 customer pada tahun 2016 menjadi 1,256 customer pada tahun 2017. Kemudian terjadi sedikit penurunan pada tahun 2018, menjadi 1,167 customer.
4. Secara keseluruhan, rata-rata order yang dilakukan customer setiap tahun bisa dikatakan stagnan. Terlihat bahwa rata-rata order yang dilakukan customer tidak pernah lebih dari 1 order dari tahun ke tahun.

# Annual Product Category Quality Analysis
Pada tahap ini dilakukan analisis terhadap kualitas kategori produk tahunan melalui pembuatan table master dengan keterangan sebagai berikut:
- total_pendapatan : Total revenue atau pendapatan perusahaan per tahun.
- cancel_order : Total cancel order yang dialami perusahaan per tahun.
- top_product_category : Kategori produk yang mendapatkan revenue terbesar per tahun.
- most_cancel_order_category : Kategori produk yang mengalami cancel order terbanyak per tahun.

  ![product_category_table](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/assets/135192484/a52726a2-0ade-4c22-b12e-6d75970e5a5e)

  Tabel Annual Product Category Quality di atas dihasilkan dengan query seperti yang terlampir pada file `annual_product_category_analysis`
### Temuan Hasil
1. Total revenue/pendapatan perusahaan meningkat tajam, dimana sebelumnya hanya di bawah 1 juta pada tahun 2016, meningkat menjadi 6,92 juta pada tahun 2017, dan terus meningkat hingga mencapai angka 8.45 juta pada tahun 2018.
2. Di satu sisi, total cancel order yang dialami perusahaan juga terus meningkat setiap tahun. Dari sebanyak 26 cancel order pada tahun 2016, menjadi 265 pada tahun 2017, dan meningkat lagi menjadi 334 pada tahun 2018.
3. Pada tahun 2016, kategori produk dengan revenue tertinggi dimiliki oleh *furniture_decor* dengan total revenue sebesar 6,899. Pada tahun 2017 revenue tertinggi dimiliki oleh kategori *bed_bath_table*, dengan total revenue sebesar 580,946. Dan pada tahun 2018 revenue tertinggi dimiliki oleh kategori *health_beuaty*, dengan total revenue sebesar 866,812.
4. Pada tahun 2016, jumlah cancel order terbanyak dimiliki oleh kategori *toys* dengan total cancel order sebanyak 3. Pada tahun 2017, jumlah cancel order terbanyak dimiliki oleh kategori *sport_leisure* dengan total cancel order sebanyak 25. Dan pada tahun 2018, jumlah cancel order terbanyak dimiliki oleh kategori *health_beauty* dengan total cancel order sebanyak 27.

# Analysis of Annual Payment Type Usage
Pada tahap ini dilakukan pembuatan tabel yang berisi informasi mengenai penggunaan tipe pembayaran untuk setiap tahun seperti yang tertera pada tabel berikut:

![annual_payment_type_usage_table](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/assets/135192484/edd6d16c-8cf5-4925-902b-1c6409e92240)


Query dapat dilihat pada file: `annual_payment_type_usage`

### Temuan Hasil
1. Tipe pembayaran favorit secara all time adalah pembayaran melalui credit_card, yaitu sebanyak 76,800; disusul boleto sebanyak 19,800; voucher sebanyak 5,800; dan debit_card sebanyak 1,500. Sedangkan tipe pembayaran lainnya hanya di bawah 100.
2. Untuk tipe pembayaran credit_card sendiri memiliki rata-rata angsuran antara 3-4 kali di masing-masing tahun.





