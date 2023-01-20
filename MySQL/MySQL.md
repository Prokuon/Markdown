# MySQL必知必会

[TOC]



## 第一章 了解SQL

## 第二章 MySQL简介

## 第三章 使用MySQL

### 3.1 连接

```mysql
mysql -u root - p
```

### 3.2 选择数据库 ==(use)==

```mysql
use crashcourse
```

### 3.2 了解数据库和表 ==(show)==

```mysql
show databases
```

```mysql
+--------------------+
| Database           |
+--------------------+
| crashcourse        |
| information_schema |
| mysql              |
| performance_schema |
| sakila             |
| sys                |
| world              |
+--------------------+
```

```mysql
show tables
```

```mysql
+-----------------------+
| Tables_in_crashcourse |
+-----------------------+
| customers             |
| orderitems            |
| orders                |
| productnotes          |
| products              |
| vendors               |
+-----------------------+
```

```mysql
show columns from customers;
```

```mysql
+--------------+-----------+------+-----+---------+----------------+
| Field        | Type      | Null | Key | Default | Extra          |
+--------------+-----------+------+-----+---------+----------------+
| cust_id      | int       | NO   | PRI | NULL    | auto_increment |
| cust_name    | char(50)  | NO   |     | NULL    |                |
| cust_address | char(50)  | YES  |     | NULL    |                |
| cust_city    | char(50)  | YES  |     | NULL    |                |
| cust_state   | char(5)   | YES  |     | NULL    |                |
| cust_zip     | char(10)  | YES  |     | NULL    |                |
| cust_country | char(50)  | YES  |     | NULL    |                |
| cust_contact | char(50)  | YES  |     | NULL    |                |
| cust_email   | char(255) | YES  |     | NULL    |                |
+--------------+-----------+------+-----+---------+----------------+
```

## 第四章 检索数据

### 4.1 select语句 ==(select)==

### 4.2 检索单个列

```mysql
select prod_name
from products;
```

```mysql
+----------------+
| prod_name      |
+----------------+
| .5 ton anvil   |
| 1 ton anvil    |
| 2 ton anvil    |
| Detonator      |
| Bird seed      |
| Carrots        |
| Fuses          |
| JetPack 1000   |
| JetPack 2000   |
| Oil can        |
| Safe           |
| Sling          |
| TNT (1 stick)  |
| TNT (5 sticks) |
+----------------+
```

### 4.3 检索多个列

```mysql
select prod_id, prod_name, prod_price
from products;
```

```mysql
+---------+----------------+------------+
| prod_id | prod_name      | prod_price |
+---------+----------------+------------+
| ANV01   | .5 ton anvil   | 5.99       |
| ANV02   | 1 ton anvil    | 9.99       |
| ANV03   | 2 ton anvil    | 14.99      |
| DTNTR   | Detonator      | 13.00      |
| FB      | Bird seed      | 10.00      |
| FC      | Carrots        | 2.50       |
| FU1     | Fuses          | 3.42       |
| JP1000  | JetPack 1000   | 35.00      |
| JP2000  | JetPack 2000   | 55.00      |
| OL1     | Oil can        | 8.99       |
| SAFE    | Safe           | 50.00      |
| SLING   | Sling          | 4.49       |
| TNT1    | TNT (1 stick)  | 2.50       |
| TNT2    | TNT (5 sticks) | 10.00      |
+---------+----------------+------------+
```

### 4.4 检索所有列 ==(*)==

```mysql
select *
from products;
```

```mysql
+---------+---------+----------------+------------+----------------------------------------------------------------+
| prod_id | vend_id | prod_name      | prod_price | prod_desc                                                      |
+---------+---------+----------------+------------+----------------------------------------------------------------+
| ANV01   |    1001 | .5 ton anvil   | 5.99       | .5 ton anvil, black, complete with handy hook                  |
| ANV02   |    1001 | 1 ton anvil    | 9.99       | 1 ton anvil, black, complete with handy hook and carrying case |
| ANV03   |    1001 | 2 ton anvil    | 14.99      | 2 ton anvil, black, complete with handy hook and carrying case |
| DTNTR   |    1003 | Detonator      | 13.00      | Detonator (plunger powered), fuses not included                |
| FB      |    1003 | Bird seed      | 10.00      | Large bag (suitable for road runners)                          |
| FC      |    1003 | Carrots        | 2.50       | Carrots (rabbit hunting season only)                           |
| FU1     |    1002 | Fuses          | 3.42       | 1 dozen, extra long                                            |
| JP1000  |    1005 | JetPack 1000   | 35.00      | JetPack 1000, intended for single use                          |
| JP2000  |    1005 | JetPack 2000   | 55.00      | JetPack 2000, multi-use                                        |
| OL1     |    1002 | Oil can        | 8.99       | Oil can, red                                                   |
| SAFE    |    1003 | Safe           | 50.00      | Safe with combination lock                                     |
| SLING   |    1003 | Sling          | 4.49       | Sling, one size fits all                                       |
| TNT1    |    1003 | TNT (1 stick)  | 2.50       | TNT, red, single stick                                         |
| TNT2    |    1003 | TNT (5 sticks) | 10.00      | TNT, red, pack of 10 sticks                                    |
+---------+---------+----------------+------------+----------------------------------------------------------------+
```

### 4.5 检索不同的行 ==(distinct)==

```mysql
select distinct vend_id
from products;
```

```mysql
+---------+
| vend_id |
+---------+
|    1001 |
|    1002 |
|    1003 |
|    1005 |
+---------+
```

### 4.6 限制结果 ==(limit)==

```mysql
select prod_name
from products
limit 5;
```

```mysql
+--------------+
| prod_name    |
+--------------+
| .5 ton anvil |
| 1 ton anvil  |
| 2 ton anvil  |
| Detonator    |
| Bird seed    |
+--------------+
```

### 4.7 使用完全限定表名

```mysql
select products.prod_name
from crashcourse.products;
```

```mysql
+----------------+
| prod_name      |
+----------------+
| .5 ton anvil   |
| 1 ton anvil    |
| 2 ton anvil    |
| Detonator      |
| Bird seed      |
| Carrots        |
| Fuses          |
| JetPack 1000   |
| JetPack 2000   |
| Oil can        |
| Safe           |
| Sling          |
| TNT (1 stick)  |
| TNT (5 sticks) |
+----------------+
```

## 第五章 排序检索数据

### 5.1 排序数据 ==(order by)==

```mysql
select prod_name
from products
order by prod_name;
```

```mysql
+----------------+
| prod_name      |
+----------------+
| .5 ton anvil   |
| 1 ton anvil    |
| 2 ton anvil    |
| Bird seed      |
| Carrots        |
| Detonator      |
| Fuses          |
| JetPack 1000   |
| JetPack 2000   |
| Oil can        |
| Safe           |
| Sling          |
| TNT (1 stick)  |
| TNT (5 sticks) |
+----------------+
```

### 5.2 按多个列排序

```mysql
select prod_id, prod_price, prod_name
from products
order by prod_price, prod_name;
```

```mysql
+---------+------------+----------------+
| prod_id | prod_price | prod_name      |
+---------+------------+----------------+
| FC      | 2.50       | Carrots        |
| TNT1    | 2.50       | TNT (1 stick)  |
| FU1     | 3.42       | Fuses          |
| SLING   | 4.49       | Sling          |
| ANV01   | 5.99       | .5 ton anvil   |
| OL1     | 8.99       | Oil can        |
| ANV02   | 9.99       | 1 ton anvil    |
| FB      | 10.00      | Bird seed      |
| TNT2    | 10.00      | TNT (5 sticks) |
| DTNTR   | 13.00      | Detonator      |
| ANV03   | 14.99      | 2 ton anvil    |
| JP1000  | 35.00      | JetPack 1000   |
| SAFE    | 50.00      | Safe           |
| JP2000  | 55.00      | JetPack 2000   |
+---------+------------+----------------+
```

### 5.3 指定排序方向 ==(desc)==

```mysql
select prod_id, prod_price, prod_name
from products
order by prod_price desc;
```

