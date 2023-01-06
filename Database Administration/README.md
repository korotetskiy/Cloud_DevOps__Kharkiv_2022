<h2>DevOps L1 course Database Administration Home Tasks</h2>
<head>
<h2>Part 1</h2>
<h3>1. Download MySQL server for your OS on VM.</br><head> 
2. Install MySQL server on VM.</h3>

```
$ sudo apt-get install mysql-server
```

<img src="https://github.com/korotetskiy/img/blob/main/db1.png">
<h3>3. Select a subject area and describe the database schema, (minimum 3 tables)</h3><img src="https://github.com/korotetskiy/img/blob/main/db3.png">
<h3>4. Create a database on the server through the console.</h3><img src="https://github.com/korotetskiy/img/blob/main/db2-1.png">
<h3>5. Fill in tables.</h3><img src="https://github.com/korotetskiy/img/blob/main/db4.png">
<h3>6. Construct and execute SELECT operator with WHERE, GROUP BY and ORDER BY.</h3><img src="https://github.com/korotetskiy/img/blob/main/db6.png">
<img src="https://github.com/korotetskiy/img/blob/main/db6-1.png">
<h3>7. Execute other different SQL queries DDL, DML, DCL.</h3>
<h4>Data Definition Language (DDL) -  CREATE,    ALTER,    DROP,   TRUNCATE</br>

```
    CREATE TABLE EMPLOYEE(Name CHAR, Email CHAR, DOB DATE);
    ALTER TABLE STU_DETAILS ADD(ADDRESS VARCHAR(20));
    ALTER TABLE STU_DETAILS MODIFY (NAME VARCHAR(20)); 
    DROP TABLE EMPLOYEE;
    TRUNCATE TABLE EMPLOYEE; 
```

<h4>Data Manipulation Language (DML) - INSERT, UPDATE, DELETE</br>

```
    INSERT INTO javatpoint (Author, Subject) VALUES ("Sonoo", "DBMS"); 
    UPDATE students    
    SET User_Name = 'Sonoo'   
    WHERE Student_Id = '3';
    DELETE FROM javatpoint  
    WHERE Author="Sonoo";
```

<h4>Data Control Language (DCL) - Grant, Revoke</br>

```
      GRANT SELECT, UPDATE ON MY_TABLE TO SOME_USER, ANOTHER_USER; 
      REVOKE SELECT, UPDATE ON MY_TABLE FROM USER1, USER2;</br> 
```

<h3>8. Create a database of new users with different privileges.</h3></br><img src="https://github.com/korotetskiy/img/blob/main/db8.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-1.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-2.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-3.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-4.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-5.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-6.png"><head></br>
<h3>Connect to the databases a new user and verify that the privileges allow or deny certain actions.</h3><img src="https://github.com/korotetskiy/img/blob/main/db8-7.png"></br><head><img src="https://github.com/korotetskiy/img/blob/main/db8-7-1.png"><head><img src="https://github.com/korotetskiy/img/blob/main/db8-8.png"><head>   
  
<h3>9. Make a selection from the main table DB MySQL.</h3>
<img src="https://github.com/korotetskiy/img/blob/main/db-9.png"></br>
 
<h2>PART 2</h2>
<h3>10. Make backup of your database.</h3><img src="https://github.com/korotetskiy/img/blob/main/db9.png">
<h3>11. Delete the table and/or part of the data in the table.</h3><head><img src="https://github.com/korotetskiy/img/blob/main/db11.png">
<h3>12. Restore your database.</h3><head><img src="https://github.com/korotetskiy/img/blob/main/db12.png">
<h3>13. Transfer your local database to RDS AWS.</h3>
    The first step in the process of migration of data to an Amazon RDS instance is creating a copy of the source data (10).
    Installing the AWS CLI to transfer local database to Amazon RDS:<img src="https://github.com/korotetskiy/img/blob/main/db13.png"><img src="https://github.com/korotetskiy/img/blob/main/db13-1.png"><img src="https://github.com/korotetskiy/img/blob/main/db13-3.png"><head>
    Creating database by restoring from S3</br><head><img src="https://github.com/korotetskiy/img/blob/main/db13-4.png">
    <img src="https://github.com/korotetskiy/img/blob/main/db13-5.png">
    <img src="https://github.com/korotetskiy/img/blob/main/db13-6.png">
    <img src="https://github.com/korotetskiy/img/blob/main/db13-7.png">
    <img src="https://github.com/korotetskiy/img/blob/main/db13-8.png">
    <img src="https://github.com/korotetskiy/img/blob/main/db13-9.png">      
<h3>14. Connect to your database.</h3><img src="https://github.com/korotetskiy/img/blob/main/db14.png">
<h3>15. Execute SELECT operator similar step 6.</h3><img src="https://github.com/korotetskiy/img/blob/main/db15.png"><img src="https://github.com/korotetskiy/img/blob/main/db15-1.png">
<h3>16. Create the dump of your database.</h3><img src="https://github.com/korotetskiy/img/blob/main/db16.png">

<h2>PART 3 – MongoDB</h2>
<h3>17. Create a database. Use the use command to connect to a new database (If it doesn't exist, Mongo will create it when you write to it).</h3><img src="https://github.com/korotetskiy/img/blob/main/db17-1.png"><img src="https://github.com/korotetskiy/img/blob/main/db17-3.png">
<h3>18. Create a collection. Use db. create Collection to create a collection.</h3></br><img src="https://github.com/korotetskiy/img/blob/main/db17-2.jpg"><img src="https://github.com/korotetskiy/img/blob/main/db17-5.png">
<h3>19. Create some documents.</h3><img src="https://github.com/korotetskiy/img/blob/main/db17-6.png">
<h3>20. Use find () to list documents out.</h3><img src="https://github.com/korotetskiy/img/blob/main/db20.png"> 
