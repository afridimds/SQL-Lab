# SQL Lab - Experiment 10
## Aim: To write and execute SQL queries using different clauses and concepts such as subqueries, joins, conditions, aggregate comparisons, and filtering in order to retrieve specific employee details from a relational database.
## Question 1 : Display the names of employees from department number 10 with salary greater than that of any employee working in other departments.
### Query :
```sql
SELECT ENAME FROM EMPLOYEE WHERE DEPTNO = 10
      AND SAL > (SELECT MIN(SAL) FROM EMPLOYEE WHERE DEPTNO <> 10);
```
### Output :
```sql
+--------+
| ENAME  |
+--------+
| MILLER |
+--------+
```
## Question 2 : Display the names of employee from department number 10 with salary greater than that of all employee working in other departments.
### Query :
```sql
SELECT ENAME FROM EMPLOYEE WHERE DEPTNO = 10
      AND SAL > ALL(SELECT SAL FROM EMPLOYEE WHERE DEPTNO <> 10);
```
### Output :
```sql
Empty set (0.001 sec)
```
## Question 3 : Display the details of employees who are in sales dept and grade is C.
### Query :
```sql
SELECT E.* FROM EMPLOYEE E
      JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
      JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
      WHERE D.DNAME = 'SALES'
      AND S.GRADE = 'C';
```
### Output :
```sql
+-------+--------+----------+------+------------+---------+--------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL     | COMM   | DEPTNO |
+-------+--------+----------+------+------------+---------+--------+--------+
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600.00 | 300.00 |     30 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500.00 |   0.00 |     30 |
+-------+--------+----------+------+------------+---------+--------+--------+
```
## Question 4 : Display those who are not managers and who manages anyone.
### Query :
```sql
 SELECT ENAME FROM EMPLOYEE
      WHERE JOB != 'MANAGER'
      AND EMPNO IN ( SELECT MGR FROM EMPLOYEE WHERE MGR IS NOT NULL);
```
### Output :
```sql
+-------+
| ENAME |
+-------+
| SCOTT |
| KING  |
| FORD  |
+-------+
```
## Question 5 : Display those employees whose manager name is jones.
### Query :
```sql
 SELECT E.ENAME FROM EMPLOYEE E 
      JOIN EMPLOYEE M ON E.MGR = M.EMPNO
      WHERE M.ENAME = 'JONES';
```
### Output :
```sql
+-------+
| ENAME |
+-------+
| SCOTT |
| FORD  |
+-------+
```
## Question 6 : Display ename who are working in sales dept.
### Query :
```sql
SELECT E.ENAME FROM EMPLOYEE E
      JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
      WHERE D.DNAME = 'SALES';
```
### Output :
```sql
+--------+
| ENAME  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
| BLAKE  |
| TURNER |
| JAMES  |
+--------+
```
## Question 7 : Display those employees whose salary greater than his manager salary.
### Query :
```sql
SELECT E.ENAME FROM EMPLOYEE E
      JOIN EMPLOYEE M ON E.MGR = M.EMPNO
      WHERE E.SAL > M.SAL;
```
### Output :
```sql
+-------+
| ENAME |
+-------+
| SCOTT |
| FORD  |
+-------+
```
## Question 8 : Display those employees who are working in the same dept where his manager is working.
### Query :
```sql
 SELECT E.ENAME FROM EMPLOYEE E
      JOIN EMPLOYEE M ON E.MGR = M.EMPNO
      WHERE E.DEPTNO = M.DEPTNO;
```
### Output :
```sql
+--------+
| ENAME  |
+--------+
| SMITH  |
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| TURNER |
| JAMES  |
| FORD   |
| MILLER |
+--------+
```
## Question 9 : Display grade and employees name for the dept no 10 or 30 but grade is not D, while joined the company before 31-dec-82.
### Query :
```sql
SELECT E.ENAME, S.GRADE FROM EMPLOYEE E
      JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
      WHERE E.DEPTNO IN (10, 30)
      AND S.GRADE != 'D'
      AND E.HIREDATE < '1982-12-31';
```
### Output :
```sql
+--------+-------+
| ENAME  | GRADE |
+--------+-------+
| ALLEN  | C     |
| WARD   | B     |
| MARTIN | B     |
| BLAKE  | E     |
| TURNER | C     |
| JAMES  | A     |
| MILLER | C     |
+--------+-------+
```