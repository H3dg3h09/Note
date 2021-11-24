
https://tianchi.aliyun.com/specials/promotion/aicampsql

### Task 01.  
1. 数据库配置相关(WSL, 非docker)  
	- 需要修改配置, 使外网可以链接  
	bind-address = 127.0.0.1  *# /etc/mysql/my.cnf*   
	- 配置远程账户\&重启  
    - 修改默认编码  

2. DDL  
	包含CREATE, DROP, ALTER, TRUNCATE  
	*TRUNCATE清空表中数据, 相比Drop/Delete, 速度最快*

---  

3. DML(Data Manipulation Language)  
	- 比较需要注意的是联合查询/嵌套查询的时候, 表与表的关系, 有时候出现同时操作同一个表就会出问题.  
	- 执行顺序: FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY  
	1. LEFT JOIN, RIGHT JOIN, INNER JOIN -- ON -- AND  
	2. GOURP BY  -- HAVING   
	SELECT无法选取GROUP BY后的某一个值, 因为并不知道该对应谁.  
	NULL是单独的一个分类.  
	由于SELECT在GOURP BY之后执行, 所以GROUP BY中不能使用alias.  
	如果要有限制, 使用HAVING而不是WHERE.    
	3. ORDER BY  
	4. other  
		1. DISTINCT 可去重结果   
		> **DISTINCT和GROUP BY的效率差异?**
		2. NULL  
		  对NULL的判断不可使用>=<, 用IS以及IS NOT    
		>   **ORDER BY 对NULL排序?**  
		3. 连接字符串用CONCAT    
		4. 不等于是\<\>  
		5. COUNT(\*)会得到包含NULL的数据行, COUNT(\<列名\>)会排除NULL    
			COUNT(DISTINCT \*\*\*)可以用来统计种类  
4. VIEW  
	1. VIEW是虚拟表, 内容为SELECT TABLE的结果。 从VIEW中查询数据可以保证数据的安全性(有权限才能修改数据), 也可以加快效率, 存放一些常用的查询语句.  
	2. 也可以对VIEW进行WHERE操作, 结果为VIEW自身所查询的结果中再去WHERE.  
	3. 有些DML不可以放在VIEW中进行保存, 因为VIEW也是TABLE的一种, 他们都有一个性质:**数据是无序的**.  
	4. 所以这些条件存入VIEW是无用的, 包含但不限于: SUM, MIN, MAX, COUNT, GROUP BY, HAVING, ORDER BY, UNION, DISINCT, FROM子句中和包含多个表.  

5. FUNCTION  
	- SUBSTRING (Split), index0 = 1.  
	- BETWEEN 是闭区间.  
	- NULL只能被IS NULL, IS NOT NULL判断, 无法被别的函数判断, 例如IN, NOT IN.  

6. CASE  
	> LIKE \<switch\>   

	- 使用场景: 实现行列转换.   
7. OLAP(Online AnalyticalPorocessing)  
	> MYSQL 8.0以上才有   
	- 当不指定PARTITION时,聚合函数SUM, AVG等在使用时, 计算的是累积到当前行的所有数据的聚合.  
	- Frame  
	  - PRECEDING(之前), 将框架指定为"截止到之前N行", 加上自身行.  
	  - FOLLOWING(之后), 将框架指定为	"截止到之后N行", 加上自身行.  
	  - BETWEEN 1 PRECEDING AND 1 FOLLOWING, 将框架指定为"之前1行 + 之后1行", 加上自身行.  
	  - OVER中的ORDER BY并不会影响最终结果的排序, 他只是用来决定窗口函数按何种顺序计算.  
8. GROUPING 扩展  
	- ROLLUP 计算分类的合计
	```MYSQL
		SELECT `type`, date, SUM(price) AS `sum` FROM Table GROUP BY `type`, `date` WITH ROLLUP

		#--------------------------
		#|  type |   date   | sum |
		#|-------------------------
		#| type1 |2020-01-01| 1000|
		#|-------------------------
		#| type1 |2020-01-05| 5500|
		#|-------------------------
		#| type1 |   null   | 6500|  # ROLLUP
		#--------------------------
		#| type2 |2020-01-01| 2300|
		#|-------------------------
		
	```








