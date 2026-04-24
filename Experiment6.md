# SQL Lab - Experiment 6
## Aim: To study and implement SQL date functions, conversion functions, and DECODE function in order to perform date manipulations, formatting, conditional display, and calculations on employee data.
## Question 1 : Display empno, ename, deptno from employee table. Instead of display department numbers display the related department name.
### Query : 
```sql 
SELECT EMPNO,ENAME, CASE DEPTNO
        WHEN 10 THEN 'RESEARCH'
        WHEN 20 THEN 'ACCOUNTING'
        WHEN 30 THEN 'SALES'
        WHEN 40 THEN 'OPERATIONS'
        END AS DNAME FROM EMPLOYEE;
```
### Output :
```sql
+-------+--------+------------+
| EMPNO | ENAME  | DNAME      |
+-------+--------+------------+
|  7369 | SMITH  | ACCOUNTING |
|  7499 | ALLEN  | SALES      |
|  7521 | WARD   | SALES      |
|  7566 | JONES  | ACCOUNTING |
|  7654 | MARTIN | SALES      |
|  7698 | BLAKE  | SALES      |
|  7782 | CLARK  | ACCOUNTING |
|  7788 | SCOTT  | OPERATIONS |
|  7839 | KING   | ACCOUNTING |
|  7844 | TURNER | SALES      |
|  7876 | ADAMS  | ACCOUNTING |
|  7900 | JAMES  | SALES      |
|  7902 | FORD   | ACCOUNTING |
|  7934 | MILLER | RESEARCH   |
+-------+--------+------------+
```
## Question 2 : Display your age in days.
### Query : 
```sql
SELECT DATEDIFF(CURDATE(),'2004-01-02');
```
### Output :
```sql
+----------------------------------+
| DATEDIFF(CURDATE(),'2004-01-02') |
+----------------------------------+
|                             8090 |
+----------------------------------+
```
## Question 3 : Display your age in months.
### Query :
```sql
SELECT TIMESTAMPDIFF(MONTH,'2004-01-02',CURDATE());
```
### Output :
```sql
+---------------------------------------------+
| TIMESTAMPDIFF(MONTH,'2004-01-02',CURDATE()) |
+---------------------------------------------+
|                                         265 |
+---------------------------------------------+
```
## Question 4 : Display the current date in the given format :- 15th August Friday Nineteen Ninety-Seven.
### Query :
```sql
SELECT DATE_FORMAT(CURDATE(),'%D %M %W %Y');
```
### Output :
```sql
+--------------------------------------+
| DATE_FORMAT(CURDATE(),'%D %M %W %Y') |
+--------------------------------------+
| 25th February Wednesday 2026         |
+--------------------------------------+
```
## Question 5 + 6 : Display the following output for each row from employee table in the given format :- Scott has joined the company on Wednesday 13th August Nineteen Ninety.
### Query :
```sql
SELECT CONCAT(ENAME, ' has joined the company on ',DATE_FORMAT(HIREDATE,'%W %D %M %Y')) AS DETAIL FROM EMPLOYEE;
```
### Output :
```sql
+--------------------------------------------------------------+
| DETAIL                                                       |
+--------------------------------------------------------------+
| SMITH has joined the company on Wednesday 17th December 1980 |
| ALLEN has joined the company on Friday 20th February 1981    |
| WARD has joined the company on Sunday 22nd February 1981     |
| JONES has joined the company on Thursday 2nd April 1981      |
| MARTIN has joined the company on Monday 28th September 1981  |
| BLAKE has joined the company on Friday 1st May 1981          |
| CLARK has joined the company on Tuesday 9th June 1981        |
| SCOTT has joined the company on Thursday 9th December 1982   |
| KING has joined the company on Tuesday 17th November 1981    |
| TURNER has joined the company on Tuesday 8th September 1981  |
| ADAMS has joined the company on Wednesday 12th January 1983  |
| JAMES has joined the company on Thursday 3rd December 1981   |
| FORD has joined the company on Thursday 3rd December 1981    |
| MILLER has joined the company on Saturday 23rd January 1982  |
+--------------------------------------------------------------+
```

