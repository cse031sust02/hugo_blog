---
date: "2018-01-30T11:50:23+06:00"
title: "Database Normalization"
---

## Intro
Database normalization is the process of organizing a relational database to reduce data redundancy (duplicate data) and improve data integrity. The concept of Normalization was introduced by [Edgar F. Codd](https://en.wikipedia.org/wiki/Edgar_F._Codd).

Normalization is part of a successful database design. It makes a Relation or Table free from insert/update/delete anomalies and saves space by removing duplicate data.

## Normal Forms :

Theory of Data Normalization is still being developed further. There are discussions even on 6th Normal Form. But usually we call a relational database as "normalized" if it meets third normal form. [(src)](https://en.wikipedia.org/wiki/Database_normalization#cite_ref-Codd1970_4-0)

### First Normal Form
	
Once a table is in first normal form, it is easier to search, filter, and sort information from that table.

The rules for first normal form :

- End row should contain a primary key to uniquely identify that row. The primary key can be a single column or combination of multiple columns.
- Each column should contains atomic value (can not be subdivided). i.e., "red, green" is not acceptable.
- Each column should contains values that are same type (i.e., do not put 'address' in 'phone' column)
- There are no repeating groups of columns (i.e., do not have columns like Phone1, Phone2, and Phone3)

### Second Normal Form

The rules for second normal form :

- The database must meet all the requirements of the 1NF.
- All the non-key columns depend on the table’s primary key.

### Third Normal Form

The rules for third nomal form :

- The database must meet all the requirements of the 2NF.
- All the columns of the table are not transitively dependent on the primary key.

This [video](https://www.youtube.com/watch?v=UrYLYV7WSHM) is very helpful to understand all the normal forms with example.