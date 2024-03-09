## Menambahkan Primary Key
```sql
ALTER TABLE customers
ADD CONSTRAINT customers_pk
PRIMARY KEY (customer_id);

ALTER TABLE	product
ADD CONSTRAINT product_pk
PRIMARY KEY (product_id);

ALTER TABLE sellers
ADD CONSTRAINT sellers_pk
PRIMARY KEY (seller_id);

ALTER TABLE orders
ADD CONSTRAINT orders_pk
PRIMARY KEY (order_id);
```
## Menambahkan Foreign Key
```sql
ALTER TABLE orders
ADD CONSTRAINT orders_fk
FOREIGN KEY (customer_id)
REFERENCES customers (customer_id);

ALTER TABLE order_reviews
ADD CONSTRAINT order_reviews_fk
FOREIGN KEY (order_id)
REFERENCES orders (order_id);

ALTER TABLE order_payments
ADD CONSTRAINT order_payments_fk
FOREIGN KEY (order_id)
REFERENCES orders (order_id);

ALTER TABLE order_items
ADD CONSTRAINT order_items_fk
FOREIGN KEY (order_id)
REFERENCES orders (order_id);

ALTER TABLE order_items
ADD CONSTRAINT order_items_fk2
FOREIGN KEY (product_id)
REFERENCES product (product_id);

ALTER TABLE order_items
ADD CONSTRAINT order_items_fk3
FOREIGN KEY (seller_id)
REFERENCES sellers (seller_id);
```
