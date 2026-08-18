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

	List all directors of pixar movies (alphabetically) without duplicates
	SELECT DISTINCT director 
	FROM movies
	ORDER BY director ASC;

	List the last 4 Pixar movies released (ordered from most recent to least)
	SELECT title, year
	FROM movies
	ORDER BY year DESC
	LIMIT 4;

	List the first five pixar movies sorted alphabetically
	SELECT title
	FROM movies
	ORDER BY title ASC
	LIMIT 5; 

	List the next 5 pixar movies sorted alphabetically
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

	List all the cities west of Chicago, order from west to East
	SELECT city, longitude
	FROM north_american_cities
	WHERE longitude < -87.629798
	ORDER BY longitude ASC;

	List the two largest cities in Mexico by population 
	SELECT city, population 
	FROM north_american_cities
	WHERE country LIKE “Mexico”
	ORDER BY population DESC
	LIMIT 2;

	List the 3rd and fourth largest cities by population inn the US
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
	
	Find the domestic and international sales for each movie
	SELECT title, domestic_sales, international_sales
	FROM movies
	JOIN boxoffice
	ON movies.id = boxoffice.movie_id

	Show sales numbers for each movie that did better internationally than domestically
	SELECT title, domestic_sales, international_sales
	FROM movies
	JOIN boxoffice
	ON movies.id = boxoffice.movie_id
	WHERE international_sales > domestic_sales; 
	
	List all the movies by their rankings in descending order
	SELECT title, ranking
	FROM movies
	JOIN boxoffice
	ON movies.id = boxoffice.movie_id
	ORDER BY rating DESC; 

	



