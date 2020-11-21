---
date: "2017-04-11T11:13:09+06:00"
title: "Database & ACID properties"
---

## What is Database? :
  A database is a collection of data that is stored in an organized manner.

> the term "database" is often used casually to refer to both a database and the DBMS used to manipulate it.

### Database Models :
A database model refers to the logical structure, representation or layout of a database and how the data will be stored, managed and processed within it.

There are many kinds of data models. Such as Relational model, Network model, Entity-attribute-value model, Object-oriented database model and many more..

DBMS popularity broken down by database model : http://db-engines.com/en/ranking

### DBMS & RDBMS :
DBMS stands for Database Management System. It is the software application to store and manage the data.

RDBMS stands for Relational Database Management System. It is based on the relational model. The relational model has relationship between tables using primary keys, foreign keys and indexes. 

Example : MySQL, PostgreSQL, MongoDB, Microsoft SQL Server, Oracle etc.

> You can say that a RDBMS is an in an extension of a DBMS. The key difference is that RDBMS applications store data in a tabular form, while DBMS applications store data as files. Does that mean there are no tables in a DBMS? There can be, but there will be no “relation” between the tables, like in a RDBMS. 

> src - https://blog.udemy.com/differences-between-dbms-and-rdbms/

Most software products in the market today are both DBMS and RDBMS compliant. 

---

## What is ACID? :

ACID is a set of properties of database transactions (a single logical operation on the data is called a transaction).

**Atomicity** :  If one part of the transaction fails, then the entire transaction fails, and the database state is left unchanged.

**Consistency** : Any data written to the database must be valid according to all defined rules.

**Isolation** : One transaction cannot read data from another transaction that is not yet completed. If two transactions are executing concurrently, each one will see the world as if they were executing sequentially, and if one needs to read data that is written by another, it will have to wait until the other is finished.

**Durability** : Once a transaction is complete, it is guaranteed that all of the changes have been recorded to a durable medium (such as a hard disk).


![Foo](https://s3-us-west-1.amazonaws.com/morpheus-staging/system/spud_media/332/original/acidoverwiew.png?1422558433)

**Image Source :** [morpheusdata](https://www.morpheusdata.com/blog/2015-01-29-when-do-you-need-acid-compliance-)

### ACID compliants :
  
Oracle is ACID compliant.

PostgreSQL is [ACID compliant](https://www.postgresql.org/about)

MySQL is not an ACID compliant database server by design, but if you use the InnoDB storage engine for your tables, you will be able to perform transaction-safe operations on your database. 

-*Source* : [Stackoverflow](http://stackoverflow.com/questions/4264849/how-to-implement-the-acid-model-for-a-database)