
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
        
        -- Execute a failing query (i.e. one which gives an error) to retrieve all employees records whose salary is lower than the average salary.
        -- The wrong way -> select * from EMPLOYEES where SALARY > avg(SALARY); 

        -- Execute a working query using a sub-select to retrieve all employees records whose salary is lower than the average salary.
        select * from EMPLOYEES where SALARY > (select avg(SALARY) from EMPLOYEES); 

        -- Execute a failing query (i.e. one which gives an error) to retrieve all employees records with EMP_ID, SALARY and maximum salary as MAX_SALARY in every row.
        -- The wrong way -> select EMP_ID, SALARY, MAX(SALARY) AS MAX_SALARY from EMPLOYEES; 

        -- Execute a Column Expression that retrieves all employees records with EMP_ID, SALARY and maximum salary as MAX_SALARY in every row.
        select EMP_ID, SALARY, (SELECT max(SALARY) as MAX_SALARY from EMPLOYEES) from EMPLOYEES;

        -- Execute a Table Expression for the EMPLOYEES table that excludes columns with sensitive employee data (i.e. does not include columns: SSN, B_DATE, SEX, ADDRESS, SALARY).
        select * from (SELECT EMP_ID, F_NAME, L_NAME, DEP_ID from EMPLOYEES) AS EMP4ALL;



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
    
    ********************************************************************************************
    
    ------------------- Accessing Multiple Tables with Sub-Queries ------------------
    
    
        -- Retrieve only the EMPLOYEES records that correspond to jobs in the JOBS table.
        select * from EMPLOYEES from where job_id in (select JOB_IDENT from jobs);

        -- Retrieve only the list of employees whose JOB_TITLE is Jr. Designer.
        select EMP_ID from EMPLOYEES Where JOB_ID in (select JOB_IDENT from JOBS where JOB_TITLE = 'Jr. Designer');

        -- Retrieve JOB information and who earn more than $70,000.
        SELECT JOB_TITLE, MIN_SALARY,MAX_SALARY,JOB_IDENT from jobs where JOB_IDENT IN(select JOB_ID from employees where SALARY > 70000);
        -- Retrieve JOB information and who earn more than $70,000. --- Another way of thinking of it ---
        SELECT EMP_ID , SALARY , JOB_ID , JOB_TITLE from Employees , jobs where JOB_ID in(SELECT JOB_ID from Employees where Salary > 70000);

        -- Retrieve JOB information and whose birth year is after 1976.
        SELECT * FROM JOBS WHERE JOB_IDENT IN (SELECT JOB_ID FROM EMPLOYEES WHERE YEAR(B_DATE)> 1976);

        --Retrieve JOB information for female employees whose birth year is after 1976.
        SELECT * FROM JOBS WHERE JOB_IDENT IN (SELECT JOB_ID FROM EMPLOYEES WHERE SEX = 'F');

        ------------------- Accessing Multiple Tables with Implicit Joins ------------------


        -- Perform an implicit cartesian/cross join between EMPLOYEES and JOBS tables.
        SELECT * FROM EMPLOYEES, JOBS;

        -- Retrieve only the EMPLOYEES records that correspond to jobs in the JOBS table.
        SELECT * FROM EMPLOYEES , JOBS WHERE JOB_ID = JOB_IDENT;
        SELECT * FROM EMPLOYEES , JOBS WHERE EMPLOYEES.JOB_ID = JOBS.JOB_IDENT; -- SAMEA

        -- Redo the previous query, using shorter aliases for table names.
        SELECT * FROM EMPLOYEES E, JOBS J WHERE E.JOB_ID = J.JOB_IDENT; 

        -- Redo the previous query, but retrieve only the Employee ID, Employee Name and Job Title.
        SELECT EMP_ID, F_NAME, L_NAME, JOB_TITLE FROM EMPLOYEES E, JOBS J WHERE E.JOB_ID = J.JOB_IDENT; 

        -- Redo the previous query, but specify the fully qualified column names with aliases in the SELECT clause.
        SELECT E.EMP_ID,E.F_NAME,E.L_NAME, J.JOB_TITLE from EMPLOYEES E, JOBS J where E.JOB_ID = J.JOB_IDENT;

        SELECT * FROM EMPLOYEES;
        
        
        ******************************************************************************************************
        The following sql queries are available in moreexecsise.txt
        ******************************************************************************************************
        --1- Write SQL query to sum all the funding AmountinUSD, where City location equals “Bengaluru”
        SELECT SUM(AmountinUSD) FROM indian_startup_funding WHERE CityLocation = "Bengaluru";

        --2- Write SQL query to sort the table by startup name DESC
        select * from indian_startup_funding ORDER by lower(StartupName) DESC;

        --3- Write SQL query to sum all the funding AmountinUSD, where City location equals “Bengaluru” and AmountinUSD>380000
        SELECT SUM(AmountinUSD) FROM indian_startup_funding WHERE CityLocation = "Bengaluru" AND AmountinUSD > 830000;

        --4- Write SQL query to get all CityLocations that has an AmountinUSD >380000
        SELECT CityLocation FROM indian_startup_funding WHERE AmountinUSD > 380000;

        --5- Write SQL query to get only unique CityLocations that has an AmountinUSD >380000
        SELECT DISTINCT(CityLocation) FROM indian_startup_funding WHERE AmountinUSD > 380000;

        --6- Write SQL query to get all StartupNames where AmountinUSD<380000
        SELECT StartupName FROM indian_startup_funding WHERE AmountinUSD > 380000;

        --7- Write SQL query to sort the output from the previous question DESC
        SELECT StartupName FROM indian_startup_funding WHERE AmountinUSD > 380000 ORDER BY StartupName DESC;

        --8- Write SQL query to get the City location that has the maximum funding amount “Note that is the data is not cleaned properly you will get non logical result
        SELECT CityLocation, AmountinUSD FROM indian_startup_funding WHERE  AmountinUSD = (SELECT MAX(AmountinUSD)FROM indian_startup_funding); -- GIVES UNKNOWN
        select CityLocation, max(AmountinUSD) from indian_startup_funding where lower(AmountinUSD) not in ('undisclosed','unknown');

        --9- Write SQL query to get the total funding AmountinUSD for each IndustryVertical
        SELECT IndustryVertical, SUM(AmountinUSD) FROM indian_startup_funding GROUP BY IndustryVertical;

        --10- Write SQL query to get the total funding AmountinUSD for each IndustryVertical that starts with letter “A”
        SELECT IndustryVertical, SUM(AmountinUSD) AS TotalFunding FROM indian_startup_funding WHERE IndustryVertical LIKE 'A%' GROUP BY IndustryVertical; --CHATGPT ANSWER
        SELECT IndustryVertical, SUM(AmountinUSD) FROM indian_startup_funding GROUP BY IndustryVertical HAVING  IndustryVertical LIKE 'A%'; --MY ANSWER

        --11- Write SQL query to get the total funding AmountinUSD for each IndustryVertical that starts with letter “A” and sort the output DESC by the total AmountinUSD
        SELECT IndustryVertical, SUM(AmountinUSD) FROM indian_startup_funding GROUP BY IndustryVertical HAVING  IndustryVertical LIKE 'A%' ORDER by IndustryVertical desc;

        --12- Write SQL query to count all the start_ups in the Education field
        SELECT COUNT(DISTINCT (StartupName)) FROM indian_startup_funding;

        --13- Write SQL query to count all the start_Ups in the E-Commerce field
         SELECT COUNT(DISTINCT (StartupName)) FROM indian_startup_funding WHERE IndustryVertical = "E-Commerce";

        --14- Write SQL query to count all the start_Ups in the E-Commerce field, where city location equals “Bengaluru”
        SELECT COUNT(DISTINCT (StartupName)) FROM indian_startup_funding WHERE IndustryVertical = "E-Commerce" AND CityLocation = "Bengaluru";

        --15- For each Industry Vertical find the total funding amount
        SELECT DISTINCT(IndustryVertical), SUM(AmountinUSD) FROM indian_startup_funding GROUP BY IndustryVertical;

        --16- For each Industry Vertical find the total funding amount as “Total_fund” and the average 
        --funding amount as “Avg_Fund”. In this question provide two answer 1- using group by Industry
        --Vertical, 2- using sub_queries
        SELECT DISTINCT(IndustryVertical), SUM(AmountinUSD) AS TOTAL_FUN, avg(AmountinUSD) AS Avg_Fund FROM indian_startup_funding GROUP BY IndustryVertical;

        -- 17- Write SQL query to get the minimum value of funding for the “Uniphore” start_up
        SELECT StartupName, MIN(AmountinUSD) FROM indian_startup_funding WHERE StartupName = "Uniphore";

        -- 18- Write SQL query to get the length of the city location names
        SELECT CityLocation, length(CityLocation) FROM indian_startup_funding;

        -- 19- Write SQL query to convert start_ups names into uppercase if the funding amount is >380,000
        SELECT upper(StartupName) FROM indian_startup_funding;

        -- 20- Write SQL query to select distinct industry vertical names, knowing that names are mix of lowercase and uppercase values.
        SELECT DISTINCT(upper(IndustryVertical)) FROM indian_startup_funding;
        