```mysql
+---------+------------+----------------+
| prod_id | prod_price | prod_name      |
+---------+------------+----------------+
| JP2000  | 55.00      | JetPack 2000   |
| SAFE    | 50.00      | Safe           |
| JP1000  | 35.00      | JetPack 1000   |
| ANV03   | 14.99      | 2 ton anvil    |
| DTNTR   | 13.00      | Detonator      |
| FB      | 10.00      | Bird seed      |
| TNT2    | 10.00      | TNT (5 sticks) |
| ANV02   | 9.99       | 1 ton anvil    |
| OL1     | 8.99       | Oil can        |
| ANV01   | 5.99       | .5 ton anvil   |
| SLING   | 4.49       | Sling          |
| FU1     | 3.42       | Fuses          |
| FC      | 2.50       | Carrots        |
| TNT1    | 2.50       | TNT (1 stick)  |
+---------+------------+----------------+
```

`order by` 与`limit` 组合使用，可以找出最高或最低的值

## 第六章 过滤数据

### 6.1 使用where语句 ==(where)==

```mysql
select prod_name, prod_price
from products
where prod_price = 2.50;
```

### 6.2 ==where子句操作符==

| **操作符** |      **说明**      |
| :--------: | :----------------: |
|     =      |        等于        |
|     <>     |       不等于       |
|     !=     |       不等于       |
|     <      |        小于        |
|     <=     |      小于等于      |
|     >      |        大于        |
|     >=     |      大于等于      |
|  between   | 在指定的两个值之间 |

#### 6.2.1 检查单个值

#### 6.2.2 不匹配检查

#### 6.2.3 范围值检查 ==(between and)==

#### 6.2.4 空值检查 ==(is null)==

```mysql
select prod_name
from products
where prod_price is null;
```

## 第七章 数据过滤

### 7.1 组合where子句

#### 7.1.1 and操作符 ==(and)==

```mysql
select prod_id, prod_price, prod_name
from products
where vend_id = 1003 and prod_price <= 10;
```

```mysql
+---------+------------+----------------+
| prod_id | prod_price | prod_name      |
+---------+------------+----------------+
| FB      | 10.00      | Bird seed      |
| FC      | 2.50       | Carrots        |
| SLING   | 4.49       | Sling          |
| TNT1    | 2.50       | TNT (1 stick)  |
| TNT2    | 10.00      | TNT (5 sticks) |
+---------+------------+----------------+
```

#### 7.1.2 or操作符 ==(or)==

```mysql
select prod_name, prod_price
from products
where vend_id = 1002 or vend_id = 1003;
```

```mysql
+----------------+------------+
| prod_name      | prod_price |
+----------------+------------+
| Fuses          | 3.42       |
| Oil can        | 8.99       |
| Detonator      | 13.00      |
| Bird seed      | 10.00      |
| Carrots        | 2.50       |
| Safe           | 50.00      |
| Sling          | 4.49       |
| TNT (1 stick)  | 2.50       |
| TNT (5 sticks) | 10.00      |
+----------------+------------+
```

#### 7.1.3 计算次序

and操作符优先级比or更高

```mysql
select prod_name, prod_price
from products
where (vend_id = 1002 or vend_id = 1003) and prod_price >= 10;
```

```mysql
+----------------+------------+
| prod_name      | prod_price |
+----------------+------------+
| Detonator      | 13.00      |
| Bird seed      | 10.00      |
| Safe           | 50.00      |
| TNT (5 sticks) | 10.00      |
+----------------+------------+
```

### 7.2 in操作符 ==(in)==

```mysql
select prod_name, prod_price
from products
where vend_id in (1002, 1003)
order by prod_name;
```

```mysql
+----------------+------------+
| prod_name      | prod_price |
+----------------+------------+
| Bird seed      | 10.00      |
| Carrots        | 2.50       |
| Detonator      | 13.00      |
| Fuses          | 3.42       |
| Oil can        | 8.99       |
| Safe           | 50.00      |
| Sling          | 4.49       |
| TNT (1 stick)  | 2.50       |
| TNT (5 sticks) | 10.00      |
+----------------+------------+
```

### 7.3 not操作符 ==(not)==

```mysql
select prod_name, prod_price
from products
where vend_id not in (1002, 1003)
order by prod_name;
```

```mysql
+--------------+------------+
| prod_name    | prod_price |
+--------------+------------+
| .5 ton anvil | 5.99       |
| 1 ton anvil  | 9.99       |
| 2 ton anvil  | 14.99      |
| JetPack 1000 | 35.00      |
| JetPack 2000 | 55.00      |
+--------------+------------+
```

## 第八章 用通配符进行过滤

### 8.1 like操作符 ==(like)==

#### 8.1.1 百分号(%)通配符 ==(%)==

```mysql
select prod_id, prod_name
from products
where prod_name like 'jet%';
```

```mysql
+---------+--------------+
| prod_id | prod_name    |
+---------+--------------+
| JP1000  | JetPack 1000 |
| JP2000  | JetPack 2000 |
+---------+--------------+
```

#### 8.1.2 下划线 (\_) 通配符  ==(\_)==

```mysql
select prod_id, prod_name
from products
where prod_name like '_ ton anvil';
```

```mysql
+---------+-------------+
| prod_id | prod_name   |
+---------+-------------+
| ANV02   | 1 ton anvil |
| ANV03   | 2 ton anvil |
+---------+-------------+
```

## 第九章 用正则表达式进行搜索

### 9.1 正则表达式介绍

### 9.2 使用MySQL正则表达式

#### 9.2.1 基本字符匹配 ==(.)==

```mysql
select prod_name
from products
where prod_name regexp '1000'
order by prod_name;
```

```mysql
+--------------+
| prod_name    |
+--------------+
| JetPack 1000 |
+--------------+
```

```mysql
select prod_name
from products
where prod_name regexp '.000'
order by prod_name;
```

```mysql
+--------------+
| prod_name    |
+--------------+
| JetPack 1000 |
| JetPack 2000 |
+--------------+
```

#### 9.2.2 进行or匹配 ==(or)==

```mysql
select prod_name
from products
where prod_name regexp '1000|2000'
order by prod_name;
```

```mysql
+--------------+
| prod_name    |
+--------------+
| JetPack 1000 |
| JetPack 2000 |
+--------------+
```

#### 9.2.3 匹配几个字符之一 ==([ ])==

```mysql
select prod_name
from products
where prod_name regexp '[123] Ton'
order by prod_name;
```

```mysql
+-------------+
| prod_name   |
+-------------+
| 1 ton anvil |
| 2 ton anvil |
+-------------+
```

#### 9.2.4 匹配范围 ==([ - ])==

```mysql
select prod_name
from products
where prod_name regexp '[1-5] Ton'
order by prod_name;
```

```mysql
+--------------+
| prod_name    |
+--------------+
| .5 ton anvil |
| 1 ton anvil  |
| 2 ton anvil  |
+--------------+
```

#### 9.2.5 ==匹配特殊字符==

```mysql
select vend_name
from vendors
where vend_name regexp '\\.'
order by vend_name;
```

| 元字符 |   说明   |
| :----: | :------: |
|  \\\f  |   换页   |
|  \\\n  |   换行   |
|  \\\r  |   回车   |
|  \\\t  |   制表   |
|  \\\v  | 纵向制表 |

#### 9.2.6 ==匹配字符类==

|      类      |                          说明                          |
| :----------: | :----------------------------------------------------: |
| [ :alnum: ]  |            任意字母和数字（同[a-zA-Z0-9]）             |
| [ :alpha: ]  |                 任意字符（同[a-zA-Z]）                 |
| [ :blank: ]  |                 空格和制表（同[\\\t]）                 |
| [ :cntrl: ]  |           ASCII控制字符（ASCII 0到31和127）            |
| [ :digit: ]  |                  任意数字（同[0-9]）                   |
| [ :graph: ]  |            与[ :print: ]相同，但不包括空格             |
| [ :lower: ]  |                任意小写字母（同[a-z]）                 |
| [ :print: ]  |                     任意可打印字符                     |
| [ :punct: ]  |     既不在[ :alnum: ]又不在[ :cntrl: ]中的任意字符     |
| [ :space: ]  | 包括空格在内的任意空白字符（同[\\\f\\\n\\\r\\\t\\\v]） |
| [ :upper: ]  |                任意大写字母（同[A-Z]）                 |
| [ :xdigit: ] |           任意十六进制数字（同[a-fA-F0-9]）            |

#### 9.2.7 ==匹配多个实例==

| 元字符 |            说明            |
| :----: | :------------------------: |
|   *    |       0个或多个匹配        |
|   +    | 1个或多个匹配（等于{1,}）  |
|   ?    | 0个或1个匹配（等于{0,1}）  |
|  {n}   |        指定数目匹配        |
|  {n,}  |     不少于指定数目匹配     |
| {n, m} | 匹配数目范围（m不超过255） |

