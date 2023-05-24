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
