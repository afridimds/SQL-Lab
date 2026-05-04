# SQL Lab - Experiment 12
## Aim: To write and execute SQL queries using subqueries, aggregate functions, relational operators, and conditional clauses in order to retrieve, delete, and analyze data from relational tables such as EMP, DEPT, and SALGRADE.
## Question 1 : Display those employees whose salary is less than his manager but more than salary of any other managers.
### Query :
```sql
SELECT e.ename, e.sal FROM employee e
    JOIN employee m ON e.mgr = m.empno
    WHERE e.sal < m.sal AND e.sal > ANY (SELECT 
    sal FROM  EMPLOYEE WHERE job = 'MANAGER');
```
### Output :
```sql
Empty set (0.001 sec)
```
## Question 2 : Find out the number of employees whose salary is greater than their manager salary?
### Query :
```sql
SELECT COUNT(*) AS total_employees
    FROM  EMPLOYEE e JOIN  EMPLOYEE m ON
    e.mgr = m.empno WHERE e.sal > m.sal;
```
### Output :
```sql
+-----------------+
| total_employees |
+-----------------+
|               2 |
+-----------------+
```
## Question 3 : Display those managers who are not working under president but they are working under any other manager?
### Query :
```sql
SELECT e.ename FROM  EMPLOYEE e
    WHERE e.job = 'MANAGER' AND e.mgr IS NOT NULL
    AND e.mgr <> (SELECT empno FROM  EMPLOYEE 
    WHERE job = 'PRESIDENT');
```
### Output :
```sql
Empty set (0.001 sec)
```
## Question 4 : Delete those department where no employee working?
### Query :
```sql
DELETE FROM department WHERE deptno NOT IN 
    (SELECT DISTINCT deptno FROM employee);
    select * from department;
```
### Output :
```sql
+--------+------------+-----------+
| Deptno | Dname      | location  |
+--------+------------+-----------+
|     20 | ACCOUNTING | MUMBAI    |
|     40 | OPERATIONS | BANGALORE |
+--------+------------+-----------+
```
## Question 5 : Delete those records from  EMPLOYEE table whose deptno not available in dept table?
### Query :
```sql
DELETE FROM employee WHERE deptno NOT IN 
    (SELECT deptno FROM department);
```
### Output :
```sql
Query OK, 0 rows affected (0.001 sec)
```
## Question 6 : Display those earners whose salary is out of the grade available in sal grade table?
### Query :
```sql
SELECT e.ename, e.sal FROM  EMPLOYEE e
    WHERE NOT EXISTS (SELECT 1 FROM salgrade s
    WHERE e.sal BETWEEN s.losal AND s.hisal);
```
### Output :
```sql
Empty set (0.001 sec)
```
## Question 7 : Display employee name, sal, comm. And whose net pay is greater than any other in the company?
### Query :
```sql
SELECT ename, sal, comm, (sal + IFNULL(comm,0)) AS net_pay
    FROM employee WHERE (sal + IFNULL(comm,0)) >= ALL (
    SELECT (sal + IFNULL(comm,0)) FROM employee);
```
### Output :
```sql
+-------+---------+------+---------+
| ename | sal     | comm | net_pay |
+-------+---------+------+---------+
| KING  | 5000.00 | NULL | 5000.00 |
+-------+---------+------+---------+
```
## Question 8 : Display those employees who are working in sales or research?
### Query :
```sql
SELECT e.ename FROM  EMPLOYEE e
    JOIN department d ON e.deptno = d.deptno
    WHERE d.dname IN ('SALES', 'RESEARCH');
```
### Output :
```sql
Empty set (0.001 sec)
```
## Question 9 : Display the grade of jones?
### Query :
```sql
SELECT s.grade FROM  EMPLOYEE e
    JOIN salgrade s ON e.sal BETWEEN 
    s.losal AND s.hisal WHERE e.ename = 'JONES';
```
### Output :
```sql
+-------+
| grade |
+-------+
| D     |
+-------+
```
## Question 10 : Display the department name the no of characters of which is equal to no of employees in any other department?
### Query :
```sql
SELECT d.dname FROM DEPARTMENT d WHERE 
    LENGTH(d.dname) IN (SELECT COUNT(*)
    FROM EMPLOYEE GROUP BY deptno);
```
### Output :
```sql
Empty set (0.001 sec)
```