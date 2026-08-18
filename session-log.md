## August 17, 2026 

SQL Bolt - Practiced Lesson 1 --> Queries 

Notes: 
- To retrieve data from SQL database, we need to write ‘SELECT’ statements → called queries
- Query: statement that declares what type of data we are looking for, where to find in the data    base
- Table in SQL is a type of entity, each row is an instance of that type, each column is common properties shared by all instances of the entity
- Select query for a specific columns:
       SELECT column, another_column,...
       FROM mytable;
- Select query for all columns:
       SELECT *
       FROM mytable; 

- Exercise: 

        Find the director of each film:
        SELECT director FROM movies; 

        Find the title and director of each film:
        SELECT title, director * FROM movies; 

        Find all the information about each film:
        SELECT * FROM movies;

---------

SQL Lesson 2 - Queries with Constraints

Notes: 
- Use WHERE clause to filter certain results from being returned
- Syntax:
	- SELECT column,...
	- FROM mytable
	- WHERE condition
		- AND/OR another_condition
- different types of condition examples:
	- col_name != 5
	- col_name BETWEEN 1.5 AND 10.5
	- col_name NOT BETWEEN 1 AND 10
	- col_name IN (2,4,6)
	- col_name NOT IN (1,3,5)

- Exercise:
  	
	Find movies with a row ID of 6:
	SELECT title
	FROM movies
	WHERE id = 6;

	Find the movies released between 2000 and 2010
	SELECT  title
	FROM movies
	WHERE year between 2000 AND 2010; 

	Find the movies not released between 2000 and 2010
	SELECT  title
	FROM movies
	WHERE year NOT BETWEEN 2000 AND 2010; 

	Find the first 5 Pixar movies and their release year:
	SELECT title, year
	FROM movies
	WHERE year <= 2003;

######################################

## August 18, 2026

SQL Lesson 3 - Queries with Constraints (cont)

- ways to filter columns based on column name:
	- col_name = “abc”
	- col_name != “abcd”
	- col_name LIKE “ABC” (case insensitive!)
	- col_name NOT LIKE “ABCD”
	- col_name LIKE “%AT%” → used anywhere in a string to match a sequence of zero or more 	characters → this code would match with “AT”, “ATTIC”, “CAT”, “BATS”
	- col_name LIKE “AN_” → matches with “AND” but not “AN”
	- col_name IN (“A”, “B”, “C”) → string exists in a list
	- col_name NOT IN (“D”, “E”, “F”) → string does not exist in a list

- Exercise:
	
	Find all the toy story movies:
	SELECT title
	FROM movies
	WHERE title LIKE “%TOY STORY%”; 

	Find all the movies directed by John Lasseter:
	SELECT title
	FROM movies
	WHERE director LIKE “JOHN LASSETER”

	Find all the movies  (and director) not directed by John Lasseter:
	SELECT title, director
	FROM movies
	WHERE director NOT LIKE “JOHN LASSESTER”

	Find all the WALL-* movies:
	SELECT * FROM movies
	WHERE title LIKE “WALL-_”;


------------

SQL Lesson 4 - Filtering and Sorting Queries

- use DISTINCT to discard duplicate rows
- syntax/how it looks:
	SELECT DISTINCT column, another_column,...
	FROM mytable
	WHERE condition(s); 
- ORDER BY clause lets you order based on ascending/descending:
	SELECT column, another_column
	FROM mytable
	WHERE condition(s)
	ORDER BY column ASC/DESC;
- LIMIT clause helps with reducing numbers of rows to return + OFFSET specifics where to begin counting the rows:
	SELECT column, another column,...
	FROM mytable
	WHERE condition(s)
	ORDER by column ASC/DESC
	LIMIT num_limit OFFSET num_offset;

- Exercise:

	List all directors of pixar movies (alphabetically) without duplicates:
	SELECT DISTINCT director 
	FROM movies
	ORDER BY director ASC;

	List the last 4 Pixar movies released (ordered from most recent to least):
	SELECT title, year
	FROM movies
	ORDER BY year DESC
	LIMIT 4;

	List the first five pixar movies sorted alphabetically:
	SELECT title
	FROM movies
	ORDER BY title ASC
	LIMIT 5; 

	List the next 5 pixar movies sorted alphabetically:
	SELECT title 
	FROM movies
	ORDER BY title ASC
	LIMIT 5 OFFSET 5;

