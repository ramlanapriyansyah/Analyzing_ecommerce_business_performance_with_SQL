```sql
--Membuat Tabel Pendapatan per Tahun
CREATE TABLE revenue AS
WITH tem AS(
	SELECT
		EXTRACT(YEAR FROM o.order_purchase_timestamp) AS tahun,
		oi.price + oi.freight_value AS pendapatan
	FROM
		orders o
	JOIN
		order_items oi
		ON o.order_id = oi.order_id
	WHERE
		o.order_status = 'delivered'
)
SELECT
	tahun,
	ceil(sum(pendapatan)) AS total_pendapatan
FROM
	tem
GROUP BY
	1;


-- Membuat Tabel Jumlah Cancel Order per Tahun
CREATE TABLE cancel_orders AS
WITH tem AS(
	SELECT
		order_id,
		EXTRACT(YEAR FROM order_purchase_timestamp) AS tahun,
		order_status
	FROM
		orders
	WHERE
		order_status = 'canceled'
)
SELECT
	tahun,
	count(order_status) AS cancel_order
FROM
	tem
GROUP BY
	1;


-- Membuat Tabel Top Kategori Produk yang Menghasilkan Revenue Terbesar per Tahun
CREATE TABLE top_product_categories AS
WITH tem AS(
	SELECT
		EXTRACT(YEAR FROM order_purchase_timestamp) AS tahun,
		p.product_category_name,
		sum(oi.price + oi.freight_value) AS revenue	
	FROM
		orders o
	JOIN
		order_items oi
		ON o.order_id = oi.order_id
	JOIN
		product p
		ON p.product_id = oi.product_id
WHERE
		order_status = 'delivered'
	GROUP BY
		1, 2
),
max_revenue AS(
	SELECT
		tahun,
		product_category_name,
		revenue,
		max(revenue) OVER (PARTITION BY tahun) AS max_rev
	FROM
		tem
)
SELECT
	tahun,
	product_category_name AS top_product_category,
	floor(revenue) AS revenue
FROM
	max_revenue
WHERE
	revenue = max_rev;


-- Membuat Tabel Kategori yang Mengalami Cancel Order Terbanyak per Tahun
CREATE TABLE most_canceled_order AS
WITH tem AS(
	SELECT
		EXTRACT(YEAR FROM order_purchase_timestamp) AS tahun,
		p.product_category_name,
		count(o.order_id) AS canceled_order
	FROM
		orders o
	JOIN
		order_items oi 
		ON o.order_id = oi.order_id
	JOIN	
		product p
		ON p.product_id = oi.product_id
	WHERE
		o.order_status = 'canceled'
	GROUP BY
		1, 2
),
tem2 AS(
	SELECT
		tahun,
		product_category_name,
		canceled_order,
		max(canceled_order) OVER(PARTITION BY tahun) AS max_canceled_order
	FROM
		tem
)
SELECT
	tahun,
	product_category_name,
	max_canceled_order AS total_canceled_order
FROM
	tem2
WHERE
	canceled_order = max_canceled_order;


-- Membuat Tabel Master Annual Product Category Analysis
CREATE TABLE annual_product_category AS
SELECT
	r.tahun,
	total_pendapatan,
	cancel_order,
	top_product_category,
	mco.product_category_name AS most_cancel_order_category
FROM
	revenue r
JOIN
	cancel_orders co
	ON r.tahun = co.tahun
JOIN
	top_product_categories tpc
	ON r.tahun = tpc.tahun
JOIN
	most_canceled_order mco
	ON r.tahun = mco.tahun;
```