```mysql
select prod_name
from products
where prod_name regexp '\\([0-9] sticks?\\)'
order by prod_name;
```

```mysql
+----------------+
| prod_name      |
+----------------+
| TNT (1 stick)  |
| TNT (5 sticks) |
+----------------+
```

```mysql
select prod_name
from products
where prod_name regexp '[[:digit:]]{4}'
order by prod_name;
```

```mysql
+--------------+
| prod_name    |
+--------------+
| JetPack 1000 |
| JetPack 2000 |
+--------------+
```

```mysql
select prod_name
from products
where prod_name regexp '[0-9][0-9][0-9][0-9]'
order by prod_name;
```

#### 9.2.8 ==定位符==

| 元字符  |    说明    |
| :-----: | :--------: |
|    ^    | 文本的开始 |
|    $    | 文本的结尾 |
| [[:<:]] |  词的开始  |
| [[:>:]] |  词的结尾  |

```mysql
select prod_name
from products
where prod_name regexp '^[0-9\\.]'
order by prod_name;
```

```mysql
+--------------+
| prod_name    |
+--------------+
| .5 ton anvil |
| 1 ton anvil  |
| 2 ton anvil  |
+--------------+
```

## 第十章 创建计算字段

### 10.1 计算字段

### 10.2 拼接字段 ==(concat())==

```mysql
select concat (vend_name, '(', vend_country, ')')
from vendors
order by vend_name;
```

```mysql
+--------------------------------------------+
| concat (vend_name, '(', vend_country, ')') |
+--------------------------------------------+
| ACME(USA)                                  |
| Anvils R Us(USA)                           |
| Furball Inc.(USA)                          |
| Jet Set(England)                           |
| Jouets Et Ours(France)                     |
| LT Supplies(USA)                           |
+--------------------------------------------+
```

```mysql
select concat(rtrim(vend_name), '(', rtrim(vend_country), ')')
from vendors
order by vend_name;
```

```mysql
+---------------------------------------------------------+
| concat(rtrim(vend_name), '(', rtrim(vend_country), ')') |
+---------------------------------------------------------+
| ACME(USA)                                               |
| Anvils R Us(USA)                                        |
| Furball Inc.(USA)                                       |
| Jet \set(England)                                       |
| Jouets Et Ours(France)                                  |
| LT Supplies(USA)                                        |
+---------------------------------------------------------+
```

```mysql
select concat(rtrim(vend_name), '(', rtrim(vend_country), ')') as vend_titles
from vendors
order by vend_name;
```

```mysql
+------------------------+
| vend_titles            |
+------------------------+
| ACME(USA)              |
| Anvils R Us(USA)       |
| Furball Inc.(USA)      |
| Jet \Set(England)      |
| Jouets Et Ours(France) |
| LT Supplies(USA)       |
+------------------------+
```

### 10.3 ==执行算数计算==

```mysql
select prod_id, quantity, item_price
from orderitems
where order_num = 20005;
```

```mysql
+---------+----------+------------+
| prod_id | quantity | item_price |
+---------+----------+------------+
| ANV01   |       10 | 5.99       |
| ANV02   |        3 | 9.99       |
| TNT2    |        5 | 10.00      |
| FB      |        1 | 10.00      |
+---------+----------+------------+
```

```mysql
select prod_id, quantity, item_price, quantity*item_price as expanded_price
from orderitems
where order_num = 20005;
```

```mysql
+---------+----------+------------+----------------+
| prod_id | quantity | item_price | expanded_price |
+---------+----------+------------+----------------+
| ANV01   |       10 | 5.99       | 59.90          |
| ANV02   |        3 | 9.99       | 29.97          |
| TNT2    |        5 | 10.00      | 50.00          |
| FB      |        1 | 10.00      | 10.00          |
+---------+----------+------------+----------------+
```

| 操作符 | 说明 |
| :----: | :--: |
|   +    |  加  |
|   -    |  减  |
|   *    |  乘  |
|   /    |  除  |

## 第十一章 使用数据处理函数

### 11.1 函数

### 11.2 使用函数

#### 11.2.1 ==文本处理函数==

```mysql
select vend_name, upper(vend_name) as vend_name_upcase
from vendors
order by vend_name;
```

```mysql
+----------------+------------------+
| vend_name      | vend_name_upcase |
+----------------+------------------+
| ACME           | ACME             |
| Anvils R Us    | ANVILS R US      |
| Furball Inc.   | FURBALL INC.     |
| Jet \Set       | JET \SET         |
| Jouets Et Ours | JOUETS ET OURS   |
| LT Supplies    | LT SUPPLIES      |
+----------------+------------------+
```

|    函数     |       说明        |
| :---------: | :---------------: |
|   left()    |  返回串左边字符   |
|  length()   |   返回串的长度    |
|  locate()   | 找出串的一个子串  |
|   lower()   |  将串转化为小写   |
|   ltrim()   | 去掉串左边的空格  |
|   right()   | 返回串右边的字符  |
|   rtrim()   | 去掉串右边的空格  |
|  soundex()  | 返回串的soundex值 |
| substring() |  返回子串的字符   |
|   upper()   |  将串转化为大写   |

```mysql
select cust_name, cust_contact
from customers
where soundex(cust_contact) = soundex('Y Lie');
```

```mysql
+-------------+--------------+
| cust_name   | cust_contact |
+-------------+--------------+
| Coyote Inc. | Y Lee        |
+-------------+--------------+
```

#### 11.2.2 ==日期和时间处理函数==

|     函数      |              说明              |
| :-----------: | :----------------------------: |
|   adddate()   |     增加一个日期（天，周）     |
|   addtime()   |     增加一个时间（时，分）     |
|   curdate()   |          返回当前日期          |
|   curtime()   |          返回当前时间          |
|    date()     |     返回日期时间的日期部分     |
|  datediff()   |        计算两个日期之差        |
|  date_add()   |     高度灵活的日期运算函数     |
| date_format() |  返回一个格式化的日期或时间串  |
|     day()     |     返回一个日期的天数部分     |
|  dayofweek()  | 对于一个日期，返回对应的星期几 |
|    hour()     |     返回一个实践的小时部分     |
|   minute()    |     返回一个时间的分钟部分     |
|    month()    |     返回一个日期的月份部分     |
|     now()     |       返回当前日期和时间       |
|   second()    |      返回一个实践的秒部分      |
|    time()     |   返回一个日期时间的时间部分   |
|    year()     |     返回一个日期的年份部分     |

```mysql
select cust_id, order_num
from orders
where date(order_date) = '2005-09-01';
```

```mysql
+---------+-----------+
| cust_id | order_num |
+---------+-----------+
|   10001 |     20005 |
+---------+-----------+
```

``` mysql
select cust_id, order_num
from orders
where date(order_date) between '2005-09-01' and '2005-09-30';
```

```mysql
+---------+-----------+
| cust_id | order_num |
+---------+-----------+
|   10001 |     20005 |
|   10003 |     20006 |
|   10004 |     20007 |
+---------+-----------+
```

#### 11.2.3 ==数值处理函数==

|  函数  |        说明        |
| :----: | :----------------: |
| abs()  | 返回一个数的绝对值 |
| cos()  | 返回一个角度的余弦 |
| exp()  | 返回一个数的指数值 |
| mod()  |  返回除操作的余数  |
|  pi()  |     返回圆周率     |
| rand() |   返回一个随机数   |
| sin()  | 返回一个角度的正弦 |
| sqrt() | 返回一个数的平方根 |
| tan()  | 返回一个角度的正切 |

## 第十二章 汇总数据

### 12.1 ==聚集函数==

|  函数   |       说明       |
| :-----: | :--------------: |
|  avg()  | 返回某列的平均值 |
| count() |  返回某列的行数  |
|  max()  | 返回某列的最大值 |
|  min()  | 返回某列的最小值 |
|  sum()  |  返回某列值之和  |

#### 12.1.1 avg()函数 ==(avg())==

```mysql
select avg(prod_price) as avg_price
from products;
```

```mysql
+-----------+
| avg_price |
+-----------+
| 16.133571 |
+-----------+
```

#### 12.1.2 count()函数 ==(count())==

```mysql
select count(cust_email) as num_cust
from customers;
```

```mysql
+----------+
| num_cust |
+----------+
|        3 |
+----------+
```

#### 12.1.3 max()函数 ==(max())==

```mysql
select max(prod_price) as max_price
from products;
```

```mysql
+-----------+
| max_price |
+-----------+
| 55.00     |
+-----------+
```

