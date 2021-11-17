### Task 01.  
1. 数据库配置相关(WSL, 非docker)  
	- 需要修改配置, 使外网可以链接  
	bind-address = 127.0.0.1  *# /etc/mysql/my.cnf*   
	- 配置远程账户\&重启  
    - 修改默认编码  

2. DDL  
	包含CREATE, DROP, ALTER, TRUNCATE  
	*TRUNCATE清空表中数据, 相比Drop/Delete, 速度最快*

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
