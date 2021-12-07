# CTF

# SEEDS Labs

## Task 1: Get Familiar with SQL Statements

- Firstly, we have done the database setup using Docker and opened a shell from the respective MySQL container, by inputting the correct user and password, through the command `mysql -u root -pdees`.

- Secondly, still in the opened shell we loaded the existing database through the command `use sqllab_users`.

- Finaly, we printed the private information of employee Alice using the following SQL statement `SELECT * from credential where Name="Alice";`. This step is shown in the following print screen:


