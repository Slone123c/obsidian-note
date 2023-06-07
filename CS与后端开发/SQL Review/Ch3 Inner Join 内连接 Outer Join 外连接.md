1. 内连接
	1. INNER JOIN 或 JOIN ON xxx = xxx 将两表内容连接
2. 跨数据库连接
	1. 用 数据库.数据表 方式表示对应数据库的表
3. 自连接
	1. 将一个表与自身 JOIN ON
4. 多表连接
	1. 使用多个 JOIN ON 连接多个表
5. 复合连接条件
	1. 在JOIN 中 用 AND 连接 ON 条件
6. 隐式连接
	1. 用 WHERE 别名.列名 = 别名.列名 来表示JOIN
```SQL
SELECT * 
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id
------ 等价 SQL 语句

--隐式连接
SELECT * 
FROM orders o, customers c
WHERE o.customer_id = c.customer_id
```


7. 外连接
``` SQL
SELECT 
		c.customer_id,
		c.first_name,
		o.order_id
FROM customers c
LEFT JOIN orders o
	ON c.customer_id = o.customer_id
ORDER BY c.customer_id
-- 使用LEFT JOIN 时，在 `customers` 表中有对应 `customer_id` 的行而在 `orders` 表中没有对应的行时，仍然会返回该行

SELECT 
		c.customer_id,
		c.first_name,
		o.order_id
FROM customers c
RIGHT JOIN orders o
	ON c.customer_id = o.customer_id
ORDER BY c.customer_id
-- RIGHT JOIN 时，右连接保证了即使在 `orders` 表中有对应 `customer_id` 的行而在 `customers` 表中没有对应的行时，仍然会返回该行

```


#### 8. 多表外连接
与多个外连接同理，使用多个LEFT JOIN

#### 9. 自外连接
使用JOIN ON 作用于相同的表
```sql
USE sql_hr

SELECT 
		e.employee_id,
		e.first_name,
		m.first_name AS manager
FROM employees e
LEFT JOIN employees m
	ON e.reports_to = m.employee_id
```

#### 10. USING 字句
使用USING来简化JOIN语句，只能作用于列名完全相同的情况
```sql
SELECT
	o.order_id,
	c.first_name,
	sh.name AS shipper
FROM orders o
JOIN customers c
	-- ON o.customer_id = c.customer_id
	USING (customer_id)
LEFT JOIN shippers sh
	USING (shipper_id)

-- Exercise
SELECT 
date,
c.name AS client,
amount,
pm.name AS name
FROM payments p
JOIN clients c
	USING (client_id)
JOIN payment_methods pm
	ON p.payment_method = pm.payment_method_id
```

#### 11. 自然连接
自动基于共同的列连接，但可能会出现不希望的结果
```sql
SELECT 
	o.order_id,
	c.first_name
FROM orders o
NATURAL JOIN customers c
```

#### 12.交叉连接
用于连接第一个表的每条记录和第二个表的每条记录(所有记录的组合)
实际案列中，会用于需要组合数据
隐式调用：选择多个表
```sql
SELECT 
	c.first_name AS customer,
	p.name AS product
FROM customers c
CROSS JOIN products p
```


#### 13. 联合
使用UNION可以合并多段查询的记录，返回的列数量应该一致，第一段的选择决定了列名
```SQL
SELECT 
	order_id,
	order_date,
	'Active' AS status
FROM orders
WHERE order_date >= '2019-01-01'
UNION
SELECT 
	order_id,
	order_date,
	'Archived' AS status
FROM orders
WHERE order_date < '2019-01-01'

-- Exercise
SELECT 
	customer_id,
	first_name,
	points,
	'Bronze' AS type
FROM customers
WHERE points < 2000
UNION
SELECT 
	customer_id,
	first_name,
	points,
	'Silver' AS type
FROM customers
-- WHERE points >= 2000 and points < 3000
WHERE points BETWEEN 2000 and 3000
UNION
SELECT 
	customer_id,
	first_name,
	points,
	'Gold' AS type
FROM customers
WHERE points >= 3000
ORDER BY first_name
```