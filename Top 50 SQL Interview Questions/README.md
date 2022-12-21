## 🔗50 SQL Query Questions and Answers for Practice.
USE sqltutorials;
SELECT * FROM bonus;
SELECT * FROM title;
SELECT * FROM worker;
	
-- Q-11. Write an SQL query to print all Worker details from the Worker table order by FIRST_NAME Ascending.
SELECT * FROM worker ORDER BY FIRST_NAME;

-- Q-12. Write an SQL query to print all Worker details from the Worker table order by FIRST_NAME Ascending and DEPARTMENT Descending.
SELECT * FROM worker ORDER BY FIRST_NAME ASC ,  DEPARTMENT DESC;

-- Q-13. Write an SQL query to print details for Workers with the first name as “Vipul” and “Satish” from Worker table.
SELECT * FROM worker WHERE FIRST_NAME in ('Vipul','Satish') ;

-- Q-14. Write an SQL query to print details of workers excluding first names, “Vipul” and “Satish” from Worker table.
SELECT * FROM worker WHERE FIRST_NAME NOT IN ('Vipul','Satish');

-- Q-15. Write an SQL query to print details of Workers with DEPARTMENT name as “Admin”.
SELECT * FROM worker WHERE DEPARTMENT = 'Admin';

-- Q-16. Write an SQL query to print details of the Workers whose FIRST_NAME contains ‘a’.
SELECT * FROM worker WHERE FIRST_NAME LIKE '%a%';

-- Q-17. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘a’.
SELECT * FROM worker WHERE FIRST_NAME LIKE '%a';

-- Q-18. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘h’ and contains six alphabets.
SELECT * FROM worker WHERE FIRST_NAME LIKE '______h';

-- Q-19. Write an SQL query to print details of the Workers whose SALARY lies between 100000 and 500000.
SELECT * FROM worker WHERE SALARY BETWEEN 100000 AND 500000;	

-- Q-20. Write an SQL query to print details of the Workers who have joined in Feb’2014.
SELECT * FROM worker WHERE YEAR(JOINING_DATE) = 2014 AND MONTH(JOINING_DATE) = 02;

-- Q-21. Write an SQL query to fetch the count of employees working in the department ‘Admin’.
SELECT count(DEPARTMENT) FROM worker WHERE DEPARTMENT = 'Admin';

-- Q-22. Write an SQL query to fetch worker names with salaries >= 50000 and <= 100000.
SELECT CONCAT(FIRST_NAME , ' ', LAST_NAME ) AS WORKER_NAME , SALARY FROM WORKER WHERE SALARY >= 50000 AND SALARY<= 100000;

SELECT CONCAT(FIRST_NAME , '', LAST_NAME ) AS WORKER_NAME , SALARY
FROM worker WHERE WORKER_ID IN (SELECT WORKER_ID FROM WORKER WHERE SALARY BETWEEN 50000 AND 100000);

-- Q-23. Write an SQL query to fetch the no. of workers for each department in the descending order.
SELECT COUNT(WORKER_ID),DEPARTMENT FROM WORKER GROUP BY DEPARTMENT ORDER BY DEPARTMENT DESC ;

-- Q-24. Write an SQL query to print details of the Workers who are also Managers.
-- METHOD 1
SELECT concat(FIRST_NAME,' ', LAST_NAME) AS WORKER_NAME, w.WORKER_ID, t.WORKER_TITLE 
FROM WORKER W JOIN title t ON w.WORKER_ID = t.WORKER_REF_ID 
WHERE WORKER_TITLE = 'Manager';
;
-- METHOD 2
SELECT DISTINCT W.FIRST_NAME, T.WORKER_TITLE
FROM Worker W
INNER JOIN Title T
ON W.WORKER_ID = T.WORKER_REF_ID
AND T.WORKER_TITLE in ('Manager');

-- Q-25. Write an SQL query to fetch duplicate records having matching data in some fields of a table.
SELECT WORKER_TITLE, AFFECTED_FROM, COUNT(*)
FROM Title
GROUP BY WORKER_TITLE, AFFECTED_FROM
HAVING COUNT(*) > 1;

-- Q-26. Write an SQL query to show only odd rows from a table.
SELECT * FROM worker WHERE mod(WORKER_ID, 2)<>0; 

-- Q-27. Write an SQL query to show only even rows from a table.
SELECT * FROM WORKER WHERE mod(WORKER_ID, 2) = 0 ; 

-- Q-28. Write an SQL query to clone a new table from another table.
SELECT * INTO Workerclone FROM worker;

-- Q-29. Write an SQL query to fetch intersecting records of two tables.
-- D O U B T 

-- Q-30. Write an SQL query to show records from one table that another table does not have.
-- D O U B T 

-- Q-31. Write an SQL query to show the current date and time.
SELECT CURDATE();
SELECT NOW();


-- Q-32. Write an SQL query to show the top n (say 10) records of a table.
SELECT * FROM worker ORDER BY SALARY DESC LIMIT 10;

-- Q-33. Write an SQL query to determine the nth (say n=5) highest salary from a table.
SELECT * FROM worker ORDER BY SALARY DESC LIMIT 5;

