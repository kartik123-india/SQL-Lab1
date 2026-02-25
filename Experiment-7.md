# Experiment-7

## Aim

To perform aggregate functions, grouping operations and advanced SQL queries on EMPLOYEE table.

------------------------------------------------------------------------

## Question 1

Compute the number of days remaining in this year.

``` sql
SELECT DATEDIFF(
STR_TO_DATE(CONCAT(YEAR(CURDATE()),'-12-31'),'%Y-%m-%d'),
CURDATE()) AS DAYS_REMAINING;
```

### Output
+----------------+
| DAYS_REMAINING |
+----------------+
| 309            |
+----------------+
1 row in set (0.001 sec)

------------------------------------------------------------------------

## Question 2

Find the highest salary, lowest salary and difference between them.

``` sql
SELECT MAX(SAL) AS HIGHEST_SALARY,
MIN(SAL) AS LOWEST_SALARY,
MAX(SAL)-MIN(SAL) AS DIFFERENCE
FROM EMPLOYEE;
```

### Output
+-----------------+----------------+------------+
| HIGHEST_SALARY  | LOWEST_SALARY  | DIFFERENCE |
+-----------------+----------------+------------+
| 5500            | 880            | 4620       |
+-----------------+----------------+------------+
1 row in set (0.002 sec)

------------------------------------------------------------------------

## Question 3

List employee whose commission is greater than 25% of salary.

``` sql
SELECT ENAME,SAL,COMM
FROM EMPLOYEE
WHERE COMM > 0.25*SAL;
```

### Output
+--------+------+------+
| ENAME  | SAL  | COMM |
+--------+------+------+
| MARTIN | 1250 | 1400 |
+--------+------+------+
1 row in set (0.002 sec)

------------------------------------------------------------------------

## Question 4

Display salary in dollar format.

``` sql
SELECT ENAME,
CONCAT('$',SAL) AS SALARY
FROM EMPLOYEE;
```

### Output
+--------+---------+
| ENAME  | SALARY  |
+--------+---------+
| SMITH  | $880    |
| ALLEN  | $1600   |
| WARD   | $1250   |
| JONES  | $3273   |
| MARTIN | $1250   |
| BLAKE  | $3135   |
| CLARK  | $2695   |
| SCOTT  | $3300   |
| KING   | $5500   |
| TURNER | $1500   |
| ADAMS  | $1210   |
| JAMES  | $1045   |
| FORD   | $3300   |
| MILLER | $1430   |
+--------+---------+
14 rows in set (0.002 sec)

------------------------------------------------------------------------

## Question 5

Create matrix query displaying job and salary based on department number.

``` sql
SELECT JOB,
SUM(CASE WHEN DEPTNO=10 THEN SAL END) AS DEPT10,
SUM(CASE WHEN DEPTNO=20 THEN SAL END) AS DEPT20,
SUM(CASE WHEN DEPTNO=30 THEN SAL END) AS DEPT30,
SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY JOB;
```

### Output
+-----------+--------+--------+--------+--------------+
| JOB       | DEPT10 | DEPT20 | DEPT30 | TOTAL_SALARY |
+-----------+--------+--------+--------+--------------+
| CLERK     | 1430   | 2090   | 1045   | 4565         |
| MANAGER   | NULL   | 5968   | 3135   | 9103         |
| SALESMAN  | NULL   | NULL   | 5600   | 5600         |
| ANALYST   | NULL   | 6600   | NULL   | 6600         |
| PRESIDENT | NULL   | 5500   | NULL   | 5500         |
+-----------+--------+--------+--------+--------------+
5 rows in set (0.003 sec)

------------------------------------------------------------------------

## Question 6

Display total employees and number hired in 1980,1981,1982 and 1983.

``` sql
SELECT 
COUNT(*) AS TOTAL_EMPLOYEES,
SUM(YEAR(HIREDATE)=1980) AS Y1980,
SUM(YEAR(HIREDATE)=1981) AS Y1981,
SUM(YEAR(HIREDATE)=1982) AS Y1982,
SUM(YEAR(HIREDATE)=1983) AS Y1983
FROM EMPLOYEE;
```

### Output
+-----------------+-------+-------+-------+-------+
| TOTAL_EMPLOYEES | Y1980 | Y1981 | Y1982 | Y1983 |
+-----------------+-------+-------+-------+-------+
| 14              | 1     | 10    | 2     | 1     |
+-----------------+-------+-------+-------+-------+
1 row in set (0.002 sec)

------------------------------------------------------------------------

## Question 7

Query to get the last Sunday of any month.

``` sql
SELECT LAST_DAY(CURDATE()) -
INTERVAL (DAYOFWEEK(LAST_DAY(CURDATE()))-1) DAY
AS LAST_SUNDAY;
```

### Output
+-------------+
| LAST_SUNDAY |
+-------------+
| 2026-02-22  |
+-------------+
1 row in set (0.001 sec)

------------------------------------------------------------------------

## Question 8

Display department numbers and total number of employees working in each department.

``` sql
SELECT DEPTNO,
COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY DEPTNO;
```

### Output
+--------+----------------+
| DEPTNO | TOTAL_EMPLOYEES|
+--------+----------------+
| 10     | 1              |
| 20     | 5              |
| 30     | 6              |
+--------+----------------+
3 rows in set (0.002 sec)

------------------------------------------------------------------------

## Question 9

Display various jobs and total number of employees within each job group.

``` sql
SELECT JOB,
COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY JOB;
```

### Output
+-----------+----------------+
| JOB       | TOTAL_EMPLOYEES|
+-----------+----------------+
| CLERK     | 4              |
| MANAGER   | 3              |
| SALESMAN  | 4              |
| ANALYST   | 2              |
| PRESIDENT | 1              |
+-----------+----------------+
5 rows in set (0.002 sec)

------------------------------------------------------------------------

## Question 10

Display department numbers and total salary for each department.

``` sql
SELECT DEPTNO,
SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY DEPTNO;
```

### Output
+--------+--------------+
| DEPTNO | TOTAL_SALARY |
+--------+--------------+
| 10     | 1430         |
| 20     | 10848        |
| 30     | 9400         |
+--------+--------------+
3 rows in set (0.002 sec)

------------------------------------------------------------------------
