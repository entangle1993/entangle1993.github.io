# SQL注入  
SQL注入，就是通过把SQL命令插入到Web表单递交或输入域名或页面请求的查询字符串，最终达到欺骗服务器执行恶意的SQL命令，比如先前的很多影视网站泄露VIP会员密码大多就是通过WEB表单递交查询字符暴出的，这类表单特别容易受到SQL注入式攻击．

# 关键字  
## INNER JOIN  
在表中存在至少一个匹配时，INNER JOIN 关键字返回行。(=JOIN)
## SQL LEFT JOIN 关键字  
LEFT JOIN 关键字会从左表 (table_name1) 那里返回所有的行，即使在右表 (table_name2) 中没有匹配的行。  
## case  
查找所有员工入职时候的薪水情况，给出emp_no以及salary， 并按照emp_no进行逆序  
CREATE TABLE `employees` (  
`emp_no` int(11) NOT NULL,  
`birth_date` date NOT NULL,  
`first_name` varchar(14) NOT NULL,    
`last_name` varchar(16) NOT NULL,  
`gender` char(1) NOT NULL,  
`hire_date` date NOT NULL,  
PRIMARY KEY (`emp_no`));  

CREATE TABLE `salaries` (  
`emp_no` int(11) NOT NULL,  
`salary` int(11) NOT NULL,  
`from_date` date NOT NULL,  
`to_date` date NOT NULL,  
PRIMARY KEY (`emp_no`,`from_date`));    
* 方法1  
找出最小日期也可以说是最早的日期（ min（from_date）），这个最小日期就是员工刚入职时候的日期，对应的工资就是入职时候的工资  
`select emp_no,salary from salaries group by emp_no having min(from_date) order by emp_no DESC`  
* 方法2
直接用逗号并列查询两张表  
`SELECT e.emp_no, s.salary FROM employees AS e, salaries AS s  
WHERE e.emp_no = s.emp_no AND e.hire_date = s.from_date  
ORDER BY e.emp_no DESC`  

查找薪水涨幅超过15次的员工号emp_no以及其对应的涨幅次数t  
* 分析：
1、用COUNT()函数和GROUP BY语句可以统计同一emp_no值的记录条数  
2、根据题意，输出的涨幅次数为t，故用AS语句将COUNT(emp_no)的值转换为t  
3、由于COUNT()函数不可用于WHERE语句中，故使用HAVING语句来限定t>15的条件  
`select emp_no, count(emp_no) as t FROM salaries GROUP BY emp_no HAVING t > 15`

from https://www.nowcoder.com/ta/sql