------------

SQL Lesson 5 - Final Review

	List all the Canadian cities and their population:
	SELECT city, country, population
	FROM north_american_cities
	WHERE country LIKE “CANADA”;


	Order all the cities in the US by their latitude from North to South:
	SELECT city, country, latitude
	FROM north_american_cities
	WHERE country LIKE “UNITED STATES”
	ORDER BY latitude DESC;

	List all the cities west of Chicago, order from west to East:
	SELECT city, longitude
	FROM north_american_cities
	WHERE longitude < -87.629798
	ORDER BY longitude ASC;

	List the two largest cities in Mexico by population:
	SELECT city, population 
	FROM north_american_cities
	WHERE country LIKE “Mexico”
	ORDER BY population DESC
	LIMIT 2;

	List the 3rd and fourth largest cities by population in the US:
	SELECT city, population FROM north_american_cities
	WHERE country LIKE "United States"
	ORDER BY population DESC
	LIMIT 2 OFFSET 2;


------------

SQL Lesson 6: Multi-Table Queries with JOINs

- database normalization: minimizes duplicate data in a table + data can grow independently --> queries get complex + more risk of performance issues
- primary key: when tables share info about one entity, they need to have primary key that identifies the entity uniquely across the entire database --> usually is some type of integer 
- use the JOIN clause in a query to combine row data into different tables 
- INNER JOIN lets you match the rows from the first and second table that have the same key to create a row with the combined rows --> when writing it out, INNER JOIN is just JOIN



Exercise: two separate tables, one w/ id, title, director, year, length_minutes; other w/ movie_id, rating, domestic_sales, international_sales
	
	Find the domestic and international sales for each movie:
	SELECT title, domestic_sales, international_sales
	FROM movies
	JOIN boxoffice
	ON movies.id = boxoffice.movie_id

	Show sales numbers for each movie that did better internationally than domestically:
	SELECT title, domestic_sales, international_sales
	FROM movies
	JOIN boxoffice
	ON movies.id = boxoffice.movie_id
	WHERE international_sales > domestic_sales; 
	
	List all the movies by their rankings in descending order:
	SELECT title, ranking
	FROM movies
	JOIN boxoffice
	ON movies.id = boxoffice.movie_id
	ORDER BY rating DESC; 

	

------------

SQL Lesson 7: OUTER JOINs

- if tables have asymmetric data, use LEFT JOIN, RIGHT JOIN, or FULL JOIN
- LEFT JOIN includes rows from A regardless if matching row in B --> for joining table A to table B
- RIGHT JOIN includes rows from B regardless if matching row in A
- FULL JOIN, rows from both tables are kept, regardless of corresponding matching table

Exercise: one table with buildings (building_name & capacity), other table with (role, name, building, & years_employed)

	Find the list of all building that have employees:
	SELECT DISTINCT building
	FROM employees

	Find the list of all buildings and their capacity:
	SELECT building_name, capacity
	FROM buildings; 

	List all the building and the distinct employee roles in each building (including empty buildings)

	SELECT DISTINCT building_name, role
	FROM buildings
	LEFT JOIN employees 
	ON building_name = building


	--> left join is keeping everything from the building table, whether or not it finds a match in employees
        --> if building has employees, it matches building name to the building and then will pull the role
        --> if the building has no employees, the role column will simply be null 



------------

SQL Lesson 8: NULLs

- alternative vals for NULL is 0 for numerical data and empty strings for text data
- NULL vals are appropriate to leave as be if it will skew analysis
- you can test column if there are NULL vals --> use IS/IS NOT NULL

Exercise: same tables as the previous lesson
	
	Find the name & role of all employees that haven't been assigned a building:
	SELECT name, role, building
	FROM employees
	WHERE building IS NULL; 

	Find the names of buildings that hold no employees:
	SELECT DISTINCT building_name
	FROM buildings
	LEFT JOIN employees
	ON building_name = building
	WHERE role IS NULL;
	--> left join keeps all the buildings
	--> if building has no employees, role will come back as NULL




