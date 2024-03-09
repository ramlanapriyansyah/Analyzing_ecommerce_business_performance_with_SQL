## Membuat Table Master Annual Customer Activity Growth
```sql
-- Membuat tabel Monthly Active Users per Tahun
CREATE TABLE monthly_active_users AS
WITH tem AS(
	SELECT
		EXTRACT(YEAR FROM order_purchase_timestamp) AS tahun,
		to_char(order_purchase_timestamp, 'Month') AS bulan,
		count(DISTINCT customer_id) AS active_user
	FROM orders
	GROUP BY 1, 2
	ORDER BY 1, 2
)
SELECT
	tahun,
	floor(avg(active_user)) AS monthly_active_user
FROM
	tem
GROUP BY 1;

-- Membuat Tabel Jumlah Customer Baru per Tahun
CREATE TABLE customer_baru AS
WITH tem AS(
	SELECT
		DISTINCT customer_id,
		EXTRACT(YEAR FROM order_purchase_timestamp) AS tahun,
		min(order_purchase_timestamp) AS first_order
	FROM
		orders
	GROUP BY
	1, 2
	ORDER BY
	2
)
SELECT
	tahun,
	count(customer_id) AS jumlah_customer_baru
FROM
	tem
GROUP BY
1;

-- Membuat Tabel Jumlah Rata-rata Customer dengan Repeat Order per Tahun
CREATE TABLE customer_dengan_repeat_order AS
WITH tem AS (
	SELECT
		cust.customer_unique_id,
		EXTRACT (YEAR FROM ord.order_purchase_timestamp) AS tahun,
		count(ord.order_id) AS total_order
	FROM
		customers cust
	JOIN
		orders ord
		ON cust.customer_id = ord.customer_id
	GROUP BY
		1, 2
	HAVING
		count(ord.order_id) >= 2
)
SELECT
	tahun,
	count(customer_unique_id) AS total_customer
FROM
	tem
GROUP BY 1
ORDER BY 1;

-- Membuat Tabel Jumlah Rata-rata Order untuk Setiap Customer per Tahun
CREATE TABLE rata_rata_orders AS
WITH tem AS (
	SELECT
		cust.customer_unique_id,
		EXTRACT (YEAR FROM ord.order_purchase_timestamp) AS tahun,
		count(ord.order_id) AS total_order
	FROM
		customers cust
	JOIN
		orders ord
		ON cust.customer_id = ord.customer_id
	GROUP BY
		1, 2
)
SELECT
	tahun,
	round(avg(total_order),2) AS rata_rata_order
FROM
	tem
GROUP BY 1
ORDER BY 1;

-- Membuat Table Master dari Ketiga Metrics
CREATE TABLE annual_customer_activity_growth AS
SELECT
	mau.tahun,
	monthly_active_user,
	jumlah_customer_baru AS cutomer_baru,
	total_customer AS customer_dengan_repeat_order,
	rata_rata_order
FROM
	monthly_active_users mau
JOIN
	customer_baru cb
	ON mau.tahun = cb.tahun
JOIN
	customer_dengan_repeat_order ro
	ON mau.tahun = ro.tahun
JOIN
	rata_rata_orders rro
	ON mau.tahun = rro.tahun;
```
