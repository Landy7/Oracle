# 实验一：分析SQL执行计划，执行SQL语句的优化指导

## 实验内容:
- 对Oracle12c中的HR人力资源管理系统中的表进行查询与分析。
- 首先运行和分析教材中的样例：本训练任务目的是查询两个部门('IT'和'Sales')的部门总人数和平均工资，以下两个查询的结果是一样的。但效率不相同。
- 设计自己的查询语句，并作相应的分析，查询语句不能太简单。

## 对比这两个查询语句：

查询1：
```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
```
查询2：
```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
HAVING d.department_name in ('IT'，'Sales');
```
第一个查询语句得到的优化指导结果：
![image](https://github.com/Landy7/Oracle/blob/master/%E5%AE%9E%E9%AA%8C111111111111.png)

第二个查询语句得到的优化指导结果：
![image](https://github.com/Landy7/Oracle/blob/master/%E5%AE%9E%E9%AA%8C1-222.png)

所以，从cost方面对比得到：虽然第一条查询语句比第二条查询语句多了两个步骤，但所花的时间总体比第二个查询语句少。
## 第二条优于第一条。




