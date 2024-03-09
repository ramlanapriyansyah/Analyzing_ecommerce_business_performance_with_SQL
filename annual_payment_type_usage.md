```sql
-- Tipe pembayaran secara all time
SELECT
	payment_type,
	count(*) AS total
FROM
	order_payments op
GROUP BY
	1
ORDER BY
	2 DESC;


 
-- Tipe Pembayaran per Tahun
SELECT
	EXTRACT(YEAR FROM order_purchase_timestamp) AS tahun,
	op.payment_type,
	count(payment_type) AS total,
	round(avg(payment_installments),2) AS rata_rata_angsuran
FROM
	orders o
JOIN
	order_payments op
	ON o.order_id = op.order_id
GROUP BY
	1, 2
ORDER BY
	1, 3 DESC;
```
