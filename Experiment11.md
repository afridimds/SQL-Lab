# SQL Lab - Experiment 11
## Aim: To write and execute SQL queries to perform advanced data manipulation and retrieval operations using conditions, joins, aggregate functions, subqueries, and grouping on employee and department tables.
## Question 1 : Delete those employees who joined the company before 31 dec-82 while there dept location is ‘DELHI’ or ‘CHENNAI’.
### Query :
```sql
 DELETE FROM EMPLOYEE
    -> WHERE HIREDATE < '1982-12-31'
    -> AND DEPTNO IN (SELECT DEPTNO FROM DEPARTMENT
    ->     WHERE LOCATION IN ('DELHI', 'CHENNAI'));

SELECT * FROM EMPLOYEE;
```
### Output :
```sql
+-------+-------+-----------+------+------------+---------+------+--------+
| EMPNO | ENAME | JOB       | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+-------+-----------+------+------------+---------+------+--------+
|  7369 | SMITH | CLERK     | 7902 | 1980-12-17 |  800.00 | NULL |     20 |
|  7566 | JONES | MANAGER   | 7839 | 1981-04-02 | 2975.00 | NULL |     20 |
|  7788 | SCOTT | ANALYST   | 7566 | 1982-12-09 | 3000.00 | NULL |     40 |
|  7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000.00 | NULL |     20 |
|  7876 | ADAMS | CLERK     | 7788 | 1983-01-12 | 1100.00 | NULL |     20 |
|  7902 | FORD  | ANALYST   | 7566 | 1981-12-03 | 3000.00 | NULL |     20 |
+-------+-------+-----------+------+------------+---------+------+--------+
```
## Question 2 : Display employee name, job, deptname, location for all who are working as managers.
### Query :
```sql
 SELECT E.ENAME,E.JOB,D.DNAME,D.LOCATION FROM EMPLOYEE E
      JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
      WHERE E.JOB = 'MANAGER';
```
### Output :
```sql
+-------+---------+------------+----------+
| ENAME | JOB     | DNAME      | LOCATION |
+-------+---------+------------+----------+
| JONES | MANAGER | ACCOUNTING | MUMBAI   |
+-------+---------+------------+----------+
```
## Question 3 : Display name and salary of ford if his sal is equal to high sal of his grade.
### Query :
```sql
SELECT E.ENAME, E.SAL FROM EMPLOYEE E
      JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
      WHERE E.ENAME = 'FORD'
      AND E.SAL = (SELECT MAX(E2.SAL) FROM EMPLOYEE E2
      JOIN SALGRADE S2 ON E2.SAL BETWEEN S2.LOSAL AND S2.HISAL
      WHERE S2.GRADE = S.GRADE);
```
### Output :
```sql
+-------+---------+
| ENAME | SAL     |
+-------+---------+
| FORD  | 3000.00 |
+-------+---------+
```
## Question 4 : Find out the top 5 earner of company.
### Query :
```sql
SELECT ENAME, SAL FROM EMPLOYEE
      ORDER BY SAL DESC LIMIT 5;
```
### Output :
```sql
+-------+---------+
| ENAME | SAL     |
+-------+---------+
| KING  | 5000.00 |
| SCOTT | 3000.00 |
| FORD  | 3000.00 |
| JONES | 2975.00 |
| ADAMS | 1100.00 |
+-------+---------+
```
## Question 5 : Display the name of those employees who are getting highest salary.
### Query :
```sql
SELECT ENAME FROM EMPLOYEE
      WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```
### Output :
```sql
+-------+
| ENAME |
+-------+
| KING  |
+-------+
```
## Question 6 : Display those employees whose salary is equal to average of maximum and minimum.
### Query :
```sql
SELECT ENAME, SAL FROM EMPLOYEE
      WHERE SAL = ((SELECT MAX(SAL) FROM EMPLOYEE) +
      (SELECT MIN(SAL) FROM EMPLOYEE)) / 2;
```
### Output :
```sql
Empty set (0.001 sec)
```
## Question 7 : Display dname where at least 3 are working and display only dname.
### Query :
```sql
 SELECT D.DNAME FROM DEPARTMENT D
      JOIN EMPLOYEE E ON D.DEPTNO = E.DEPTNO
      GROUP BY D.DNAME HAVING COUNT(*) >= 3;
```
### Output :
```sql
+------------+
| DNAME      |
+------------+
| ACCOUNTING |
+------------+
```
## Question 8 : Display name of those managers names whose salary is more than average salary of company.
### Query :
```sql
SELECT ENAME FROM EMPLOYEE WHERE JOB = 'MANAGER'
      AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE);
```
### Output :
```sql
+-------+
| ENAME |
+-------+
| JONES |
+-------+
```
## Question 9 : Display those managers name whose salary is more than an average salary of his employees.
### Query :
```sql
 SELECT M.ENAME FROM EMPLOYEE M WHERE M.JOB = 'MANAGER'
      AND M.SAL > (SELECT AVG(E.SAL)FROM EMPLOYEE E
      WHERE E.MGR = M.EMPNO);
```
### Output :
```sql
Empty set (0.001 sec)
```
## Question 10 : Display employee name, sal, comm and net pay for those employees whose net pay are greater than or equal to any other employee salary of the company?
### Query :
```sql
 SELECT ENAME, SAL, COMM, (SAL + IFNULL(COMM,0)) 
      AS NET_PAY FROM EMPLOYEE WHERE 
      (SAL + IFNULL(COMM,0)) >= ANY (SELECT SAL FROM EMPLOYEE);
```
### Output :
```sql
+-------+---------+------+---------+
| ENAME | SAL     | COMM | NET_PAY |
+-------+---------+------+---------+
| SMITH |  800.00 | NULL |  800.00 |
| JONES | 2975.00 | NULL | 2975.00 |
| SCOTT | 3000.00 | NULL | 3000.00 |
| KING  | 5000.00 | NULL | 5000.00 |
| ADAMS | 1100.00 | NULL | 1100.00 |
| FORD  | 3000.00 | NULL | 3000.00 |
+-------+---------+------+---------+
```