## Question 7 : Find the date for nearest Saturday after current date.
### Query :
```sql
SELECT DATE_ADD(CURDATE(),INTERVAL (5-WEEKDAY(CURDATE())+7) %7 DAY);
```
### Output :
```sql
+---------------------------------------------------------+
| DATE_ADD(CURDATE(),INTERVAL (5-WEEKDAY(CURDATE())) DAY) |
+---------------------------------------------------------+
| 2026-02-28                                              |
+---------------------------------------------------------+
```
## Question 8 : Display current time.
### Query :
```sql
SELECT TIME(NOW());
```
### Output :
```sql
+-------------+
| TIME(NOW()) |
+-------------+
| 16:45:28    |
+-------------+
```
## Question 9 : Display the date three months Before the current date.
### Query :
```sql
SELECT DATE_SUB(CURDATE(),INTERVAL 3 MONTH);
```
### Output :
```sql
+--------------------------------------+
| DATE_SUB(CURDATE(),INTERVAL 3 MONTH) |
+--------------------------------------+
| 2025-11-25                           |
+--------------------------------------+
```
## Question 10 : Display those employees who joined in the company in the month of Dec.
### Query :
```sql
select * from employee where MONTH(HIREDATE) =  12;
```
### Output :
```sql
+-------+-------+---------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+---------+------+------------+------+------+--------+
|  7369 | SMITH | CLERK   | 7902 | 1980-12-17 |  880 | NULL |     20 |
|  7788 | SCOTT | ANALYST | 7566 | 1982-12-09 | 3300 | NULL |     40 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 | 1045 | NULL |     30 |
|  7902 | FORD  | ANALYST | 7566 | 1981-12-03 | 3300 | NULL |     20 |
+-------+-------+---------+------+------------+------+------+--------+
```
## Question 11 : Display those employees whose first 2 characters from hire date = last 2 characters of salary.
### Query :
```sql
SELECT * FROM EMPLOYEE WHERE LEFT(DATE_FORMAT(HIREDATE, '%D %M %Y'), 2) = RIGHT(SAL, 2);
```
### Output :
```sql
Empty set (0.000 sec)
```
## Question 12 : Display those employees whose 10% of salary is equal to the year of joining.
### Query :
```sql
SELECT * FROM EMPLOYEE WHERE SAL * 0.10 = YEAR(HIREDATE);
```
### Output :
```sql
Empty set (0.001 sec)
```
## Question 13 : Display those employees who joined the company before 15 of the months.
### Query :
```sql
SELECT * FROM EMPLOYEE WHERE DAY(HIREDATE) < 15;
```
### Output :
```sql
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7566 | JONES  | MANAGER  | 7839 | 1981-04-02 | 3273 | NULL |     20 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 3135 | NULL |     30 |
|  7782 | CLARK  | MANAGER  | 7839 | 1981-06-09 | 2695 | NULL |     20 |
|  7788 | SCOTT  | ANALYST  | 7566 | 1982-12-09 | 3300 | NULL |     40 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK    | 7788 | 1983-01-12 | 1210 | NULL |     20 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 | 1045 | NULL |     30 |
|  7902 | FORD   | ANALYST  | 7566 | 1981-12-03 | 3300 | NULL |     20 |
+-------+--------+----------+------+------------+------+------+--------+
```
## Question 14 : Display those employees who has joined before 15th of the month.
### Query :
```sql
SELECT * FROM EMPLOYEE WHERE DAY(HIREDATE) < 15;
```
### Output :
```sql
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7566 | JONES  | MANAGER  | 7839 | 1981-04-02 | 3273 | NULL |     20 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 3135 | NULL |     30 |
|  7782 | CLARK  | MANAGER  | 7839 | 1981-06-09 | 2695 | NULL |     20 |
|  7788 | SCOTT  | ANALYST  | 7566 | 1982-12-09 | 3300 | NULL |     40 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK    | 7788 | 1983-01-12 | 1210 | NULL |     20 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 | 1045 | NULL |     30 |
|  7902 | FORD   | ANALYST  | 7566 | 1981-12-03 | 3300 | NULL |     20 |
+-------+--------+----------+------+------------+------+------+--------+
```
## Question 15 : Display those employees whose joining DATE is available in deptno.
### Query :
```sql
SELECT * FROM EMPLOYEE WHERE DAY(HIREDATE) = DEPTNO;
```
### Output :
```sql
Empty set (0.001 sec)
```
