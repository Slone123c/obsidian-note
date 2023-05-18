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

8. 多表外连接