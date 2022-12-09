<h2>DevOps L1 course Database Administration Home Tasks</h2>
<head>
<h3>Part 1</h3>
1. Download MySQL server for your OS on VM. 
2. Install MySQL server on VM.</br><h3>sudo apt-get install mysql-server</h3><img src="https://github.com/korotetskiy/img/blob/main/db1.png"></br>
3. Select a subject area and describe the database schema, (minimum 3 tables)</br><img src="https://github.com/korotetskiy/img/blob/main/db3.png"></br><head>
4. Create a database on the server through the console.</br><img src="https://github.com/korotetskiy/img/blob/main/db2-1.png"><head>
5. Fill in tables.</br><img src="https://github.com/korotetskiy/img/blob/main/db4.png"></br><head>  
6. Construct and execute SELECT operator with WHERE, GROUP BY and ORDER BY.</br><img src="https://github.com/korotetskiy/img/blob/main/db6.png"></br><head>
<img src="https://github.com/korotetskiy/img/blob/main/db6-1.png"></br><head>
    
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

8. Create a database of new users with different privileges.</br></br><img src="https://github.com/korotetskiy/img/blob/main/db8.png"></br><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-1.png"></br><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-2.png"></br><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-3.png"></br><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-4.png"></br><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-5.png"></br><head>
  <img src="https://github.com/korotetskiy/img/blob/main/db8-6.png"></br><head>
Connect to the databases a new user and verify that the privileges allow or deny certain actions.</br><img src="https://github.com/korotetskiy/img/blob/main/db8-7.png"></br><head><img src="https://github.com/korotetskiy/img/blob/main/db8-7-1.png"></br><head><img src="https://github.com/korotetskiy/img/blob/main/db8-8.png"></br><head>   
  
9. Make a selection from the main table DB MySQL.</br><head>
<img src="https://github.com/korotetskiy/img/blob/main/db-9.png"></br><head>
 
<h3>PART 2</h3>
10. Make backup of your database.</br><img src="https://github.com/korotetskiy/img/blob/main/db9.png"></br><head>
11. Delete the table and/or part of the data in the table.</br><head><img src="https://github.com/korotetskiy/img/blob/main/db11.png"></br><head> 
12. Restore your database.</br><head><img src="https://github.com/korotetskiy/img/blob/main/db12.png"></br><head> 
13. Transfer your local database to RDS AWS.
    The first step in the process of migration of data to an Amazon RDS instance is creating a copy of the source data (10).
    Installing the AWS CLI to transfer local database to Amazon RDS:
    
    Creating database by restoring from S3
 
 




  
      
14. Connect to your database.
15. Execute SELECT operator similar step 6.
16. Create the dump of your database.

<h3>PART 3 – MongoDB</h3>
17. Create a database. Use the use command to connect to a new database (If it doesn't exist, Mongo will create it when you write to it).
18. Create a collection. Use db. create Collection to create a collection. I'll leave the subject up to you. Run show dbs and show collections to view your database and collections.
19. Create some documents. Insert a couple of documents into your collection. I'll leave the subject matter up to you, perhaps cars or hats.
20. Use find () to list documents out.