********************************************************************************************************************************
More Complex Queries - creating procedures
*********************************************************************************************************************************

        Procedures
        _________________________
        1- create table pet
        -- Drop the table in case it exists

        DROP TABLE PETSALE;

        -- Create the table

        CREATE TABLE PETSALE (
                ID INTEGER NOT NULL,
                ANIMAL VARCHAR(20),
                SALEPRICE DECIMAL(6,2),
                SALEDATE DATE,
                QUANTITY INTEGER,
                PRIMARY KEY (ID)
                );

        -- Insert sample data into the table

        INSERT INTO PETSALE VALUES
        (1,'Cat',450.09,'2018-05-29',9),
        (2,'Dog',666.66,'2018-06-01',3),
        (3,'Parrot',50.00,'2018-06-04',2),
        (4,'Hamster',60.60,'2018-06-11',6),
        (5,'Goldfish',48.48,'2018-06-14',24);

        -- Retrieve all records from the table

        SELECT * FROM PETSALE;


        ___________________________________________________
        2- create the procedure
        --#SET TERMINATOR @
        CREATE PROCEDURE RETRIEVE_ALL       -- Name of this stored procedure routine

        LANGUAGE SQL                        -- Language used in this routine 
        READS SQL DATA                      -- This routine will only read data from the table

        DYNAMIC RESULT SETS 1               -- Maximum possible number of result-sets to be returned to the caller query

        BEGIN 

            DECLARE C1 CURSOR               -- CURSOR C1 will handle the result-set by retrieving records row by row from the table
            WITH RETURN FOR                 -- This routine will return retrieved records as a result-set to the caller query

            SELECT * FROM PETSALE;          -- Query to retrieve all the records from the table

            OPEN C1;                        -- Keeping the CURSOR C1 open so that result-set can be returned to the caller query

        END
        @                                   -- Routine termination character
        ________________________________________________________
        3- call it

        CALL RETRIEVE_ALL;      -- Caller query

        ___________________________________________________
        ____________________________________________________________________________________________________
        Another procedure
        ____________________________
        --#SET TERMINATOR @
        CREATE PROCEDURE UPDATE_SALEPRICE ( 
            IN Animal_ID INTEGER, IN Animal_Health VARCHAR(5) )     -- ( { IN/OUT type } { parameter-name } { data-type }, ... )

        LANGUAGE SQL                                                -- Language used in this routine
        MODIFIES SQL DATA                                           -- This routine will only write/modify data in the table

        BEGIN 

            IF Animal_Health = 'BAD' THEN                           -- Start of conditional statement
                UPDATE PETSALE
                SET SALEPRICE = SALEPRICE - (SALEPRICE * 0.25)
                WHERE ID = Animal_ID;

            ELSEIF Animal_Health = 'WORSE' THEN
                UPDATE PETSALE
                SET SALEPRICE = SALEPRICE - (SALEPRICE * 0.5)
                WHERE ID = Animal_ID;

            ELSE
                UPDATE PETSALE
                SET SALEPRICE = SALEPRICE
                WHERE ID = Animal_ID;

            END IF;                                                 -- End of conditional statement

        END
        @                                                           -- Routine termination character
        ________________________________________________
        call it

        CALL RETRIEVE_ALL;

        CALL UPDATE_SALEPRICE(1, 'BAD');        -- Caller query

        CALL RETRIEVE_ALL;


        ______________________________
        call it again
        CALL RETRIEVE_ALL;

        CALL UPDATE_SALEPRICE(3, 'WORSE');      -- Caller query

        CALL RETRIEVE_ALL;

        ____________________________
        Drop the procedure
        DROP PROCEDURE UPDATE_SALEPRICE;