------------

SQL Lesson 9 - Queries w/ Expressions

- expressions are for complex logic on columns in queries
- use mathematical + string functions to alter values in the query
- when you use expressions, you should have a descriptive alias ~ AS


Exercise: one table w/ id, title, director, year, length_minutes; other table w/ movie_id, rating, domestic_sales, international_sales

	List all movies and their combined sales in millions of dollars
	SELECT title, (domestic_sales + international_sales) / 1000000 AS gross_sales_millions
	FROM movies
	JOIN boxoffice
	ON movies.id = boxoffice.movie_id;
	--> we add + divide and create a new gross_sales_millions column to display on our new query
	--> we join w/ boxoffice to display title + new column we just made


	List all the movies and their ratings in percent:
	SELECT title, rating * 10 AS ratings_percent
	FROM movies
	JOIN boxoffice
	ON movies.id = boxoffice.movie_id;
	--> multiply by 10 to convert to percentages, similar steps as the previous problem

	List all the movies that were released on even number years:
	SELECT title, year
	FROM movies
	JOIN boxoffice
	ON movies.id = boxoffice.movie_id
	WHERE year % 2 != 1; 

------------

SQL Lesson 10 - Queries w/ Aggregates (Part 1)

- aggregate functions summarizes information
- common aggregate functions:
	- COUNT: counts # of rows in group if no column name is specified (), otherwise will count the # of rows in the group that has no non-NULL values in specified column
	- MIN(column): returns the smallest numerical val in specified column for all rows in group
	- MAX(column): returns the largest numerical val in a specified column for all rows in the group
	- AVG(column): returns the average numerical val in a specified column for all rows in the group
	- SUM(column): returns the sum of all numerical values in a specified column for all rows in the group.

- you can also use the GROUP BY clause to group together rows with the same col vals


Exercise: one table with role, name, building, years_employed

	Find the longest time that an employee has been at the studio:
	SELECT name, MAX(years_employed)
	FROM employees; 

	For each role, find the average number of years employed by employees in that role:
	SELECT role, AVG(years_employed)
	FROM employees
	GROUP BY role; 

	Find the total number of employee years worked in each building:
	SELECT building, sum(years_employed)
	FROM employees
	GROUP BY building; 


------------

SQL Lesson 11 - Queries w/ Aggregates (Part 2)	

- GROUP BY is executed after WHERE clause
- HAVING clause allows us to filter rows
- order is: select, from, where, group by, rows


Exercise: table w/ role, name, building, years_employed

	Find the # of artists in the studio (without using a HAVING clause):
	SELECT role, COUNT(*) AS num_of_artists
	FROM employees
	WHERE role = "Artist"; 

	Find the number of employees of each role in the studio:
	SELECT role, COUNT(*)
	FROM employees,
	GROUP BY role; 

	Find the total number of years employed by all engineers:
	SELECT role, sum(years_employed)
	FROM employees
	WHERE role = "Engineer"; 

------------

SQL Lesson 12 - Order of Execution of a Query 

- order: SELECT, FROM, JOIN, ON, WHERE, GROUP BY, HAVING, ORDER BY (ASC/DESC), LIMIT, OFFSET; 
- group by should only be used when you have aggregate functions in your query


Exercise: one table w/ id, title, director, year, length_minutes; other w/ movie_id, rating, domestic_sales, international_sales

	Find the number of movies each director has directed:
	SELECT director, COUNT(id) AS num_movies
	FROM movies
	GROUP BY director; 
	
	Find the total domestic + international sales that can be attributed to each director
	SELECT director, SUM(domestic_sales + international_sales) AS all_movie_sales
	FROM movies
	INNER JOIN boxoffice
	ON movies.id = boxoffice.movie_id
	GROUP BY director; 
	--> inner join is connecting the movie table with the box office table via movie ids
	--> by doing so, we can create a total sales album per movie and then sum!


------------

SQL Lesson 13 - Inserting Rows

