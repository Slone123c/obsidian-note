# 列属性 Column Attributes
介绍了列拥有的一些属性

# 插入单行 | Inserting a Row
```SQL
-- 拥有默认值的属性可以填写默认值或者DEFAULT关键字
INSERT INTO customers
VALUES (
 DEFAULT,
 'John', 
 'Smith',
 '1990-01-01',
 NULL,
 'address',
 'city',
 'CA',
 DEFAULT)
--  选择对应的列属性加入
INSERT INTO customers (
	last_name, 
	first_name,
	birth_date,
	address,
	city,
	state)
VALUES (
 'John', 
 'Smith',
 '1990-01-01',
 'address',
 'city',
 'CA')
```


# 3- 插入多行 | Inserting Multiple Rows
```SQl
INSERT INTO shippers (name)
VALUES('Shipper1'),
	  ('Shipper2'),
	  ('Shipper3')
			
```

# 4- 插入分层行 | Inserting Hierarchical Rows
```SQL
INSERT INTO orders (customer_id, order_date, status)
VALUES(1, '2019-01-02', 1);

INSERT INTO order_items
VALUES 
	(LAST_INSERT_ID(), 1, 1, 2.95),
	(LAST_INSERT_ID(), 2, 1, 3.95)

SELECT LAST_INSERT_ID()

```