*********************************************************************************************************************************
More Complex Queries - Inner, Left Outer, Right Outer, Full Outer Join
*********************************************************************************************************************************
        --1-Select the names and job start dates of all employees who work for the department number 5.
        select E.F_NAME,E.L_NAME, JH.START_DATE 
        from EMPLOYEES as E 
        INNER JOIN JOB_HISTORY as JH on E.EMP_ID=JH.EMPL_ID 
        where E.DEP_ID ='5';	


        --2-Select the names, job start dates, and job titles of all employees who work for the department number 5.
        select E.F_NAME,E.L_NAME, JH.START_DATE, J.JOB_TITLE 
        from EMPLOYEES as E 
        INNER JOIN JOB_HISTORY as JH on E.EMP_ID=JH.EMPL_ID 
        INNER JOIN JOBS as J on E.JOB_ID=J.JOB_IDENT
        where E.DEP_ID ='5';


        --3-Perform a Left Outer Join on the EMPLOYEES and DEPARTMENT tables and select employee id, last name, department id and department name for all employees.
        select E.EMP_ID,E.L_NAME,E.DEP_ID,D.DEP_NAME
        from EMPLOYEES AS E 
        LEFT OUTER JOIN DEPARTMENTS AS D ON E.DEP_ID=D.DEPT_ID_DEP;


        --4-Re-write the previous query but limit the result set to include only the rows for employees born before 1980.
        select E.EMP_ID,E.L_NAME,E.DEP_ID,D.DEP_NAME
        from EMPLOYEES AS E 
        LEFT OUTER JOIN DEPARTMENTS AS D ON E.DEP_ID=D.DEPT_ID_DEP 
        where YEAR(E.B_DATE) < 1980;

        --5-Re-write the previous query but have the result set include all the employees but department names for only the employees who were born before 1980.
        select E.EMP_ID,E.L_NAME,E.DEP_ID,D.DEP_NAME
        from EMPLOYEES AS E 
        LEFT OUTER JOIN DEPARTMENTS AS D ON E.DEP_ID=D.DEPT_ID_DEP 
        AND YEAR(E.B_DATE) < 1980;

        --6-Perform a Full Join on the EMPLOYEES and DEPARTMENT tables and select the First name, Last name and Department name of all employees.
        select E.F_NAME,E.L_NAME,D.DEP_NAME
        from EMPLOYEES AS E 
        FULL OUTER JOIN DEPARTMENTS AS D ON E.DEP_ID=D.DEPT_ID_DEP;

        --7-Re-write the previous query but have the result set include all employee names but department id and department names only for male employees.
        select E.F_NAME,E.L_NAME,D.DEPT_ID_DEP, D.DEP_NAME
        from EMPLOYEES AS E 
        FULL OUTER JOIN DEPARTMENTS AS D ON E.DEP_ID=D.DEPT_ID_DEP AND E.SEX = 'M';
        ________________________________________________________________________________________________

        #List the case number, type of crime and community area for all crimes in community area number 18.
        %sql select CD.CASE_NUMBER,CD.PRIMARY_TYPE, CD.COMMUNITY_AREA_NUMBER \
        from CHICAGO_CRIME_DATA as CD \
        INNER JOIN CENSUS_DATA as CN on CD.COMMUNITY_AREA_NUMBER=CN.COMMUNITY_AREA_NUMBER \
        where CD.COMMUNITY_AREA_NUMBER =18;
        _____________________________________________________________________________________________
        #List all crimes that took place at a school. Include case number, crime type and community name.
        %sql select CD.CASE_NUMBER,CD.PRIMARY_TYPE, CN.COMMUNITY_AREA_NAME \
        from CHICAGO_CRIME_DATA as CD \
        LEFT OUTER JOIN CENSUS_DATA as CN on CD.COMMUNITY_AREA_NUMBER=CN.COMMUNITY_AREA_NUMBER \
        where lower(CD.LOCATION_DESCRIPTION) like '%school%';

        _____________________________________________________________________________________________
        #For the communities of Oakland, Armour Square, Edgewater and CHICAGO list the associated community_area_numbers and the case_numbers.
        %sql select CD.CASE_NUMBER,CD.PRIMARY_TYPE, CN.COMMUNITY_AREA_NAME \
        from CHICAGO_CRIME_DATA as CD \
        FULL OUTER JOIN CENSUS_DATA as CN on CD.COMMUNITY_AREA_NUMBER=CN.COMMUNITY_AREA_NUMBER \
        where lower(CN.COMMUNITY_AREA_NAME) in ('oakland', 'armour square', 'edgewater', 'chicago');