#### 12.1.4 min()函数 ==(min())==

```mysql
select min(prod_price) as min_price
from products;
```

```mysql
+-----------+
| min_price |
+-----------+
| 2.50      |
+-----------+
```

#### 12.1.5 sum()函数 ==(sum())==

```mysql
select sum(quantity) as items_ordered
from orderitems
where order_num = 20005;
```

```mysql
+---------------+
| items_ordered |
+---------------+
| 19            |
+---------------+
```

```mysql
select sum(item_price * quantity) as total_price
from orderitems
where order_num = 20005;
```

```mysql
+-------------+
| total_price |
+-------------+
| 149.87      |
+-------------+
```

### 12.2 聚集不同值

```mysql
select avg(distinct prod_price) as avg_price
from products
where vend_id = 1003;
```

```mysql
+-----------+
| avg_price |
+-----------+
| 15.998000 |
+-----------+
```

### 12.3 组合聚集函数

``` mysql
select count(*) as num_items, 
	   min(prod_price) as price_min,
	   max(prod_price) as price_max,
	   avg(prod_price) as price_avg
from products;
```

```mysql
+-----------+-----------+-----------+-----------+
| num_items | price_min | price_max | price_avg |
+-----------+-----------+-----------+-----------+
|        14 | 2.50      | 55.00     | 16.133571 |
+-----------+-----------+-----------+-----------+
```

## 第十三章 分组数据

### 13.1 数据分组

```mysql
select count(*) as num_prods
from products
where vend_id = 1003;
```

```mysql
+-----------+
| num_prods |
+-----------+
|         7 |
+-----------+
```

### 13.2 创建分组 ==(group by)==

```mysql
select vend_id, count(*) as num_prods
from products
group by vend_id;
```

```mysql
+---------+-----------+
| vend_id | num_prods |
+---------+-----------+
|    1001 |         3 |
|    1002 |         2 |
|    1003 |         7 |
|    1005 |         2 |
+---------+-----------+
```

### 13.3 过滤分组 ==(having)==

```mysql
select cust_id, count(*) as orders
from orders
group by cust_id
having count(*) >= 2;
```

```mysql
+---------+--------+
| cust_id | orders |
+---------+--------+
|   10001 |      2 |
+---------+--------+
```

```mysql
select vend_id, count(*) as num_prods
from products
where prod_price >= 10
group by vend_id
having count(*) >= 2;
```

```mysql
+---------+-----------+
| vend_id | num_prods |
+---------+-----------+
|    1003 |         4 |
|    1005 |         2 |
+---------+-----------+
```

### 13.4 分组和排序

|              order by              |                       group by                       |
| :--------------------------------: | :--------------------------------------------------: |
|           排序产生的输出           |           分组行，但输出可能不是分组的顺序           |
| 任意列都可以使用（甚至非选择的列） | 只可能使用选择列或表达式，而且必须使用每个选择表达式 |
|             不一定需要             |   如果与聚集函数一起使用列（或表达式），则必须使用   |

```mysql
select order_num, sum(quantity * item_price) as ordertotal
from orderitems
group by order_num
having sum(quantity * item_price) >= 50;
```

```mysql
+-----------+------------+
| order_num | ordertotal |
+-----------+------------+
|     20005 | 149.87     |
|     20006 | 55.00      |
|     20007 | 1000.00    |
|     20008 | 125.00     |
+-----------+------------+
```

```mysql
select order_num, sum(quantity * item_price) as ordertotal
from orderitems
group by order_num
having sum(quantity * item_price) >= 50
order by ordertotal;
```

```mysql
+-----------+------------+
| order_num | ordertotal |
+-----------+------------+
|     20006 | 55.00      |
|     20008 | 125.00     |
|     20005 | 149.87     |
|     20007 | 1000.00    |
+-----------+------------+
```

### 13.5 ==select子语句顺序==

|   子句   |        说明        |      是否必须使用      |
| :------: | :----------------: | :--------------------: |
|  select  | 要返回的列或表达式 |           是           |
|   from   |  从中检索数据的表  | 仅在从表选择数据时使用 |
|  where   |      行级过滤      |           否           |
| group by |      分组说明      | 仅在按组计算聚集时使用 |
|  having  |      组级过滤      |           否           |
| order by |    输出排序顺序    |           否           |
|  limit   |    要检索的行数    |           否           |

## 第十四章 使用子查询

### 14.1 子查询

### 14.2 利用子查询进行过滤

```mysql
select order_num
from orderitems
where prod_id = 'TNT2';
```

```mysql
+-----------+
| order_num |
+-----------+
|     20005 |
|     20007 |
+-----------+
```

```mysql
select cust_id
from orders
where order_num in (20005, 20007);
```

```mysql
+---------+
| cust_id |
+---------+
|   10001 |
|   10004 |
+---------+
```

```mysql
select cust_id
from orders
where order_num in (select order_num
                    from orderitems
                   	where prod_id = 'TNT2');
```

```mysql
+---------+
| cust_id |
+---------+
|   10001 |
|   10004 |
+---------+
```

```mysql
select cust_name, cust_contact
from customers
where cust_id in (select cust_id
                  from orders
                  where order_num in (select order_num
                                      from orderitems
                                      where prod_id = 'TNT2'));
```

```mysql
+----------------+--------------+
| cust_name      | cust_contact |
+----------------+--------------+
| Coyote Inc.    | Y Lee        |
| Yosemite Place | Y Sam        |
+----------------+--------------+
```

### 14.3 作为计算字段使用子查询

```mysql
select count(*) as orders
from orders
where cust_id = 10001;
```

```mysql
select cust_name,
	   cust_state,
	   (select count(*)
       	from orders
       	where orders.cust_id = customers.cust_id) as orders
from customers
order by cust_name;
```

```mysql
+----------------+------------+--------+
| cust_name      | cust_state | orders |
+----------------+------------+--------+
| Coyote Inc.    | MI         |      2 |
| E Fudd         | IL         |      1 |
| Mouse House    | OH         |      0 |
| Wascals        | \IN        |      1 |
| Yosemite Place | AZ         |      1 |
+----------------+------------+--------+
```

```mysql
select cust_name,
	   cust_state,
	   (select count(*)
        from orders
        where cust_id = cust_id) as orders
from customers
order by cust_name;
```

```mysql
+----------------+------------+--------+
| cust_name      | cust_state | orders |
+----------------+------------+--------+
| Coyote Inc.    | MI         |      5 |
| E Fudd         | IL         |      5 |
| Mouse House    | OH         |      5 |
| Wascals        | \IN        |      5 |
| Yosemite Place | AZ         |      5 |
+----------------+------------+--------+
```

## 第十五章 联结表

### 15.1 联结

#### 15.1.1 关系表

#### 15.1.2 为什么要使用联结

### 15.2 ==创建联结==

```mysql
select vend_name, prod_name, prod_price
from vendors, products
where vendors.vend_id = products.vend_id
order by vend_name, prod_name;
```

```mysql
+-------------+----------------+------------+
| vend_name   | prod_name      | prod_price |
+-------------+----------------+------------+
| ACME        | Bird seed      | 10.00      |
| ACME        | Carrots        | 2.50       |
| ACME        | Detonator      | 13.00      |
| ACME        | Safe           | 50.00      |
| ACME        | Sling          | 4.49       |
| ACME        | TNT (1 stick)  | 2.50       |
| ACME        | TNT (5 sticks) | 10.00      |
| Anvils R Us | .5 ton anvil   | 5.99       |
| Anvils R Us | 1 ton anvil    | 9.99       |
| Anvils R Us | 2 ton anvil    | 14.99      |
| Jet Set     | JetPack 1000   | 35.00      |
| Jet Set     | JetPack 2000   | 55.00      |
| LT Supplies | Fuses          | 3.42       |
| LT Supplies | Oil can        | 8.99       |
+-------------+----------------+------------+
```

#### 15.2.1 where 子句的重要性

```mysql
select vend_name, prod_name, prod_price
from vendors, products
order by vend_name, prod_name;
```

> **笛卡尔积** 由没有联结条件的表关系返回的结果为笛卡尔积。
>
> 检索出的行的数目将是第一个表中的行数乘以第二个表中的行数。

#### 15.2.2 内部联结 ==(inner join)==

```mysql
select vend_name, prod_name, prod_price
from vendors inner join products
on vendors.vend_id = products.vend_id;

====================

select vend_name, prod_name, prod_price
from vendors, products
where vendors.vend_id = products.vend_id
order by vend_name, prod_name;
```

