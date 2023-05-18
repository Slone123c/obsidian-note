1. 内连接
	1. INNER JOIN 或 JOIN ON xxx = xxx 将两表内容连接
2. 跨数据库连接
	1. 数据库.数据表 表示对应数据库的表
3. 自连接
	1. 将一个表与自身 JOIN
4. 多表连接
	1. 使用多个 JOIN 连接多个表
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