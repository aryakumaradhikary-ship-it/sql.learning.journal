## August 17, 2026 - SQLBolt Session

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

Example Query: 

        Find the director of each film:
        SELECT director FROM movies; 

        Find the title and director of each film:
        SELECT title, director * FROM movies; 

        Find all the information about each film:
        SELECT * FROM movies;