#### 15.2.3 联结多个表

```mysql
select prod_name, vend_name, prod_price, quantity
from orderitems, products, vendors
where products.vend_id = vendors.vend_id
and orderitems.prod_id = products.prod_id
and order_num = 20005;
```

```mysql
+----------------+-------------+------------+----------+
| prod_name      | vend_name   | prod_price | quantity |
+----------------+-------------+------------+----------+
| .5 ton anvil   | Anvils R Us | 5.99       |       10 |
| 1 ton anvil    | Anvils R Us | 9.99       |        3 |
| TNT (5 sticks) | ACME        | 10.00      |        5 |
| Bird seed      | ACME        | 10.00      |        1 |
+----------------+-------------+------------+----------+
```

```mysql
select cust_name, cust_contact
from customers
where cust_id in (select cust_id
                  from orders
                  where order_num in (select order_num
                                      from orderitems
                                      where prod_id = 'TNT2'));
                                      
====================

select cust_name, cust_contact
from customers, orders, orderitems
where customers.cust_id = orders.cust_id
and orderitems.order_num = orders.order_num
and prod_id = 'TNT2';
```

## 第十六章 创建高级联结

### 16.1 使用表别名

```mysql
select concat(rtrim(vend_name), '(', rtrim(vend_country), ')') as vend_title
from vendors
order by vend_name;
```

```mysql
+------------------------+
| vend_title             |
+------------------------+
| ACME(USA)              |
| Anvils R Us(USA)       |
| Furball Inc.(USA)      |
| Jet \Set(England)      |
| Jouets Et Ours(France) |
| LT Supplies(USA)       |
+------------------------+
```

```mysql
select cust_name, cust_contact
from customers as c, orders as o, orderitems as oi
where c.cust_id = o.cust_id
and oi.order_num = o.order_num
and prod_id = 'TNT2';
```

```mysql
+----------------+--------------+
| cust_name      | cust_contact |
+----------------+--------------+
| Coyote Inc.    | Y Lee        |
| Yosemite Place | Y Sam        |
+----------------+--------------+
```

### 16.2 使用不同类型的联结

#### 16.2.1 自联结

```mysql
select prod_id, prod_name
from products
where vend_id = (select vend_id
                 from products
                 where prod_id = 'DTNTR');
```

```mysql
+---------+----------------+
| prod_id | prod_name      |
+---------+----------------+
| DTNTR   | Detonator      |
| FB      | Bird seed      |
| FC      | Carrots        |
| SAFE    | Safe           |
| SLING   | Sling          |
| TNT1    | TNT (1 stick)  |
| TNT2    | TNT (5 sticks) |
+---------+----------------+
```

```mysql
select p1.prod_id, p1.prod_name
from products as p1, products as p2
where p1.vend_id = p2.vend_id
and p2.prod_id = 'DTNTR';
```

```mysql
+---------+----------------+
| prod_id | prod_name      |
+---------+----------------+
| DTNTR   | Detonator      |
| FB      | Bird seed      |
| FC      | Carrots        |
| SAFE    | Safe           |
| SLING   | Sling          |
| TNT1    | TNT (1 stick)  |
| TNT2    | TNT (5 sticks) |
+---------+----------------+
```

#### 16.2.2 自然联结

```mysql
select c.*, o.order_num, o.order_date,
oi.prod_id, oi.quantity, OI.item_price
from customers as c, orders as o, orderitems as oi
where c.cust_id = o.cust_id
and oi.order_num = o.order_num
and prod_id = 'FB';
```

```mysql
+---------+-------------+----------------+-----------+------------+----------+--------------+--------------+-----------------+-----------+---------------------+---------+----------+------------+
|   10001 | Coyote Inc. | 200 Maple Lane | Detroit   | MI         | 44444    | USA          | Y Lee        | ylee@coyote.com |     20005 | 2005-09-01 00:00:00 | FB      |        1 | 10.00      |
|   10001 | Coyote Inc. | 200 Maple Lane | Detroit   | MI         | 44444    | USA          | Y Lee        | ylee@coyote.com |     20009 | 2005-10-08 00:00:00 | FB      |        1 | 10.00      |
+---------+-------------+----------------+-----------+------------+----------+--------------+--------------+-----------------+-----------+---------------------+---------+----------+------------+
```

#### 16.2.3 外部联结 ==(outer join)==

```mysql
select customers.cust_id, orders.order_num
from customers inner join orders
on customers.cust_id = orders.cust_id;
```

```mysql
+---------+-----------+
| cust_id | order_num |
+---------+-----------+
|   10001 |     20005 |
|   10001 |     20009 |
|   10003 |     20006 |
|   10004 |     20007 |
|   10005 |     20008 |
+---------+-----------+
```

```mysql
select customers.cust_id, orders.order_num
from customers left outer join orders
on customers.cust_id = orders.cust_id;
```

```mysql
+---------+-----------+
| cust_id | order_num |
+---------+-----------+
|   10001 |     20005 |
|   10001 |     20009 |
|   10002 |      NULL |
|   10003 |     20006 |
|   10004 |     20007 |
|   10005 |     20008 |
+---------+-----------+
```

```mysql
select customers.cust_id, orders.order_num
from customers right outer join orders
on customers.cust_id = orders.cust_id;
```

```mysql
+---------+-----------+
| cust_id | order_num |
+---------+-----------+
|   10001 |     20005 |
|   10001 |     20009 |
|   10003 |     20006 |
|   10004 |     20007 |
|   10005 |     20008 |
+---------+-----------+
```

### 16.3 使用带聚集函数的联结

```mysql
select customers.cust_name,
	   customers.cust_id,
	   count(orders.order_num) as num_ord
from customers inner join orders
on customers.cust_id = orders.cust_id
group by customers.cust_id;
```

```mysql
+----------------+---------+---------+
| cust_name      | cust_id | num_ord |
+----------------+---------+---------+
| Coyote Inc.    |   10001 |       2 |
| Wascals        |   10003 |       1 |
| Yosemite Place |   10004 |       1 |
| E Fudd         |   10005 |       1 |
+----------------+---------+---------+
```

```mysql
select customers.cust_name,
	   customers.cust_id,
	   count(orders.order_num) as num_ord
from customers left outer join orders
on customers.cust_id = orders.cust_id
group by customers.cust_id;
```

```mysql
+----------------+---------+---------+
| cust_name      | cust_id | num_ord |
+----------------+---------+---------+
| Coyote Inc.    |   10001 |       2 |
| Mouse House    |   10002 |       0 |
| Wascals        |   10003 |       1 |
| Yosemite Place |   10004 |       1 |
| E Fudd         |   10005 |       1 |
+----------------+---------+---------+
```

### 16.4 使用联结和联结条件

* 注意所使用的联结类型。一般我们使用内部联结，但使用外部联结也是有效的。
* 保证使用正确的联结条件，否则将返回不正确的数据。
* 应该总是提供联结条件，否则会得出笛卡儿积。
* 在一个联结中可以包含多个表，甚至对于每个联结可以采用不同的联结类型。虽然这样做是合法的，一般也很有用，但应该在一起测试它们前，分别测试每个联结。这将使故障排除更为简单。

## 第十七章 组合查询

### 17.1 组合查询

### 17.2 创建组合查询

#### 17.2.1 使用union ==(union)==

```mysql
select vend_id, prod_id, prod_price
from products
where prod_price <= 5
union
select vend_id, prod_id, prod_price
from products
where vend_id in (1001, 1002)
order by vend_id;
```

```mysql
+---------+---------+------------+
| vend_id | prod_id | prod_price |
+---------+---------+------------+
|    1003 | FC      | 2.50       |
|    1002 | FU1     | 3.42       |
|    1003 | SLING   | 4.49       |
|    1003 | TNT1    | 2.50       |
|    1001 | ANV01   | 5.99       |
|    1001 | ANV02   | 9.99       |
|    1001 | ANV03   | 14.99      |
|    1002 | OL1     | 8.99       |
+---------+---------+------------+
```

```mysql
select vend_id, prod_id, prod_price
from products
where prod_price <= 5
or vend_id in (1001, 1002);
```

```mysql
+---------+---------+------------+
| vend_id | prod_id | prod_price |
+---------+---------+------------+
|    1001 | ANV01   | 5.99       |
|    1001 | ANV02   | 9.99       |
|    1001 | ANV03   | 14.99      |
|    1003 | FC      | 2.50       |
|    1002 | FU1     | 3.42       |
|    1002 | OL1     | 8.99       |
|    1003 | SLING   | 4.49       |
|    1003 | TNT1    | 2.50       |
+---------+---------+------------+
```

