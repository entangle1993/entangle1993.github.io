# INNER JOIN  
在表中存在至少一个匹配时，INNER JOIN 关键字返回行。(=JOIN)
# SQL LEFT JOIN 关键字  
LEFT JOIN 关键字会从左表 (table_name1) 那里返回所有的行，即使在右表 (table_name2) 中没有匹配的行。  
# case  
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
`select emp_no,salary from salaries group by emp_no having min(from_date) order by emp_no DESC`