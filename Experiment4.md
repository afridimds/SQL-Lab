# SQL Lab - Experiment 1
## Aim: To study and perform various SQL Operations on a table.
## Question 1 : Display the list of employees who have joined the company before 30th June 80 or after 31st Dec 81.
### Query : 
```sql
SELECT ENAME,HIREDATE FROM  EMPLOYEE WHERE HIREDATE>'1981-12-31' OR HIREDATE<'1980-01-30';
```
### Output :
```sql
+--------+------------+
| ENAME  | HIREDATE   |
+--------+------------+
| SCOTT  | 1982-12-09 |
| ADAMS  | 1983-01-12 |
| MILLER | 1982-01-23 |
+--------+------------+
```
## Question 2 : Display the names of employees whose names have second alphabet A in their names.
### Query : 
```sql   
 SELECT ENAME FROM  EMPLOYEE WHERE ENAME LIKE '_A%';
```
### Output :
```sql
+--------+
| ENAME  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+
```
## Question 3 : Display the names of employees whose name is exactly five characters in length
### Query :
```sql   
SELECT ENAME FROM  EMPLOYEE WHERE ENAME LIKE '_____';
```
### Output :
```sql
+-------+
| ENAME |
+-------+
| SMITH |
| ALLEN |
| JONES |
| BLAKE |
| CLARK |
| SCOTT |
| ADAMS |
| JAMES |
+-------+
```
## Question 4 : Display the names of employees whose names have second alphabet A in their names.
### Query :
```sql   
SELECT ENAME FROM  EMPLOYEE WHERE ENAME LIKE '%A_';
```
### Output :
```sql
Empty set (0.002 sec)
```
## Question 5 : Display the names of employees who are not working as salesman or clerk or analyst.
### Query :
```sql   
SELECT ENAME,JOB  FROM EMPLOYEE WHERE JOB NOT IN ('CLERK','SELESMAN','ANALYST');
```
### Output :
```sql
+-------+-----------+
| ENAME | JOB       |
+-------+-----------+
| JONES | MANAGER   |
| BLAKE | MANAGER   |
| CLARK | MANAGER   |
| KING  | PRESIDENT |
+-------+-----------+
```
## Question 6 : Display the name of the employee along with their annual salary (sal*12). The name of the employee earning highest salary should appear first.
### Query :
```sql   
 SELECT ENAME , (SAL*12) AS ANNUAL_SAL FROM EMPLOYEE ORDER BY SAL DESC;
```
### Output :
```sql
+--------+------------+
| ENAME  | ANNUAL_SAL |
+--------+------------+
| KING   |      66000 |
| SCOTT  |      39600 |
| FORD   |      39600 |
| JONES  |      39276 |
| BLAKE  |      37620 |
| CLARK  |      32340 |
| ALLEN  |      19200 |
| TURNER |      18000 |
| MILLER |      17160 |
| MARTIN |      15000 |
| WARD   |      15000 |
| ADAMS  |      14520 |
| JAMES  |      12540 |
| SMITH  |      10560 |
+--------+------------+
```
## Question 7 : Display name, sal, hra, pf, da, totalsal for each employee. The output should be in the order of total sal, hra 15% of sal, da 10% of sal, pf 5% of sal. Total salary will be (sal*hra*da)-pf.
### Query :
```sql   
SELECT ENAME, SAL, SAL*0.15 AS HRA, SAL*0.10 AS DA, SAL*0.05 AS PF, (SAL+SAL*0.15+SAL*0.10-SAL*0.05) AS TOTAL_SAL FROM EMPLOYEE ORDER BY TOTAL_SAL;
```
### Output :
```sql
+--------+------+--------+--------+--------+-----------+
| ENAME  | SAL  | HRA    | DA     | PF     | TOTAL_SAL |
+--------+------+--------+--------+--------+-----------+
| SMITH  |  800 | 120.00 |  80.00 |  40.00 |    960.00 |
| JAMES  |  950 | 142.50 |  95.00 |  47.50 |   1140.00 |
| ADAMS  | 1100 | 165.00 | 110.00 |  55.00 |   1320.00 |
| WARD   | 1250 | 187.50 | 125.00 |  62.50 |   1500.00 |
| MARTIN | 1250 | 187.50 | 125.00 |  62.50 |   1500.00 |
| MILLER | 1300 | 195.00 | 130.00 |  65.00 |   1560.00 |
| TURNER | 1500 | 225.00 | 150.00 |  75.00 |   1800.00 |
| ALLEN  | 1600 | 240.00 | 160.00 |  80.00 |   1920.00 |
| CLARK  | 2450 | 367.50 | 245.00 | 122.50 |   2940.00 |
| BLAKE  | 2850 | 427.50 | 285.00 | 142.50 |   3420.00 |
| JONES  | 2975 | 446.25 | 297.50 | 148.75 |   3570.00 |
| FORD   | 3000 | 450.00 | 300.00 | 150.00 |   3600.00 |
| SCOTT  | 3000 | 450.00 | 300.00 | 150.00 |   3600.00 |
| KING   | 5000 | 750.00 | 500.00 | 250.00 |   6000.00 |
+--------+------+--------+--------+--------+-----------+
```
## Question 8 : Update the salary of each employee by 10% increment who are not eligible for commission.
### Query :
```sql   
UPDATE EMPLOYEE SET SAL=SAL*1.10 WHERE COMM IS NULL;
SELECT*FROM EMPLOYEE;
```
### Output :
```sql
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  880 | NULL |     20 |
|  7499 | ALLEN  | SELESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SELESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 3273 | NULL |     20 |
|  7654 | MARTIN | SELESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-03-01 | 3135 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2695 | NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3300 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5500 | NULL |     20 |
|  7844 | TURNER | SELESMAN  | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1210 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 | 1045 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3300 | NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1430 | NULL |     10 |
+-------+--------+-----------+------+------------+------+------+--------+
```
## Question 9 : Display those employees whose salary is more than 3000 after giving 20% increment.
### Query :
```sql 
SELECT ENAME,SAL*1.20 AS SAL_INC_BY_20PER FROM EMPLOYEE WHERE SAL*1.20>3000;
```
### Output :
```sql
+-------+------------------+
| ENAME | SAL_INC_BY_20PER |
+-------+------------------+
| JONES |          3927.60 |
| BLAKE |          3762.00 |
| CLARK |          3234.00 |
| SCOTT |          3960.00 |
| KING  |          6600.00 |
| FORD  |          3960.00 |
+-------+------------------+
```
## Question 10 : Display those employees whose salary contains atleast 3 digits.
### Query :
```sql   
SELECT ENAME,SAL FROM EMPLOYEE WHERE SAL>99;
```
### Output :
```sql
+--------+------+
| ENAME  | SAL  |
+--------+------+
| SMITH  |  880 |
| ALLEN  | 1600 |
| WARD   | 1250 |
| JONES  | 3273 |
| MARTIN | 1250 |
| BLAKE  | 3135 |
| CLARK  | 2695 |
| SCOTT  | 3300 |
| KING   | 5500 |
| TURNER | 1500 |
| ADAMS  | 1210 |
| JAMES  | 1045 |
| FORD   | 3300 |
| MILLER | 1430 |
+--------+------+
```