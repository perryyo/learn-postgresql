
###learn-postgresql
Learn how to use PostgreSQL to store your relational data

### Installation
Before you get started with using PostgreSQL, you'll have to install it.
Follow these steps to get started:

1. There are a couple of ways to install PostgreSQL. One of the easier ways to
get started is with Postgres.app. Navigate to http://postgresapp.com/ and then
click "Download":
![download](https://cloud.githubusercontent.com/assets/12450298/19641848/6d3cfa4a-99da-11e6-858f-3ff2ada026be.png)

2. Once it's finished downloading, double click on the file to unzip then move
the PostgreSQL elephant icon into your `applications` folder. Double click the
icon to launch the application.

3. You should see a new window launched that says "Welcome to Postgres". If it
says that it cannot connect to the postgres server this means that the DEFAULT
port is probably already in use. Make sure you don't have any other instances of
Postgres on your computer. Uninstall them if you do and then resume with these
steps. Click on the button that says "Open psql":
![open psql](https://cloud.githubusercontent.com/assets/12450298/19642044/463eceae-99db-11e6-8907-bb3a6cc532a7.png)

4. After clicking the button a new terminal window should open. You might see an
error that looks like: `psql: FATAL:  role "[your_username]" does not exist`.
This is because Postgres needs to be set up with a `Postgres` user. Type the
following into your terminal to switch the user and then type your password:

`sudo -u postgres '/Applications/Postgres.app/Contents/Versions/9.6/bin'/psql -p5432`

5. You should then see something in your terminal that looks like this:
![terminal](https://cloud.githubusercontent.com/assets/12450298/19642816/f8ac0c66-99de-11e6-87e2-db55e6abc27b.png)

6. You should now be all set up to start using PostgreSQL. For documentation on
command line tools etc see http://postgresapp.com/documentation/

### Create your first PostgreSQL database

1. To start PostgreSQL, type this command into the terminal:  
`sudo -u postgres psql`  
It's saying, "start the PostgreSQL server with the postgres admin user"

2. Next type this command into the PostgreSQL interface:  
`CREATE DATABASE test;`  
**NOTE:** Don't forget the semi-colon. If you do, useful error messages won't
show up.

3. To check that our database has been created, type `\l` into the psql prompt.
You should see something like this in your terminal:
![test db](https://cloud.githubusercontent.com/assets/12450298/19650613/ce278678-9a01-11e6-89ad-b124c0adcfe5.png)

### Create a user entry for your database

1. If you closed the PostgreSQL server, start it again with:  
`sudo -u postgres psql`  

2. To create a new user, type the following into the psql prompt:  
`CREATE USER test;`

3. Check that your user has been created. Type `\du` into the prompt. You should
see something like this:
![user](https://cloud.githubusercontent.com/assets/12450298/19650852/9c340708-9a02-11e6-8f06-75f1e30a86b3.png)
Users can be used to access the `psql` prompt. 

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
