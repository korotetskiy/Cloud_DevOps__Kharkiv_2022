  <main role="main" class="container">
<body>
    <div class="starter-template">
      <h1>EPAM Cloud&DevOps Fundamentals Autumn 2022</h1>
      <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="essets/Css/style.css">
</head>
    <img src="https://vkor-www.s3.amazonaws.com/main1.jpg">
    <h1>Vladimir</h1>
      <hr>
    </div>
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="essets/Css/style.css">
</head>
<body>
   Option2
</h3>
  <p>lDevOps L1course Database Administration TASK DB1
1. Download MySQL server for your OS on VM.
2. Install MySQL server on VM.
sudo apt-get install mysql-server
  <img src="https://vkor-www.s3.amazonaws.com/main1.jpg">
3. Select a subject area and describe the database schema, (minimum 3 tables)
  <img src="https://vkor-www.s3.amazonaws.com/main1.jpg">
4. Create a database on the server through the console.
  <img src="https://vkor-www.s3.amazonaws.com/main1.jpg">
 
5. Fill in tables.
     <img src="https://vkor-www.s3.amazonaws.com/main1.jpg">



6. Construct and execute SELECT operator with WHERE, GROUP BY and ORDER BY.
  <img src="https://vkor-www.s3.amazonaws.com/main1.jpg"> 
 
7. Execute other different SQL queries DDL, DML, DCL.
Data Definition Language (DDL) -  CREATE,    ALTER,    DROP,   TRUNCATE
    CREATE TABLE EMPLOYEE(Name CHAR, Email CHAR, DOB DATE);  
    ALTER TABLE STU_DETAILS ADD(ADDRESS VARCHAR(20));  
    ALTER TABLE STU_DETAILS MODIFY (NAME VARCHAR(20));  
    DROP TABLE EMPLOYEE;
    TRUNCATE TABLE EMPLOYEE;   

Data Manipulation Language (DML) - INSERT, UPDATE, DELETE
    INSERT INTO javatpoint (Author, Subject) VALUES ("Sonoo", "DBMS");  
    UPDATE students    
    SET User_Name = 'Sonoo'    
    WHERE Student_Id = '3';
    DELETE FROM javatpoint  
    WHERE Author="Sonoo";

Data Control Language (DCL) - Grant, Revoke
      GRANT SELECT, UPDATE ON MY_TABLE TO SOME_USER, ANOTHER_USER; 
      REVOKE SELECT, UPDATE ON MY_TABLE FROM USER1, USER2; 

8. Create a database of new users with different privileges.           
Connect to the databases a new user and verify that the privileges allow or deny certain actions.  
  <img src="https://vkor-www.s3.amazonaws.com/main1.jpg">
 
9. Make a selection from the main table DB MySQL.
  <img src="https://vkor-www.s3.amazonaws.com/main1.jpg">

PART 2
10. Make backup of your database.
  <img src="https://vkor-www.s3.amazonaws.com/main1.jpg">
11. Delete the table and/or part of the data in the table.
 
12. Restore your database.
 
13. Transfer your local database to RDS AWS.
      The first step in the process of migration of data to an Amazon RDS instance is creating a copy of the source data (10).
     Installing the AWS CLI to transfer local database to Amazon RDS:
      
    Creating database by restoring from S3
 
 




  
      
14. Connect to your database.
15. Execute SELECT operator similar step 6.
16. Create the dump of your database.

PART 3 – MongoDB
17. Create a database. Use the use command to connect to a new database (If it doesn't exist, Mongo will create it when you write to it).
18. Create a collection. Use db. create Collection to create a collection. I'll leave the subject up to you. Run show dbs and show collections to view your database and collections.
19. Create some documents. Insert a couple of documents into your collection. I'll leave the subject matter up to you, perhaps cars or hats.
20. Use find () to list documents out.
 </p>

