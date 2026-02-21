# SQL Lab - Experiment 2
## Aim: To study and perform SQL data retrieval operations using Employee table.
## Question 1 : List all distinct job in Employee.
### Query : 
~~~sql   
 SELECT DISTINCT job FROM EMPLOYEE;
~~~
### Output :
~~~SQL
+-----------+
| job       |
+-----------+
| CLERK     |
| SELESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
~~~

## Question 2 : List all information about employee in Department Number 30.
### Query :
~~~sql   
SELECT* FROM EMPLOYEE WHERE DEPTNO=30;
~~~
### Output :
~~~SQL
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7499 | ALLEN  | SELESMAN | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SELESMAN | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7654 | MARTIN | SELESMAN | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-03-01 | 2850 | NULL |     30 |
|  7844 | TURNER | SELESMAN | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950 | NULL |     30 |
+-------+--------+----------+------+------------+------+------+--------+
~~~

## Question 3 : Find all department number with department names greater than 20.
### Query :
~~~sql   
  SELECT JOB,DEPTNO FROM EMPLOYEE WHERE DEPTNO >20;
~~~
### Output :
~~~SQL
+----------+--------+
| JOB      | DEPTNO |
+----------+--------+
| SELESMAN |     30 |
| SELESMAN |     30 |
| SELESMAN |     30 |
| MANAGER  |     30 |
| ANALYST  |     40 |
| SELESMAN |     30 |
| CLERK    |     30 |
+----------+--------+
~~~

## Question 4 : Find all information about all the managers as well as the clerks in department 30.
### Query :
~~~sql   
SELECT * FROM EMPLOYEE WHERE JOB IN("MANAGER","CLERK") AND DEPTNO=30;
~~~
### Output :
~~~SQL
+-------+-------+---------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+---------+------+------------+------+------+--------+
|  7698 | BLAKE | MANAGER | 7839 | 1981-03-01 | 3135 | NULL |     30 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 | 1045 | NULL |     30 |
+-------+-------+---------+------+------------+------+------+--------+
~~~

## Question 5 : List the Employee name, Employee numbers and department of all clerks.
### Query :
~~~sql   
SELECT ENAME,EMPNO,JOB FROM EMPLOYEE WHERE JOB="CLERK";
~~~
### Output :
~~~SQL
+--------+-------+-------+
| ENAME  | EMPNO | JOB   |
+--------+-------+-------+
| SMITH  |  7369 | CLERK |
| ADAMS  |  7876 | CLERK |
| JAMES  |  7900 | CLERK |
| MILLER |  7934 | CLERK |
+--------+-------+-------+
~~~

## Question 6 : Find all managers not in department 30.
### Query :
~~~sql  
SELECT EMPNO, ENAME,JOB FROM EMPLOYEE WHERE JOB="MANAGER" AND DEPTNO<>30;
~~~
### Output :
~~~SQL
+-------+-------+---------+
| EMPNO | ENAME | JOB     |
+-------+-------+---------+
|  7566 | JONES | MANAGER |
|  7782 | CLARK | MANAGER |
+-------+-------+---------+
~~~
## Question 7 : List information about all Employees in department 10 who are not manager or clerks.
### Query :
~~~sql   
 SELECT* FROM EMPLOYEE WHERE DEPTNO=10 AND JOB NOT IN('MANAGER','CLERK');
~~~
### Output :
~~~SQL
Empty set (0.006 sec)
~~~

## Question 8 : Find Employees and jobs earning between 1200 and 1400.
### Query :
~~~sql   
SELECT ENAME,JOB,SAL FROM EMPLOYEE WHERE SAL BETWEEN 1200 AND 1400;
~~~
### Output :
~~~SQL
+--------+----------+------+
| ENAME  | JOB      | SAL  |
+--------+----------+------+
| WARD   | SELESMAN | 1250 |
| MARTIN | SELESMAN | 1250 |
| MILLER | CLERK    | 1300 |
+--------+----------+------+
~~~
## Question 9 : List Name and Department Number of employee who are clerks, analyst or salesman.
### Query :
~~~sql   
SELECT ENAME,DEPTNO,JOB FROM EMPLOYEE WHERE JOB IN ('CLERK','ANALYST','SALESMAN');
~~~
### Output :
~~~SQL
+--------+--------+---------+
| ENAME  | DEPTNO | JOB     |
+--------+--------+---------+
| SMITH  |     20 | CLERK   |
| SCOTT  |     40 | ANALYST |
| ADAMS  |     20 | CLERK   |
| JAMES  |     30 | CLERK   |
| FORD   |     20 | ANALYST |
| MILLER |     10 | CLERK   |
+--------+--------+---------+

~~~
## Question 10 : List Name and Department Number of employee whose names began with M.
### Query :
~~~sql   
SELECT ENAME,DEPTNO FROM EMPLOYEE WHERE ENAME LIKE 'M%';
~~~
### Output :
~~~SQL
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| MARTIN |     30 |
| MILLER |     10 |
+--------+--------+

~~~
