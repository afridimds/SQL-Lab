# SQL Lab - Experiment 8
## Aim: To study and implement SQL queries involving multiple tables using different types of joins, conditions, grouping, and sorting in order to retrieve meaningful information such as employee details, department names, manager relationships, salary grades, and aggregated results.
## Question 1 : Display all employees with their dept name.
### Query :
```sql
SELECT E.ENAME,D.DNAME FROM EMPLOYEE E JOIN DEPARTMENT D ON
     E.DEPTNO = D.DEPTNO;
```
### Output :
```sql
+--------+------------+
| ENAME  | DNAME      |
+--------+------------+
| MILLER | RESEARCH   |
| SMITH  | ACCOUNTING |
| JONES  | ACCOUNTING |
| CLARK  | ACCOUNTING |
| KING   | ACCOUNTING |
| ADAMS  | ACCOUNTING |
| FORD   | ACCOUNTING |
| ALLEN  | SALES      |
| WARD   | SALES      |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| TURNER | SALES      |
| JAMES  | SALES      |
| SCOTT  | OPERATIONS |
+--------+------------+
```
## Question 2 : Display those employees whose manager names is jones, and also display their manager name.
### Query :
```sql
SELECT E.ENAME,M.ENAME AS MANAGER FROM EMPLOYEE E JOIN EMPLOYEE M ON E.MGR = M.EMPNO WHERE M.ENAME ='JONES';
```
### Output :
```sql
+-------+---------+
| ENAME | MANAGER |
+-------+---------+
| SCOTT | JONES   |
| FORD  | JONES   |
+-------+---------+
```
## Question 3 : Display employee name, his job, his dept name, his manager name, his grade and make out of an under department wise.
### Query :
```sql
SELECT E.ENAME, E.JOB, D.DNAME, M.ENAME AS MANAGER
      FROM EMPLOYEE E JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
      LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO ORDER BY D.DNAME;
```
### Output :
```sql
+--------+-----------+------------+---------+
| ENAME  | JOB       | DNAME      | MANAGER |
+--------+-----------+------------+---------+
| SMITH  | CLERK     | ACCOUNTING | FORD    |
| JONES  | MANAGER   | ACCOUNTING | KING    |
| CLARK  | MANAGER   | ACCOUNTING | KING    |
| KING   | PRESIDENT | ACCOUNTING | NULL    |
| ADAMS  | CLERK     | ACCOUNTING | SCOTT   |
| FORD   | ANALYST   | ACCOUNTING | JONES   |
| SCOTT  | ANALYST   | OPERATIONS | JONES   |
| MILLER | CLERK     | RESEARCH   | CLARK   |
| ALLEN  | SALESMAN  | SALES      | BLAKE   |
| WARD   | SALESMAN  | SALES      | BLAKE   |
| MARTIN | SALESMAN  | SALES      | BLAKE   |
| BLAKE  | MANAGER   | SALES      | KING    |
| TURNER | SALESMAN  | SALES      | BLAKE   |
| JAMES  | CLERK     | SALES      | BLAKE   |
+--------+-----------+------------+---------+
```
## Question 4 : List out all the employees name, job, and salary grade and department name for everyone in the company except ‘clerk’. Sort on salary display the highest salary.
### Query :
```sql
SELECT E.ENAME, E.JOB, S.GRADE, D.DNAME, E.SAL
      FROM EMPLOYEE E JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
      JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL WHERE
      E.JOB <> 'CLERK' ORDER BY E.SAL DESC;
```
### Output :
```sql
+--------+-----------+-------+------------+------+
| ENAME  | JOB       | GRADE | DNAME      | SAL  |
+--------+-----------+-------+------------+------+
| KING   | PRESIDENT | E     | ACCOUNTING | 5500 |
| SCOTT  | ANALYST   | E     | OPERATIONS | 3300 |
| FORD   | ANALYST   | E     | ACCOUNTING | 3300 |
| JONES  | MANAGER   | E     | ACCOUNTING | 3273 |
| BLAKE  | MANAGER   | E     | SALES      | 3135 |
| CLARK  | MANAGER   | D     | ACCOUNTING | 2695 |
| ALLEN  | SALESMAN  | C     | SALES      | 1600 |
| TURNER | SALESMAN  | C     | SALES      | 1500 |
| WARD   | SALESMAN  | B     | SALES      | 1250 |
| MARTIN | SALESMAN  | B     | SALES      | 1250 |
+--------+-----------+-------+------------+------+
```
## Question 5 : Display employee name, his job and his manager. Display also employees who are without manager.
### Query :
```sql
SELECT E.ENAME, E.JOB, M.ENAME AS MANAGER FROM
      EMPLOYEE E LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
```
### Output :
```sql
+--------+-----------+---------+
| ENAME  | JOB       | MANAGER |
+--------+-----------+---------+
| SMITH  | CLERK     | FORD    |
| ALLEN  | SALESMAN  | BLAKE   |
| WARD   | SALESMAN  | BLAKE   |
| JONES  | MANAGER   | KING    |
| MARTIN | SALESMAN  | BLAKE   |
| BLAKE  | MANAGER   | KING    |
| CLARK  | MANAGER   | KING    |
| SCOTT  | ANALYST   | JONES   |
| KING   | PRESIDENT | NULL    |
| TURNER | SALESMAN  | BLAKE   |
| ADAMS  | CLERK     | SCOTT   |
| JAMES  | CLERK     | BLAKE   |
| FORD   | ANALYST   | JONES   |
| MILLER | CLERK     | CLARK   |
+--------+-----------+---------+
```
## Question 6 : List the employee name, job, annual salary, deptno, dept name and grade who earn 36000 a year or who are not clerks.
### Query :
```sql
SELECT E.ENAME, E.JOB, (E.SAL * 12) AS Annual_Salary,
      E.DEPTNO, D.DNAME, S.GRADE FROM EMPLOYEE E JOIN DEPARTMENT D ON
      E.DEPTNO = D.DEPTNO JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND
      S.HISAL WHERE (E.SAL * 12) = 36000 AND E.JOB <> 'CLERK';
```
### Output :
```sql
Empty set (0.001 sec)
```
## Question 7 : List ename, job, annual sal, deptno, dname and grade who earn 30000 per year and who are not clerks.
### Query :
```sql
SELECT E.ENAME, E.JOB, (E.SAL * 12) AS Annual_Salary,
      E.DEPTNO, D.DNAME, S.GRADE FROM EMPLOYEE E JOIN DEPARTMENT D ON
      E.DEPTNO = D.DEPTNO JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND
      S.HISAL WHERE (E.SAL * 12) = 30000 AND E.JOB <> 'CLERK';
```
### Output :
```sql
Empty set (0.024 sec)
```
## Question 8 : List out all employees by name and number along with their manager’s name and number also display ‘no manager’ who has no manager.
### Query :
```sql
SELECT E.ENAME, E.EMPNO, IFNULL(M.EMPNO, 0) AS MGR_NO,
      IFNULL(M.ENAME, 'NO MANAGER') AS MANAGER FROM EMPLOYEE E
      LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
```
### Output :
```sql
+--------+-------+--------+------------+
| ENAME  | EMPNO | MGR_NO | MANAGER    |
+--------+-------+--------+------------+
| SMITH  |  7369 |   7902 | FORD       |
| ALLEN  |  7499 |   7698 | BLAKE      |
| WARD   |  7521 |   7698 | BLAKE      |
| JONES  |  7566 |   7839 | KING       |
| MARTIN |  7654 |   7698 | BLAKE      |
| BLAKE  |  7698 |   7839 | KING       |
| CLARK  |  7782 |   7839 | KING       |
| SCOTT  |  7788 |   7566 | JONES      |
| KING   |  7839 |      0 | NO MANAGER |
| TURNER |  7844 |   7698 | BLAKE      |
| ADAMS  |  7876 |   7788 | SCOTT      |
| JAMES  |  7900 |   7698 | BLAKE      |
| FORD   |  7902 |   7566 | JONES      |
| MILLER |  7934 |   7782 | CLARK      |
+--------+-------+--------+------------+
```
## Question 9 : Select dept name, dept no and sum of sal.
### Query :
```sql
SELECT D.DNAME,D.DEPTNO, SUM(E.SAL) AS Total_Salary
      FROM EMPLOYEE E JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
      GROUP BY D.DNAME,D.DEPTNO;
```
### Output :
```sql
+------------+--------+--------------+
| DNAME      | DEPTNO | Total_Salary |
+------------+--------+--------------+
| ACCOUNTING |     20 |        16858 |
| OPERATIONS |     40 |         3300 |
| RESEARCH   |     10 |         1430 |
| SALES      |     30 |         9780 |
+------------+--------+--------------+
```
## Question 10 : Display employee number, name and department name in which he is working.
### Query :
```sql
SELECT E.EMPNO, E.ENAME, D.DNAME FROM EMPLOYEE E
      JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```
### Output :
```sql
+-------+--------+------------+
| EMPNO | ENAME  | DNAME      |
+-------+--------+------------+
|  7934 | MILLER | RESEARCH   |
|  7369 | SMITH  | ACCOUNTING |
|  7566 | JONES  | ACCOUNTING |
|  7782 | CLARK  | ACCOUNTING |
|  7839 | KING   | ACCOUNTING |
|  7876 | ADAMS  | ACCOUNTING |
|  7902 | FORD   | ACCOUNTING |
|  7499 | ALLEN  | SALES      |
|  7521 | WARD   | SALES      |
|  7654 | MARTIN | SALES      |
|  7698 | BLAKE  | SALES      |
|  7844 | TURNER | SALES      |
|  7900 | JAMES  | SALES      |
|  7788 | SCOTT  | OPERATIONS |
+-------+--------+------------+
```