#### 17.2.2 union规则

* UNION必须由两条或两条以上的SELECT语句组成，语句之间用关键字UNION分隔（因此，如果组合4条SELECT语句，将要使用3个UNION关键字）。
* UNION中的每个查询必须包含相同的列、表达式或聚集函数（不过各个列不需要以相同的次序列出）。
* 列数据类型必须兼容：类型不必完全相同，但必须是DBMS可以隐含地转换的类型（例如，不同的数值类型或不同的日期类型）。

#### 17.2.3 包含或取消重复的行 ==(union all)==

``` mysql
select vend_id, prod_id, prod_price
from products
where prod_price <= 5
union all
select vend_id, prod_id, prod_price
from products
where vend_id in (1001, 1002);
```

```mysql
+---------+---------+------------+
| vend_id | prod_id | prod_price |
+---------+---------+------------+
|    1003 | FC      | 2.50       |
|    1002 | FU1     | 3.42       |
|    1003 | SLING   | 4.49       |
|    1003 | TNT1    | 2.50       |
|    1001 | ANV01   | 5.99       |
|    1001 | ANV02   | 9.99       |
|    1001 | ANV03   | 14.99      |
|    1002 | FU1     | 3.42       |
|    1002 | OL1     | 8.99       |
+---------+---------+------------+
```

#### 17.2.4 对组合查询结果排序

```mysql
select vend_id, prod_id, prod_price
from products
where prod_price <= 5
union
select vend_id, prod_id, prod_price
from products
where vend_id in (1001, 1002)
order by vend_id, prod_price;
```

```mysql
+---------+---------+------------+
| vend_id | prod_id | prod_price |
+---------+---------+------------+
|    1001 | ANV01   | 5.99       |
|    1001 | ANV02   | 9.99       |
|    1001 | ANV03   | 14.99      |
|    1002 | FU1     | 3.42       |
|    1002 | OL1     | 8.99       |
|    1003 | FC      | 2.50       |
|    1003 | TNT1    | 2.50       |
|    1003 | SLING   | 4.49       |
+---------+---------+------------+
```

## 第十八章 全文本搜索

### 18.1 理解全文本搜索

### 18.2 使用全文本搜索

#### 18.2.1 启用全文本搜索支持

```mysql
creat table productnotes
(
    note_id		int 		not null auto_increment,
    prod_id 	char(10)	not null,
    note_date	datetime	not null,
    note_text	text		null,
    primary key(note_id),
    fulltext(note_text)
)	engine = myisam;
```

#### 18.2.2 进行全文本搜索

```mysql
select note_text
from productnotes
where match(note_text) against('rabbit');
```

```mysql
+---------------------------------------------------------------------------------------------------------------------+
| note_text                                                                                                           |
+---------------------------------------------------------------------------------------------------------------------+
| Customer complaint: rabbit has been able to detect trap, food apparently less effective now.                        |
| Quantity varies, sold by the sack load.
All guaranteed to be bright and orange, and suitable for use as rabbit bait. |
+---------------------------------------------------------------------------------------------------------------------+
```

```mysql
select note_text
from productnotes
where note_text like '%rabbit%';
```

```mysql
+---------------------------------------------------------------------------------------------------------------------+
| note_text                                                                                                           |
+---------------------------------------------------------------------------------------------------------------------+
| Quantity varies, sold by the sack load.
All guaranteed to be bright and orange, and suitable for use as rabbit bait. |
| Customer complaint: rabbit has been able to detect trap, food apparently less effective now.                        |
+---------------------------------------------------------------------------------------------------------------------+
```

```mysql
select note_text,
match(note_text) against('rabbit') as ran
from productnotes;
```

```mysql
+----------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| note_text                                                                                                                                                | ran                |
+----------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Customer complaint:
Sticks not individually wrapped, too easy to mistakenly detonate all at once.
Recommend individual wrapping.                           |                  0 |
| Can shipped full, refills not available.
Need to order new can if refill needed.                                                                          |                  0 |
| Safe is combination locked, combination not provided with safe.
This is rarely a problem as safes are typically blown up or dropped by customers.         |                  0 |
| Quantity varies, sold by the sack load.
All guaranteed to be bright and orange, and suitable for use as rabbit bait.                                      | 1.5905543565750122 |
| Included fuses are short and have been known to detonate too quickly for some customers.
Longer fuses are available (item FU1) and should be recommended. |                  0 |
| Matches not included, recommend purchase of matches or detonator (item DTNTR).                                                                           |                  0 |
| Please note that no returns will be accepted if safe opened using explosives.                                                                            |                  0 |
| Multiple customer returns, anvils failing to drop fast enough or falling backwards on purchaser. Recommend that customer considers using heavier anvils. |                  0 |
| Item is extremely heavy. Designed for dropping, not recommended for use with slings, ropes, pulleys, or tightropes.                                      |                  0 |
| Customer complaint: rabbit has been able to detect trap, food apparently less effective now.                                                             | 1.6408053636550903 |
| Shipped unassembled, requires common tools (including oversized hammer).                                                                                 |                  0 |
| Customer complaint:
Circular hole in safe floor can apparently be easily cut with handsaw.                                                                |                  0 |
| Customer complaint:
Not heavy enough to generate flying stars around head of victim. If being purchased for dropping, recommend ANV02 or ANV03 instead.   |                  0 |
| Call from individual trapped in safe plummeting to the ground, suggests an escape hatch be added.
Comment forwarded to vendor.                            |                  0 |
+----------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
```

#### 18.2.3 使用查询扩展 ==(with query expansion)==

```mysql
select note_text
from productnotes
where match(note_text) against('anvils');
```

```mysql
+----------------------------------------------------------------------------------------------------------------------------------------------------------+
| note_text                                                                                                                                                |
+----------------------------------------------------------------------------------------------------------------------------------------------------------+
| Multiple customer returns, anvils failing to drop fast enough or falling backwards on purchaser. Recommend that customer considers using heavier anvils. |
+----------------------------------------------------------------------------------------------------------------------------------------------------------+
```

```mysql
select note_text
from productnotes
where match(note_text) against('anvils' with query expansion);
```

```mysql
+----------------------------------------------------------------------------------------------------------------------------------------------------------+
| note_text                                                                                                                                                |
+----------------------------------------------------------------------------------------------------------------------------------------------------------+
| Multiple customer returns, anvils failing to drop fast enough or falling backwards on purchaser. Recommend that customer considers using heavier anvils. |
| Customer complaint:
Sticks not individually wrapped, too easy to mistakenly detonate all at once.
Recommend individual wrapping.                           |
| Customer complaint:
Not heavy enough to generate flying stars around head of victim. If being purchased for dropping, recommend ANV02 or ANV03 instead.   |
| Please note that no returns will be accepted if safe opened using explosives.                                                                            |
| Customer complaint: rabbit has been able to detect trap, food apparently less effective now.                                                             |
| Customer complaint:
Circular hole in safe floor can apparently be easily cut with handsaw.                                                                |
| Matches not included, recommend purchase of matches or detonator (item DTNTR).                                                                           |
+----------------------------------------------------------------------------------------------------------------------------------------------------------+
```

> **行越多越好** 表中行越多，使用查询扩展返回的结果越好

#### 18.2.4 布尔文本搜索 ==(in boolean mode)==

```mysql
select note_text
from productnotes
where match(note_text) against('heavy -rope*' in boolean mode);
```

```mysql
+--------------------------------------------------------------------------------------------------------------------------------------------------------+
| note_text                                                                                                                                              |
+--------------------------------------------------------------------------------------------------------------------------------------------------------+
| Customer complaint:
Not heavy enough to generate flying stars around head of victim. If being purchased for dropping, recommend ANV02 or ANV03 instead. |
+--------------------------------------------------------------------------------------------------------------------------------------------------------+
```

| 布尔操作符 |                             说明                             |
| :--------: | :----------------------------------------------------------: |
|     +      |                       包含，词必须存在                       |
|     -      |                      排除，词必须不存在                      |
|     >      |                     包含，而且增加等级值                     |
|     <      |                     包含，而且减少等级值                     |
|     ()     |  把词组成子表达式（允许子表达式作为组被包含、排除、排列等）  |
|     ~      |                      取消一个词的排序值                      |
|     *      |                         词尾的通配符                         |
|     “”     | 定义一个短语（与单个词的列表不一样，它匹配整个短语以便包含或排除这个短语） |

