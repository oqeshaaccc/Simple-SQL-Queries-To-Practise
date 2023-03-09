
# simple_sql_queries_practise
Movies.csv has Table Movies
********************************************************************************
1. Write a query in SQL to find the name and year of the movies.
2. Write a query in SQL to find the year when the movie American Beauty
released.
3. Write a query in SQL to find the movie which was released in the year
1999.
4. Write a query in SQL to find the movies which was released before 1998. 
5. Write a query in SQL to return the name of all reviewers and name of
movies together in a single list.
6. Write a query in SQL to find the name of all reviewers who have rated 7 or
more stars to their rating.
7. Write a query in SQL to find the titles of all movies that have no ratings.
8. Write a query in SQL to find the titles of the movies with ID 905, 907, 917.
9. Write a query in SQL to find the list of all those movies with year which
include the words Boogie Nights.

************************************************************************
Solution
************************************************************************

        select DISTINCT(mov_name), mov_year from Movies;

        SELECT mov_year from Movies where mov_name="American Beauty";

        SELECT * from Movies where mov_year < 1999;

        SELECT * from Movies where mov_year < 1998;

        SELECT mov_name, rev_name from Movies;

        SELECT rev_name FROM Movies where rev_stars >=7;

        SELECT * from Movies Where num_o_ratings is null;

        select * from Movies where id= 905 or id= 907 or id=917;

        select * from Movies where  mov_name  like '%Boogie Nights%';


*****************************************************************************************************


#lap-sql-range-set-order-group.txt has some more complex queries on Employees and Departments tables


SQL-Query-Exersise


        /*Retrieve all employees whose address is in Elgin,IL.*/
        select * from EMPLOYEES  WHERE ADDRESS like '%Elgin,IL%';

        /*Retrieve all employees who were born during the 1970's.*/
        select * from Employees Where year(B_DATE) between 1970 AND 1979;

        /*Retrieve all employees in department 5 whose salary is between 60000 and 70000.*/
        select * from EMPLOYEES Where dep_ID =5 And SALARY between 60000 AND 70000;

        /*Retrieve a list of employees ordered by department ID.*/
        select * from EMPLOYEES ORDER BY dep_id;

        /*Retrieve a list of employees ordered in descending order by department ID and within each department ordered alphabetically in descending order by last name.*/
        SELECT * FROM EMPLOYEES ORDER BY dep_id DESC, L_NAME DESC;

        /*In SQL problem 2 (Exercise 2 Problem 2), use department name instead of department ID. Retrieve a list of employees ordered by department name, and within each department ordered alphabetically in descending order by last name.*/
        SELECT D.DEP_NAME , E.F_NAME, E.L_NAME FROM EMPLOYEES as E, DEPARTMENTS as D WHERE E.DEP_ID = D.DEPT_ID_DEP ORDER BY D.DEP_NAME, E.L_NAME DESC;

        /*For each department ID retrieve the number of employees in the department.*/
        SELECT DEP_ID, COUNT(*) FROM EMPLOYEES GROUP BY DEP_ID;

        /*For each department retrieve the number of employees in the department, and the average employee salary in the department..*/
        select dep_id, count(*), avg(salary) from EMPLOYEES GROUP BY DEP_ID;

        /*Label the computed columns in the result set of SQL problem 2 (Exercise 3 Problem 2) as NUM_EMPLOYEES and AVG_SALARY.*/
        select dep_id, count(*) AS NUM_EMPLOYEES, avg(salary) AS AVG_SALARY from EMPLOYEES GROUP BY DEP_ID;

        /*In SQL problem 3 (Exercise 3 Problem 3), order the result set by Average Salary..*/
        select dep_id, count(*) AS NUM_EMPLOYEES, avg(salary) AS AVG_SALARY from EMPLOYEES GROUP BY DEP_ID ORDER BY AVG_SALARY;

        /*In SQL problem 4 (Exercise 3 Problem 4), limit the result to departments with fewer than 4 employees.*/
        select dep_id, count(*) AS NUM_EMPLOYEES, avg(salary) AS AVG_SALARY from EMPLOYEES GROUP BY DEP_ID HAVING count(*) < 4 ORDER BY AVG_SALARY;



****************************************************************************************************
----------------------------- Exersise 1 Queries Using functions ---------------------------------------

    -- Query A1: Enter a function that calculates the total cost of all animal rescues in the PETRESCUE table.
    select sum(COST) from PETRESCUE;

    -- Query A2: Enter a function that displays the total cost of all animal rescues in the PETRESCUE table in a column called SUM_OF_COST.
    select sum(COST) from PETRESCUE as sum_of_cost;

    -- Query A3: Enter a function that displays the maximum quantity of animals rescued.
    select max(QUANTITY) from PETRESCUE;

    -- Query A4: Enter a function that displays the average cost of animals rescued.
    select avg(COST) from PETRESCUE;

    -- Query A5: Enter a function that displays the average cost of rescuing a dog.
    select avg(COST) from PETRESCUE where lower(ANIMAL) = 'dog';

----------------------------- Exersise 2 Queries Using functions ---------------------------------------

    -- Query B1: Enter a function that displays the rounded cost of each rescue.
    select round(COST) from PETRESCUE;

    -- Query B2: Enter a function that displays the length of each animal name.
    select LENGTH(ANIMAL) from PETRESCUE;

    -- Query B3: Enter a function that displays the animal name in each rescue in uppercase.
    select upper(ANIMAL) from PETRESCUE;

    -- Query B4: Enter a function that displays the animal name in each rescue in uppercase without duplications.
    select distinct(upper(ANIMAL)) from PETRESCUE;

    -- Query B5: Enter a query that displays all the columns from the PETRESCUE table, where the animal(s) rescued are cats. Use cat in lower case in the query.
    select * from PETRESCUE where lower(ANIMAL) = 'cat';

----------------------------- Exersise 3 Queries Using functions ---------------------------------------

    -- Query C1: Enter a function that displays the day of the month when cats have been rescued.
    select DAY(RESCUEDATE) from PETRESCUE;

    -- Query C2: Enter a function that displays the number of rescues on the 5th month.
    select SUM(QUANTITY) from PETRESCUE where MONTH(RESCUEDATE) = 05;

    -- Query C3: Enter a function that displays the number of rescues on the 14th day of the month.
    select SUM(QUANTITY) from PETRESCUE where DAY(RESCUEDATE) = 14;

    -- Query C4: Animals rescued should see the vet within three days of arrivals. Enter a function that displays the third day from each rescue.
    select (RESCUEDATE + 3 DAYS) as SHOULD_SEE_THE_VET_ON from PETRESCUE;

    -- Query C5: Enter a function that displays the length of time the animals have been rescued; the difference between today’s date and the rescue date.
    select (CURRENT_DATE - RESCUEDATE) as NUMBER_OF_DAYS_SINCE_RESCUED from PETRESCUE;

    select * from petrescue;



