# SQL Lab - Experiment 5
## Aim: To study and implement SQL aggregate functions and string functions on the Employee table in order to retrieve summarized salary information and manipulate employee name data using various built-in SQL functions.
## Question 1 : Display the total number of employee working in the company.
### Query :
```sql
SELECT COUNT(*) AS total_employees FROM employee;
```
### Output :
```sql
+-----------------+
| total_employees |
+-----------------+
|              14 |
+-----------------+
```
## Question 2 : Display the total salary being paid to all employees.
### Query :
```sql
SELECT SUM(sal) AS total_salary FROM employee;
```
### Output :
```sql
+--------------+
| total_salary |
+--------------+
|        31368 |
+--------------+
```
## Question 3 : Display the maximum salary from employee table.
### Query :
```sql
SELECT MAX(sal) AS max_salary FROM employee;
```
### Output :
```sql
+------------+
| max_salary |
+------------+
|       5500 |
+------------+
```
## Question 4 : Display the minimum salary from employee table.
### Query :
```sql
SELECT MIN(sal) AS min_salary FROM employee;
```
### Output :
```sql
+------------+
| min_salary |
+------------+
|        880 |
+------------+
```
## Question 5 : Display the average salary from employee table.
### Query :
```sql
SELECT AVG(sal) AS avg_salary FROM employee;
```
### Output :
```sql
+------------+
| avg_salary |
+------------+
|  2240.5714 |
+------------+
```
## Question 6 : Display the maximum salary being paid to clerk.
### Query :
```sql
SELECT MAX(sal) AS max_clerk_salary FROM employee WHERE job = 'CLERK';
```
### Output :
```sql
+------------------+
| max_clerk_salary |
+------------------+
|             1430 |
+------------------+
```
## Question 7 : Display the maximum salary being paid in dept no 20.
### Query :
```sql
SELECT MAX(sal) AS max_salary_dept20 FROM employee WHERE deptno = 20;
```
### Output :
```sql
+-------------------+
| max_salary_dept20 |
+-------------------+
|              5500 |
+-------------------+
```
## Question 8 : Display the minimum salary paid to any salesman.
### Query :
```sql
SELECT MIN(sal) AS min_salesman_salary FROM employee WHERE job = 'SALESMAN';
```
### Output :
```sql
+---------------------+
| min_salesman_salary |
+---------------------+
|                1250 |
+---------------------+
```
## Question 9 : Display the average salary drawn by managers.
### Query :
```sql
SELECT AVG(sal) AS avg_manager_salary FROM employee WHERE job = 'MANAGER';
```
### Output :
```sql
+--------------------+
| avg_manager_salary |
+--------------------+
|          3034.3333 |
+--------------------+
```
## Question 10 : Display the total salary drawn by analyst working in dept no 40.
### Query :
```sql
SELECT SUM(sal) AS total_analyst_salary_dept40 FROM employee WHERE job = 'ANALYST' AND deptno = 40;
```
### Output :
```sql
+-----------------------------+
| total_analyst_salary_dept40 |
+-----------------------------+
|                        3300 |
+-----------------------------+
```
## Question 11 : Display the names of the employee in Uppercase.
### Query :
```sql
SELECT UPPER(ename) AS employee_name_upper FROM employee;
```
### Output :
```sql
+---------------------+
| employee_name_upper |
+---------------------+
| SMITH               |
| ALLEN               |
| WARD                |
| JONES               |
| MARTIN              |
| BLAKE               |
| CLARK               |
| SCOTT               |
| KING                |
| TURNER              |
| ADAMS               |
| JAMES               |
| FORD                |
| MILLER              |
+---------------------+
```
## Question 12 : Display the names of the employee in Lowercase.
### Query :
```sql
SELECT LOWER(ename) AS employee_name_lower FROM employee;
```
### Output :
```sql
+---------------------+
| employee_name_lower |
+---------------------+
| smith               |
| allen               |
| ward                |
| jones               |
| martin              |
| blake               |
| clark               |
| scott               |
| king                |
| turner              |
| adams               |
| james               |
| ford                |
| miller              |
+---------------------+
```
## Question 13 : Display the names of the employee in Proper case.
### Query :
```sql
SELECT CONCAT(UPPER(LEFT(ename,1)), LOWER(SUBSTRING(ename,2))) AS employee_name_proper FROM employee;
```
### Output :
```sql
+----------------------+
| employee_name_proper |
+----------------------+
| Smith                |
| Allen                |
| Ward                 |
| Jones                |
| Martin               |
| Blake                |
| Clark                |
| Scott                |
| King                 |
| Turner               |
| Adams                |
| James                |
| Ford                 |
| Miller               |
+----------------------+
```
## Question 14 : Display the length of Your name using appropriate function.
### Query :
```sql
SELECT LENGTH('Shadab') AS name_length FROM dual;
```
### Output :
```sql
+-------------+
| name_length |
+-------------+
|           6 |
+-------------+
```
## Question 15 : Display the length of all the employee names..
### Query :
```sql
SELECT ename, LENGTH(ename) AS name_length FROM employee;
```
### Output :
```sql
+--------+-------------+
| ename  | name_length |
+--------+-------------+
| SMITH  |           5 |
| ALLEN  |           5 |
| WARD   |           4 |
| JONES  |           5 |
| MARTIN |           6 |
| BLAKE  |           5 |
| CLARK  |           5 |
| SCOTT  |           5 |
| KING   |           4 |
| TURNER |           6 |
| ADAMS  |           5 |
| JAMES  |           5 |
| FORD   |           4 |
| MILLER |           6 |
+--------+-------------+
```