```mysql
select note_text
from productnotes
where match(note_text) against('+rabbit +bait' in boolean mode);
```

匹配包含词 rabbit 和 bait 的行

```mysql
select note_text
from productnotes
where match(note_text) against('rabbit bait' in boolean mode);
```

匹配包含 rabbit 和 bait 中的至少一个词的行

```mysql
select note_text
from productnotes
where match(note_text) against('"rabbit bait"' in boolean mode);
```

匹配短语 rabbit bait

```mysql
select note_text
from productnotes
where match(note_text) against('>rabbit <carrot' in boolean mode);
```

匹配 rabbit 和 carrot，增强前者的等级，降低后者的等级。

```mysql
select note_text
from productnotes
where match(note_text) against('+safe +(<combination)' in boolean mode);
```

#### 18.2.5 全文本搜索的使用说明

## 第十九章 插入数据

### 19.1 数据插入

* 插入完整的行
* 插入行的一部分
* 插入多行
* 插入某些查询的结果

### 19.2 插入完整的行 ==(insert into)==

```mysql
insert into customers
values(null,
      'pep e. lapew',
      '100 main street',
      'los angeles',
      'ca',
      '90046',
      'usa',
      null,
      null);
```

```mysql
Query OK, 1 row affected (0.03 sec)
```

```mysql
insert into customers(cust_name,
                     cust_address,
                     cust_city,
                     cust_state,
                     cust_zip,
                     cust_country,
                     cust_contact,
                     cust_email)
values(null,
      'pep e. lapew',
      '100 main street',
      'los angeles',
      'ca',
      '90046',
      'usa',
      null,
      null);
```

### 19.3 插入多个行

```mysql
insert into customers(cust_name,
                     cust_address,
                     cust_city,
                     cust_state,
                     cust_zip,
                     cust_country)
values('pep e. lapew',
      '100 main street',
      'los angeles',
      'ca',
      '90046',
      'usa'),
      ('m. martian',
      '42 galaxy way',
      'new york',
      'ny',
      '11213',
      'usa');
```

```mysql
Query OK, 2 rows affected (0.05 sec)
Records: 2  Duplicates: 0  Warnings: 0
```

### 19.4 插入检索出的数据

```mysql
insert into customers(cust_id,
                    cust_contact,
                    cust_email,
                    cust_name,
                    cust_address,
                    cust_city,
                    cust_zip,
                    cust_country)
select cust_id,
	   cust_contact,
	   cust_email,
	   cust_name,
	   cust_address,
	   cust_city,
	   cust_zip,
	   cust_country
from custnew;
```

## 第二十章 更新和删除数据

### 20.1 更新数据 ==(update)==

* 更新表中特定行
* 更新表中所有行

```mysql
update customers
set cust_email = 'elmer@fudd.com'
where cust_id = 10005;
```

```mysql
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

```mysql
update customers
set cust_name = 'the fudds',
	cust_email = 'elmer@fudd.com'
where cust_id = 10005;
```

```mysql
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

### 20.2 删除数据 ==(delete)==

```mysql
delete from customers
where cust_id = 10006;
```

```mysql
Query OK, 1 row affected (0.01 sec)
```

**MySQL没有撤销按钮** 

## 第二十一章 创建和操纵表

### 21.1 创建表

#### 21.1.1 表创建基础 ==(create table)==

```mysql
create table cust
(cust_id		int			not null auto_increment,
 cust_name		char(50)	not null,
 cust_address	char(50)	null,
 cust_city		char(50)	null,
 cust_state		char(5)		null,
 cust_zip		char(10)	null,
 cust_country	char(50)	null,
 cust_contact	char(50)	null,
 cust_email		char(255)	null,
 primary key (cust_id)
) engine = innodb;
```

#### 21.1.2 使用null值 ==(null)==

```mysql
create table orders
(order_num 	int 		not null auto_increment,
 order_date datetime	not null,
 cust_id 	int			not null,
 primary key (order_num)
) engine = innodb;
```

#### 21.1.3 主键再介绍 ==(primary key)==

**主键值必须唯一。**即表中的每个行必须具有唯一的主键值。如果主键使用单个列，则它的值必须唯
一。如果使用多个列，则这些列的组合值必须唯一。

```mysql
create table orderitems
(
    order_num	int				not null,
    order_item	int				not null,
    prod_id		char(10)		not null,
    quantity	int				not null,
    item_price	decimal(8,2)	not null,
    primary key (order_num, order_item)
) engine = innodb;
```

`primary key (order_num, order_item)` 主键组合是唯一的

#### 21.1.4 使用auto_increment ==(auto_increment)==

#### 21.1.5 指定默认值 ==(default)==

```mysql
create table orderitems
(
    order_num	int				not null,
    order_item	int				not null,
    prod_id		char(10)		not null,
    quantity	int				not null	default 1,
    item_price	decimal(8,2)	not null,
    primary key (order_num, order_item)
) engine = innodb;
```

 **不允许函数** MySQL不允许使用函数作为默认值，它只支持常量

#### 21.1.6 引擎类型 ==(innodb, memory, myisam)==

* **innodb** 是一个可靠的事务处理引擎，它不支持文本搜索
* **memory** 在功能等同于 **myisam** ，但由于数据存储在内存（不是磁盘）中，速度很快（特别适用于临时表）
* **myisam** 是一个性能极高的引擎，它支持全文本搜索，不支持事务处理

引擎可以混用。

### 21.2 更新表 ==(alter table)==

```mysql
# 给表添加一个列
alter table vendors
add vend_phone char(20);
```

```mysql
# 删除刚刚添加的列
alter table vendors
drop column vend_phone;
```

### 21.3 删除表 ==(drop)==

```mysql
drop table customers2;
```

### 21.4 重命名表 ==(rename)==

```mysql
rename table customers2 to customers;
```

## 第二十二章 使用视图

### 22.1 视图

```mysql
select cust_name, cust_contact
from customers, orders, orderitems
where customers.cust_id = orders.cust_id
and orderitems.order_num = orders.order_num
and prod_id = 'TNT2';
```

#### 22.1.1 为什么使用视图

* 重用SQL语句
* 简化复杂的SQL操作。在编写查询后，可以方便地重用它而不必知道它的基本查询细节
* 使用表的组成部分而不是整个表
* 保护数据。可以给用户授予表的特定部分的访问权限而不是整个表的访问权限
* 更改数据格式和表示。视图可返回与底层表的表示和格式不同的数据

#### 22.1.2 视图的规则和限制

* 与表一样，视图必须唯一命名
* 对于可以创建的视图数目没有限制
* 为了创建视图，必须具有足够的访问权限
* 视图可以嵌套
* `order by` 可以用在视图中，但如果从该视图检索数据 `select` 也含有 `order by` ，那么该视图中的 `order by` 将被覆盖
* 视图不能索引，也不能有关联的触发器或默认值
* 视图可以和表一起使用。例如，编写一条联结表和视图的 `select` 语句

### 22.2 使用视图

* 视图用 `create view` 语句来创建
* 使用 `show create view viewname;` 来查看创建视图的语句
* 用 `drop` 删除视图，其语法为 `drop view viewname;`
* 更新视图时，可以先用 `drop` 再用 `create`，也可以直接用 `create or replace view`。如果要更新的视图不存在，则第二条更新语句会创建一个视图；如果要更新的视图存在，则第二条更新语句会替换原有的视图。

#### 22.2.1 利用视图简化复杂的联结 ==(create view)==

```mysql
create view productcustomers as
select cust_name, cust_contact, prod_id
from customers, orders, orderitems
where customers.cust_id = orders.cust_id
and orderitems.order_num = orders.order_num;
```

```mysql
select cust_name, cust_contact
from productcustomers
where prod_id = 'TNT2';
```

```mysql
+----------------+--------------+
| cust_name      | cust_contact |
+----------------+--------------+
| Coyote Inc.    | Y Lee        |
| Yosemite Place | Y Sam        |
+----------------+--------------+
```

#### 22.2.2 用视图重新格式化检索出的数据

```mysql
select concat(rtrim(vend_name), '(', rtrim(vend_country), ')') as vend_title
from vendors
order by vend_name;
```

```mysql
+------------------------+
| vend_title             |
+------------------------+
| ACME(USA)              |
| Anvils R Us(USA)       |
| Furball Inc.(USA)      |
| Jet \Set(England)      |
| Jouets Et Ours(France) |
| LT Supplies(USA)       |
+------------------------+
```

