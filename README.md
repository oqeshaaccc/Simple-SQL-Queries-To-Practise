
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


#lap-sql-range-set-order-group.txt has some more complex queries on Employees and Departments tables
