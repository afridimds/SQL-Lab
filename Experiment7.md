# SQL Lab - Experiment 7
## Aim: To perform various SQL queries for data retrieval, aggregation, formatting, and analysis on an employee database. The objective is to Calculate date-based values such as remaining days in a year and last Sunday of a month, Perform salary analysis including highest, lowest, and difference, Filter records based on conditions (e.g., commission > 25% of salary), Format output (e.g., salary in dollar format), Use aggregate functions like COUNT, SUM, MAX, MIN, Apply grouping using GROUP BY for departments and job roles, Generate summary reports and matrix-style outputs
## Question 1 : Compute the no. of days remaining in this year.
### Query :
```sql
SELECT DATEDIFF(CONCAT(YEAR(CURDATE()),"-12-31"),CURDATE()) AS REMAINING_DAYS;
```
### Output :
```sql
+----------------+
| REMAINING_DAYS |
+----------------+
|            263 |
+----------------+
```
## Question 2 : Find the highest and lowest salaries and the difference between of them.
### Query :
```sql
SELECT MAX(SAL) AS MAX_SAL, MIN(SAL) AS MIN_SAL, MAX(SAL) - MIN(SAL) AS SAL_DIFF FROM EMPLOYEE;
```
### Output :
```sql
+---------+---------+----------+
| MAX_SAL | MIN_SAL | SAL_DIFF |
+---------+---------+----------+
|    5500 |     880 |     4620 |
+---------+---------+----------+
```
## Question 3 : List employee whose commission is greater than 25 % of their salaries.
### Query :
```sql
SELECT * FROM EMPLOYEE WHERE COMM > (0.25 * SAL);
```
### Output :
```sql
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
+-------+--------+----------+------+------------+------+------+--------+
```
## Question 4 : Make a query that displays salary in dollar format.
### Query :
```sql
SELECT CONCAT("$", SAL) AS SAL_IN_DOLLAR FROM EMPLOYEE;
```
### Output :
```sql
+---------------+
| SAL_IN_DOLLAR |
+---------------+
| $880          |
| $1600         |
| $1250         |
| $3273         |
| $1250         |
| $3135         |
| $2695         |
| $3300         |
| $5500         |
| $1500         |
| $1210         |
| $1045         |
| $3300         |
| $1430         |
+---------------+
```
## Question 5 : Create a matrix query to display the job, the salary for that job based on department number, and the total salary for that job for all departments, giving each column an appropriate heading.
### Query :
```sql
SELECT JOB, SUM(CASE DEPTNO WHEN 10 THEN SAL ELSE 0 END) AS DEPT10,
      SUM(CASE DEPTNO WHEN 20 THEN SAL ELSE 0 END) AS DEPT20,
      SUM(CASE DEPTNO WHEN 30 THEN SAL ELSE 0 END) AS DEPT30,
      SUM(CASE DEPTNO WHEN 40 THEN SAL ELSE 0 END) AS DEPT40,
      SUM(SAL) AS TOTAL_SAL FROM EMPLOYEE GROUP BY JOB;
```
### Output :
```sql
+-----------+--------+--------+--------+--------+-----------+
| JOB       | DEPT10 | DEPT20 | DEPT30 | DEPT40 | TOTAL_SAL |
+-----------+--------+--------+--------+--------+-----------+
| ANALYST   |      0 |   3300 |      0 |   3300 |      6600 |
| CLERK     |   1430 |   2090 |   1045 |      0 |      4565 |
| MANAGER   |      0 |   5968 |   3135 |      0 |      9103 |
| PRESIDENT |      0 |   5500 |      0 |      0 |      5500 |
| SALESMAN  |      0 |      0 |   5600 |      0 |      5600 |
+-----------+--------+--------+--------+--------+-----------+
```
## Question 6 : Query that will display the total no of employees, and of that total the number who were hired in 1980,1981,1982 and 1983. Give appropriate column heading.
### Query :
```sql
SELECT COUNT(*), SUM(CASE YEAR(HIREDATE) WHEN "1980" THEN 1 ELSE 0 END) AS HIRED_IN1980,
      SUM(CASE YEAR(HIREDATE) WHEN "1981" THEN 1 ELSE 0 END) AS HIRED_IN1981,
      SUM(CASE YEAR(HIREDATE) WHEN "1982" THEN 1 ELSE 0 END) AS HIRED_IN1982,
      SUM(CASE YEAR(HIREDATE) WHEN "1983" THEN 1 ELSE 0 END) AS HIRED_IN1983
      FROM EMPLOYEE;
```
### Output :
```sql
+----------+--------------+--------------+--------------+--------------+
| COUNT(*) | HIRED_IN1980 | HIRED_IN1981 | HIRED_IN1982 | HIRED_IN1983 |
+----------+--------------+--------------+--------------+--------------+
|       14 |            1 |           10 |            2 |            1 |
+----------+--------------+--------------+--------------+--------------+
```
## Question 7 : Query to get the last Sunday of Any Month.
### Query :
```sql
SELECT DATE_SUB(LAST_DAY(CURDATE()),
      INTERVAL(WEEKDAY(LAST_DAY(CURDATE())) +1) % 7 DAY) AS LAST_SUNDAY;
```
### Output :
```sql
+-------------+
| LAST_SUNDAY |
+-------------+
| 2026-04-26  |
+-------------+
```
## Question 8 : Display department numbers and total number of employees working in each department.
### Query :
```sql
SELECT DEPTNO AS DEPARTMENT_NUMBER,
      COUNT(*) AS Total_Employees FROM EMPLOYEE GROUP BY DEPTNO;
```
### Output :
```sql
+-------------------+-----------------+
| DEPARTMENT_NUMBER | Total_Employees |
+-------------------+-----------------+
|                10 |               1 |
|                20 |               6 |
|                30 |               6 |
|                40 |               1 |
+-------------------+-----------------+
```
## Question 9 : Display the various jobs and total number of employees within each job group.
### Query :
```sql
SELECT JOB AS Job_Title,
      COUNT(*) AS Total_Employees FROM EMPLOYEE GROUP BY JOB;
```
### Output :
```sql
+-----------+-----------------+
| Job_Title | Total_Employees |
+-----------+-----------------+
| ANALYST   |               2 |
| CLERK     |               4 |
| MANAGER   |               3 |
| PRESIDENT |               1 |
| SALESMAN  |               4 |
+-----------+-----------------+
```
## Question 10 : Display the department numbers and total salary for each department.
### Query :
```sql
SELECT DEPTNO AS Department_Number,
      SUM(SAL) AS Total_Salary FROM Employee GROUP BY DEPTNO;
```
### Output :
```sql
+-------------------+--------------+
| Department_Number | Total_Salary |
+-------------------+--------------+
|                10 |         1430 |
|                20 |        16858 |
|                30 |         9780 |
|                40 |         3300 |
+-------------------+--------------+
```