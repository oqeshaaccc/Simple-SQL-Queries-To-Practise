
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


********************************* Queries Using functions ************************************;
----------------------------- Exersise 1 ---------------------------------------;
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

----------------------------- Exersise 2 ---------------------------------------;
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

----------------------------- Exersise 3 ---------------------------------------;
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



