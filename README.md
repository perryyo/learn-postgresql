
###learn-postgresql
Learn how to use PostgreSQL to store your relational data

### Commands
Once you are serving the database from your computer

- To change db
`\connect database_name;`

- To see the tables in the database
`\d;`

- To select (and show in terminal) all tables
`select * from table_name`


- To make a table
`CREATE TABLE table_name (col_name1, col_name2)`

- To add a row
`INSERT INTO table_name ( col_name )
VALUES ( col_value)`
col_name only require if only some of the cols are being filled out

- To edit a column to a table 
`ALTER TABLE table_name
  ALTER COLUMN column_name SET DEFAULT expression`

- To add a column to a table 
`ALTER TABLE table_name
  ADD COLUMN column_name data_type`

- To find the number of instances where the word “Day” is present in the title of a table
`SELECT count(title) FROM table_name WHERE title LIKE '%Day%’;`

- To delete a row in a table
`DELETE FROM table_name
  WHERE column_name = ‘hello';`





Postgresql follows the SQL convention of calling relations TABLES, attributes COLUMNs and tuples ROWS

**Transaction**
All or nothing, if something fails the other commands are rolled back like nothing happened

**Reference**
When a table is being created you can reference a column in another table to make sure any value which is added to that column exists in the referenced table.

`CREATE TABLE cities (
  name text NOT NULL,
  postal_code varchar(9) CHECK (postal_code <> ''),
  country_code char(2) REFERENCES countries,
  PRIMARY KEY (country_code, postal_code)
);`

“<>” means not equal


**Join reads**
You can join tables together when reading them,

**Inner Join**
Joins together two tables by specifying a column in each to join them by i.e.

`SELECT cities.*, country_name
  FROM cities INNER JOIN countries
  ON cities.country_code = countries.country_code;`

This will select all of the columns in both the countries and cities tables the data, the rows are matched up by country_code.

**Grouping**
You can put rows into groups where the group is defined by a shared value in a particular column.

`SELECT venue_id, count(*)
  FROM events
  GROUP BY venue_id;`

This will group the rows together by the venue_id, count is then performed on each of the groups.