-- Q-34. Write an SQL query to determine the 5th highest salary without using TOP or limit method.
SELECT DISTINCT SALARY , FIRST_NAME FROM worker;

-- Q-35. Write an SQL query to fetch the list of employees with the same salary.
SELECT * FROM worker AS  w1 WHERE 4 = (SELECT COUNT(DISTINCT SALARY) FROM worker w2 WHERE  w2.salary >  w1.salary);

-- Q-36. Write an SQL query to show the second highest salary from a table.
SELECT MAX(SALARY) FROM worker WHERE SALARY < (SELECT MAX(SALARY) FROM worker);
SELECT DISTINCT SALARY FROM worker ORDER BY SALARY DESC;

-- Q-37. Write an SQL query to show one row twice in results from a table.
SELECT FIRST_NAME, LAST_NAME, DEPARTMENT FROM worker w WHERE DEPARTMENT = 'HR' 
UNION ALL
SELECT FIRST_NAME, LAST_NAME, DEPARTMENT FROM worker w1 WHERE DEPARTMENT = 'HR';

-- Q-38. Write an SQL query to fetch intersecting records of two tables.


-- Q-39. Write an SQL query to fetch the first 50% records from a table.
SELECT * FROM worker WHERE WORKER_ID <= (SELECT COUNT(WORKER_ID)/2 FROM worker);

-- Q-40. Write an SQL query to fetch the departments that have less than five people in it.
SELECT DEPARTMENT, COUNT(WORKER_ID) AS NO_OF_WORKER FROM WORKER GROUP BY DEPARTMENT HAVING COUNT(WORKER_ID) < 5;
SELECT DEPARTMENT, COUNT(WORKER_ID) as 'Number of Workers' FROM Worker GROUP BY DEPARTMENT HAVING COUNT(WORKER_ID) < 5;

-- Q-41. Write an SQL query to show all departments along with the number of people in there.
SELECT DEPARTMENT, COUNT(WORKER_ID) AS 'No of worker' FROM WORKER GROUP BY DEPARTMENT;

-- Q-42. Write an SQL query to show the last record from a table.
SELECT * FROM WORKER ORDER BY WORKER_ID DESC LIMIT 1 ;
Select * from Worker where WORKER_ID = (SELECT max(WORKER_ID) from Worker);

-- Q-43. Write an SQL query to fetch the first row of a table.
SELECT * FROM WORKER ORDER BY WORKER_ID  LIMIT 1 ;
SELECT * FROM WORKER WHERE WORKER_ID = (SELECT MIN(WORKER_ID) FROM WORKER);

-- Q-44. Write an SQL query to fetch the last five records from a table.
SELECT * FROM WORKER ORDER BY WORKER_ID  LIMIT 5 ;
-- * DOUBT
SELECT * FROM Worker WHERE WORKER_ID <=5
UNION
SELECT * FROM (SELECT * FROM Worker W order by W.WORKER_ID DESC) AS W1 WHERE W1.WORKER_ID <=5;

-- Q-45. Write an SQL query to print the name of employees having the highest salary in each department.
SELECT MAX(SALARY), FIRST_NAME, LAST_NAME, DEPARTMENT FROM WORKER GROUP BY DEPARTMENT;

SELECT t.DEPARTMENT,t.FIRST_NAME,t.Salary from(SELECT max(Salary) as TotalSalary,DEPARTMENT from Worker group by DEPARTMENT) as TempNew 
Inner Join Worker t on TempNew.DEPARTMENT=t.DEPARTMENT 
 and TempNew.TotalSalary=t.Salary;

-- Q-46. Write an SQL query to fetch three max salaries from a table.
SELECT DISTINCT SALARY , FIRST_NAME, LAST_NAME, DEPARTMENT FROM WORKER ORDER BY SALARY DESC LIMIT 3;
SELECT distinct Salary from worker a WHERE 3 >= (SELECT count(distinct Salary) from worker b WHERE a.Salary <= b.Salary) order by a.Salary desc;
SELECT COUNT(DISTINCT SALARY) FROM WORKER;

-- Q-47. Write an SQL query to fetch three min salaries from a table.
SELECT distinct Salary from worker a WHERE 3 >= (SELECT count(distinct Salary) from worker b WHERE a.Salary >= b.Salary) order by a.Salary desc;

-- Q-48. Write an SQL query to fetch nth max salaries from a table.
SELECT distinct Salary from worker a WHERE n >= (SELECT count(distinct Salary) from worker b WHERE a.Salary <= b.Salary) order by a.Salary desc;
-- Q-49. Write an SQL query to fetch departments along with the total salaries paid for each of them.
 SELECT DEPARTMENT, sum(Salary) from worker group by DEPARTMENT;

-- Q-50. Write an SQL query to fetch the names of workers who earn the highest salary.
SELECT FIRST_NAME, SALARY from Worker WHERE SALARY=(SELECT max(SALARY) from Worker);
SELECT FIRST_NAME, SALARY FROM worker WHERE SALARY = (SELECT MAX(SALARY) FROM worker);
