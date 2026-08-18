## August 17, 2026 - SQLBolt Session 1 - Morning 

Practiced Lesson 1 --> Queries 

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

## August 17, 2026 - SQLBolt Session 2 - Afternoon

Practiced Lesson 2 - Queries with Constraints

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

## August 18, 2026 - SQL Session 3

Lesson 3 - Queries with Constraints (cont)

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