```mysql
create view vendorlocations as
select concat(rtrim(vend_name), '(', rtrim(vend_country), ')') as vend_title
from vendors
order by vend_name;
```

```mysql
select *
from vendorlocations;
```

```mysql
+------------------------+
| vend_title             |
+------------------------+
| ACME(USA)              |
| Anvils R Us(USA)       |
| Furball Inc.(USA)      |
| Jet \Set(England)      |
| Jouets Et Ours(France) |
| LT Supplies(USA)       |
+------------------------+
```

#### 22.2.3 用视图过滤不想要的数据

```mysql
create view customeremaillist as
select cust_id, cust_name, cust_email
from customers
where cust_email is not null;
```

```mysql
select *
from customeremaillist;
```

```mysql
+---------+----------------+---------------------+
| cust_id | cust_name      | cust_email          |
+---------+----------------+---------------------+
|   10001 | Coyote Inc.    | ylee@coyote.com     |
|   10003 | Wascals        | rabbit@wascally.com |
|   10004 | Yosemite Place | sam@yosemite.com    |
|   10005 | the fudds      | elmer@fudd.com      |
+---------+----------------+---------------------+
```

#### 22.2.4 使用视图与计算字段

```mysql
select prod_id,
quantity,
item_price,
quantity*item_price as expanded_price
from orderitems
where order_num = 20005;
```

```mysql
+---------+----------+------------+----------------+
| prod_id | quantity | item_price | expanded_price |
+---------+----------+------------+----------------+
| ANV01   |       10 | 5.99       | 59.90          |
| ANV02   |        3 | 9.99       | 29.97          |
| TNT2    |        5 | 10.00      | 50.00          |
| FB      |        1 | 10.00      | 10.00          |
+---------+----------+------------+----------------+
```

```mysql
create view orderitemsexpanded as
select order_num,
	   prod_id,
	   item_price,
	   quantity * item_price as expanded_price
from orderitems;
```

```mysql
select *
from orderitemsexpanded
where order_num = 20005;
```

```mysql
+-----------+---------+------------+----------------+
| order_num | prod_id | item_price | expanded_price |
+-----------+---------+------------+----------------+
|     20005 | ANV01   | 5.99       | 59.90          |
|     20005 | ANV02   | 9.99       | 29.97          |
|     20005 | TNT2    | 10.00      | 50.00          |
|     20005 | FB      | 10.00      | 10.00          |
+-----------+---------+------------+----------------+
```

#### 22.2.5 更新视图

如果视图定义中有以下操作，则不能进行视图的更新：

* 分组 (`group by  having`)
* 联结
* 子查询
* 并
* 聚集函数 (`min() count() sum()`)
* distinct
* 导出（计算）列

## 第二十三章 使用存储过程

### 23.1 存储过程

### 23.2 为什么要使用存储过程

### 23.3 使用存储过程

#### 23.3.1 执行存储过程

```mysql
call productpricing(@pricelow,
                   	@pricehigh,
                    @priceaverage);
```

#### 23.3.2 创建与使用存储过程 ==(create procedure，call)==

```mysql
create procedure productpricing()
begin
	select avg(prod_price) as priceaverage
	from products;
end;
```

```mysql
call productpricing();
```

```mysql
+--------------+
| priceaverage |
+--------------+
| 16.133571    |
+--------------+
```

#### 23.3.3 删除存储过程 ==(drop procedure)==

```mysql
drop procedure productpricing;
```

#### 23.3.4 使用参数 ==(in，out，inout)==

```mysql
create procedure productpricing
(
    out pl decimal(8,2),
    out ph decimal(8,2),
    out pa decimal(8,2)
)
begin
	select min(prod_price)
	into pl
	from products;
	select max(prod_price)
	into ph
	from products;
	select avg(prod_price)
	into pa
	from products;
end;
```

```mysql
call productpricing
(
    @pricelow,
    @pricehigh,
    @priceaverage
);
```

```mysql
select @priceaverage;
```

```mysql
+---------------+
| @priceaverage |
+---------------+
| 16.13         |
+---------------+
```

```mysql
select @pricehigh, @pricelow, @priceaverage;
```

```mysql
+------------+-----------+---------------+
| @pricehigh | @pricelow | @priceaverage |
+------------+-----------+---------------+
| 55.00      | 2.50      | 16.13         |
+------------+-----------+---------------+
```

```mysql
create procedure ordertotal
(
    in onumber int,
    out ototal decimal(8,2)
)
begin
	select sum(item_price * quantity)
	from orderitems
	where order_num = onumber
	into ototal;
end;
```

```mysql
call ordertotal(20005, @total);
```

```mysql
select @total;
```

```mysql
+--------+
| @total |
+--------+
| 149.87 |
+--------+
```

```mysql
call ordertotal(20009, @total);
select @total;
```

```mysql
+--------+
| @total |
+--------+
| 38.47  |
+--------+
```

#### 23.3.5 建立智能存储过程

```mysql
# name: ordertotal
# parameters: onumber = order number
# 			  taxable = 0 if not taxable, 1 if taxable
#			  ototal  = order total variable

create procedure ordertotal
(
    in onumber int,
    in taxable boolean,
    out ototal decimal(8,2)
) comment 'Obtain order total, optionally adding tax'
begin

	# declare variable for total
	declare total decimal(8,2);
	# declare tax percentage
	declare taxrate int default 6;
	
	# get the order total
	select sum(item_price*quantity)
	from orderitems
	where order_num = onumber
	into total;
	
	# is this taxable?
	if taxable then
		# yes, so add taxrate to the total
		select total+(total/100*taxrate) into total;
	end if;
	# and finally, save to out variable
	select total into ototal;
end;
```

```mysql
call ordertotal(20005, 0, @total);
select @total;
```

```mysql
+--------+
| @total |
+--------+
| 149.87 |
+--------+
```

```mysql
call ordertotal(20005, 1, @total);
select @total;
```

```mysql
+--------+
| @total |
+--------+
| 158.86 |
+--------+
```

#### 23.3.6 检查存储过程

```mysql
show create procedure ordertotal;
```

## 第二十四章

### 24.1 游标

### 24.2 使用游标

#### 24.2.1 创建游标 ==(declare)==

```mysql
create procedure processorders()
begin
	declare ordernumbers cursor
	for
	select order_num from orders;
end;
```

#### 24.2.2 打开和关闭游标 ==(open,	close)==

```mysql
# 打开游标
open ordernumbers;
```

```mysql
# 关闭游标
close ordernumbers;
```

```mysql
create procedure processorders()
begin
	# declare the cursor
	declare ordernumbers cursor
	for
	select order_num from orders;
	# open the cursor
	open ordernumbers;
	# close the cursor
	close ordernumbers;
end;
```

#### 24.2.3 使用游标数据

```mysql
# 从游标中检索单个行（第一行）
create procedure processorders()
begin
	# declare local variables
	declare o int;
	# declare the cursor
	declare ordernumbers cursor
	for
	select order_num from orders;
	# open the cursor
	open ordernumbers;
	# get order number
	fetch ordernumbers into o;
	close ordernumbers;
end;
```

```mysql
# 循环检索数据，从第一行到最后一行
create procedure processorders()
begin
	# declare local variables
	declare done boolean default 0;
	declare o int;
	# declare the cursor
	declare ordernumbers cursor
	for
	select order_num from orders;
	# declare continue handler
	declare continue handler for sqlstate '02000' set done=1;
	# open the cursor
	open ordernumbers;
	# loop through all rows
	repeat
		# get order number
		fetch ordernumbers into o;
	# end of loop
	until done end repeat;
	# close the cursor
	close ordernumbers;
end;
```

```mysql
create procedure processorders()
begin
	# declare local variables
	declare done boolean deafault 0;
	declare o int;
	declardecimal(8, 2);
	# declare the cursor
	declare ordernumbers cursor
	for
	select order_num from orders;
	# declare continue handler
	declare continue handler for sqlstate '02000' set done = 1;
	# create a table to store the results
	create table if not exists ordertotals
		(order_num int, total decimal(8, 2));
	# open the cursor
	open ordernumbers;
	# loop through all rows
	repeat
		# get order number
		fetch ordernumbers into o;
		# get the total for this order
		call ordertotal(o, 1, t);
		# insert order and total into ordertotals
		insert into ordertotals(order_num, total)
		values(o, t);
	# end of loop
    until done end repeat;
	# close the cursor
	close ordernumbers;
end;
```

