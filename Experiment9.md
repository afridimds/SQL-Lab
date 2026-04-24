# SQL Lab - Experiment 9
## Aim: 
## Question 1 : Display the name of emp name who earns highest salary.
### Query :
```sql
SELECT ENAME FROM EMPLOYEE WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```
### Output :
```sql
+-------+
| ENAME |
+-------+
| KING  |
+-------+
```
## Question 2 : Display the employee number and name of employee working as clerk and earning highest salary among clerks.
### Query :
```sql
SELECT EMPNO, ENAME FROM EMPLOYEE WHERE JOB = 'CLERK'
    -> AND SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```
### Output :
```sql
+-------+--------+
| EMPNO | ENAME  |
+-------+--------+
|  7934 | MILLER |
+-------+--------+
```
## Question 3 : Display the names of the salesman who earns a salary more than the highest salary of any clerk.
### Query :
```sql
SELECT ENAME FROM EMPLOYEE WHERE JOB = 'SALESMAN'
    -> AND SAL > (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```
### Output :
```sql
+--------+
| ENAME  |
+--------+
| ALLEN  |
| TURNER |
+--------+
```
## Question 4 : Display the names of clerks who earn salary more than that of james of that of sal lesser than that of scott.
### Query :
```sql
SELECT ENAME FROM EMPLOYEE WHERE JOB = 'CLERK'
    -> AND SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
    -> AND SAL < (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
+--------+
```
### Output :
```sql
+--------+
| ENAME  |
+--------+
| ADAMS  |
| MILLER |
+--------+
```
## Question 5 : Display the names of employees who earn a sal more than that of james or that of salary greater than that of scott.
### Query :
```sql
SELECT ENAME FROM EMPLOYEE WHERE
    -> SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
    -> OR SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```
### Output :
```sql
+--------+
| ENAME  |
+--------+
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| BLAKE  |
| CLARK  |
| SCOTT  |
| KING   |
| TURNER |
| ADAMS  |
| FORD   |
| MILLER |
+--------+
```
## Question 6 : Display the names of the employees who earn highest salary in their respective departments.
### Query :
```sql
SELECT ENAME FROM EMPLOYEE E WHERE
    -> SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE DEPTNO = E.DEPTNO);
```
### Output :
```sql
+--------+
| ENAME  |
+--------+
| BLAKE  |
| SCOTT  |
| KING   |
| MILLER |
+--------+
```
## Question 7 : Display the names of employees who earn highest salaries in their respective job groups.
### Query :
```sql
SELECT ENAME FROM EMPLOYEE E WHERE
    -> SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = E.JOB);
```
### Output :
```sql
+--------+
| ENAME  |
+--------+
| ALLEN  |
| JONES  |
| SCOTT  |
| KING   |
| FORD   |
| MILLER |
+--------+
```
## Question 8 : Display the employee names who are working in accounting dept.
### Query :
```sql
SELECT ENAME FROM EMPLOYEE
    ->     WHERE DEPTNO = (SELECT DEPTNO FROM DEPARTMENT
    ->     WHERE DNAME = 'ACCOUNTING');
```
### Output :
```sql
+-------+
| ENAME |
+-------+
| SMITH |
| JONES |
| KING  |
| ADAMS |
| FORD  |
+-------+
```
## Question 9 : Display the job groups having total salary greater than the maximum salary for managers.
### Query :
```sql
SELECT JOB, SUM(SAL) AS TOTAL_SALARY
     FROM EMPLOYEE
     GROUP BY JOB
     HAVING SUM(SAL) > ( SELECT MAX(SAL) FROM EMPLOYEE 
     WHERE JOB = 'MANAGER');
```
### Output :
```sql
+-----------+--------------+
| JOB       | TOTAL_SALARY |
+-----------+--------------+
| ANALYST   |      6600.00 |
| CLERK     |      4565.00 |
| MANAGER   |      9102.50 |
| PRESIDENT |      5500.00 |
| SALESMAN  |      5600.00 |
+-----------+--------------+
```