- database schema: what described the structure of each table & database types that each column can contain
- to insert data, we need INSERT statement --> ex: INSERT INTO mutable
						   VALUES(val_or_exp),...
- to add column: INSERT INTO boxoffice
		 (movie_id, rating, sales)
		 VALUES (2, 8.0, 8900000)

Exercise: one table w/id, title, director, year, length_minutes; other w/ movie_id, rating, domestic_sales, international_sales

	Add the studio's new production, Toy Story 4 w/ any director:
	INSERT INTO movies 
	VALUES(4, "Toy Story 4", "John Lasseter, 120); 
	
	Toy Story 4 has been released. It has a rating of 8.7, made 340M domestically, 270 internationally. Add this record to the BoxOfffice table:
	INSERT INTO boxoffice
	VALUES (4, 8.7, 340000000, 270000000); 
	

------------

SQL Lesson 14 - Updating Rows

- UPDATE statement to update rows; requires same data types in each column 
- always write the constraint first and test with a SELECT query to check that the correct rows are being updated

Exercise: 
	
	The director for a Bug's Life is incorrect, it was actually directed by John Lasseter:
	UPDATE movies
	SET director = "John Lasseter"
	WHERE title = "A Bug's Life";

	The year that Toy Story 2 came out is incorrect, it was actually released in 1999:
	UPDATE movies
	SET year = 1999
	WHERE title = "Toy Story 2";
	
	Both the title and director for Toy Story 8 is incorrect. Title should be Toy Story 3 & it was directed by Lee Unkrich:
	UPDATE movies
	SET title = "Toy Story 3", director = "Lee Unkrich"
	WHERE title = "Toy Story 8";


------------

SQL Lesson 15 - Deleting Rows

- use the DELETE statement to describe the table to act on, and the WEHRE clause to decide which row
- if you don't use the WHERE clause, all rows will be deleted!


Exercise:

	Database is getting too big. Remove all movies released before 2005:
	DELETE from movies
	WHERE year < 2005; 

	Andrew Stanton has left the studio, remove all movies directed by him:
	DELETE from movies
	WHERE director = "Andrew Stanton"; 


------------

SQL Lesson 16 - Creating Tables

- to create a new database, use the CREATE TABLE statement
- if a table with the same name already exists, then there may be an error --> use IF NOT EXISTS clause to bypass this
- table data types:
	- int
	- boolean
	- float/double/real
	- character, varchar, text
	- date, datetime
	- blob (where binary data can be stored)

- constraints:
	- primary key: vals in column are unique 
	- auto increment: for int vals, this vals s automatically filled in and incremented w/ each row insertion
	- unique: all vals have to be unique --> doesn't need to be a key for a row in the table
	- not null: inserted val can't be null
	- check: complex expression to test whether vals are valid
	- foreign key: checks whether val in one column matches another column

Exercise: 
	Create a new table named Database with the following columns: Name, a string (text) describing the name of the database; Version, a number (floating point) of the latest version of this database; download_count, an integer count of the number of times this database was downloaded

	CREATE TABLE database (
	name STRING, 
	version FLOAT,
	download_count INTEGER
	); 


------------

SQL Lesson 17 - Altering Tables

- ALTER TABLE clause lets you alter the table (pretty self explanatory!)
- you can drop columns but sometimes you may have to create a new table altogether
- to rename a table, you just use RENAME TO


Exercise: 
	Add a column called aspect_ratio with a float data type to restore the aspect ration each movie was released in: 	
	ALTER TABLE movies
	ADD column aspect_ratio FLOAT
	DEFAULT 0; 

	Add column named language w/ text data type to store language the movie was released in. Default language should be English: 

	ALTER TABLE movies
	ADD column language TEXT
	DEFAULT English;


------------

SQL Lesson 18 - Dropping Tables

- if you want to remove the entire table schema from the database, use DROP TABLE IF EXISTS


Exercise: one table w/ id, title, director, year, length_minutes; other w/ movie_id, rating, domestic_sales, international_sales

	Clean up by removing the movies table:
	DROP TABLE IF EXISTS movies; 

	Drop BoxOffice table as well: 
	DROP TABLE IF EXISTS boxoffice; 
	






