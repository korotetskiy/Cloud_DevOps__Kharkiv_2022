<h2>DevOps L1 course Database Administration Home Tasks</h2>
<head>
<h3>Part 1</h3>
1. Download MySQL server for your OS on VM.</br><head> 
2. Install MySQL server on VM.</br><h3>sudo apt-get install mysql-server</h3><img src="https://github.com/korotetskiy/img/blob/main/db1.png">
3. Select a subject area and describe the database schema, (minimum 3 tables)</br><img src="https://github.com/korotetskiy/img/blob/main/db3.png">
4. Create a database on the server through the console.</br><img src="https://github.com/korotetskiy/img/blob/main/db2-1.png">
5. Fill in tables.</br><img src="https://github.com/korotetskiy/img/blob/main/db4.png"></br>
6. Construct and execute SELECT operator with WHERE, GROUP BY and ORDER BY.</br><img src="https://github.com/korotetskiy/img/blob/main/db6.png">
<img src="https://github.com/korotetskiy/img/blob/main/db6-1.png">
    
7. Execute other different SQL queries DDL, DML, DCL.</br><head>
<h4>Data Definition Language (DDL) -  CREATE,    ALTER,    DROP,   TRUNCATE</br>
    CREATE TABLE EMPLOYEE(Name CHAR, Email CHAR, DOB DATE);</br>  
    ALTER TABLE STU_DETAILS ADD(ADDRESS VARCHAR(20));</br>  
    ALTER TABLE STU_DETAILS MODIFY (NAME VARCHAR(20)); </br> 
    DROP TABLE EMPLOYEE;</br>
    TRUNCATE TABLE EMPLOYEE;</h4>   

<h4>Data Manipulation Language (DML) - INSERT, UPDATE, DELETE</br>
    INSERT INTO javatpoint (Author, Subject) VALUES ("Sonoo", "DBMS"); </br> 
    UPDATE students    </br>
    SET User_Name = 'Sonoo' </br>   
    WHERE Student_Id = '3';</br>
    DELETE FROM javatpoint</br>  
    WHERE Author="Sonoo";</h4>

<h4>Data Control Language (DCL) - Grant, Revoke</br>
      GRANT SELECT, UPDATE ON MY_TABLE TO SOME_USER, ANOTHER_USER; </br>
      REVOKE SELECT, UPDATE ON MY_TABLE FROM USER1, USER2;</br> </h4>

8. Create a database of new users with different privileges.</br></br><img src="https://github.com/korotetskiy/img/blob/main/db8.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-1.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-2.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-3.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-4.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-5.png"><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-6.png"><head></br>
Connect to the databases a new user and verify that the privileges allow or deny certain actions.</br><img src="https://github.com/korotetskiy/img/blob/main/db8-7.png"></br><head><img src="https://github.com/korotetskiy/img/blob/main/db8-7-1.png"><head><img src="https://github.com/korotetskiy/img/blob/main/db8-8.png"><head>   
  
9. Make a selection from the main table DB MySQL.</br><head>
<img src="https://github.com/korotetskiy/img/blob/main/db-9.png"></br><head>
 
<h3>PART 2</h3>
10. Make backup of your database.</br><img src="https://github.com/korotetskiy/img/blob/main/db9.png">
11. Delete the table and/or part of the data in the table.</br><head><img src="https://github.com/korotetskiy/img/blob/main/db11.png">
12. Restore your database.</br><head><img src="https://github.com/korotetskiy/img/blob/main/db12.png">
13. Transfer your local database to RDS AWS.</br></br>
    The first step in the process of migration of data to an Amazon RDS instance is creating a copy of the source data (10).
    Installing the AWS CLI to transfer local database to Amazon RDS:<img src="https://github.com/korotetskiy/img/blob/main/db13.png"><img src="https://github.com/korotetskiy/img/blob/main/db13-1.png"><img src="https://github.com/korotetskiy/img/blob/main/db13-3.png"><head>
    Creating database by restoring from S3</br><head><img src="https://github.com/korotetskiy/img/blob/main/db13-4.png">
    <img src="https://github.com/korotetskiy/img/blob/main/db13-5.png">
    <img src="https://github.com/korotetskiy/img/blob/main/db13-6.png">
    <img src="https://github.com/korotetskiy/img/blob/main/db13-7.png">
    <img src="https://github.com/korotetskiy/img/blob/main/db13-8.png">
    <img src="https://github.com/korotetskiy/img/blob/main/db13-9.png">      
14. Connect to your database.<img src="https://github.com/korotetskiy/img/blob/main/db14.png">
15. Execute SELECT operator similar step 6.<img src="https://github.com/korotetskiy/img/blob/main/db15.png"><img src="https://github.com/korotetskiy/img/blob/main/db15-1.png">
16. Create the dump of your database.<img src="https://github.com/korotetskiy/img/blob/main/db16.png">

<h3>PART 3 – MongoDB</h3>
17. Create a database. Use the use command to connect to a new database (If it doesn't exist, Mongo will create it when you write to it).</br><img src="https://github.com/korotetskiy/img/blob/main/db17-1.png"><img src="https://github.com/korotetskiy/img/blob/main/db17-3.png">
18. Create a collection. Use db. create Collection to create a collection.</br></br><img src="https://github.com/korotetskiy/img/blob/main/db17-2.jpg"><img src="https://github.com/korotetskiy/img/blob/main/db17-5.png">
19. Create some documents.<img src="https://github.com/korotetskiy/img/blob/main/db17-6.png">
20. Use find () to list documents out.</br>
