# Mulesoft's Anypoint Studio and Teradata Vantage - Sample Use Cases

This repository contains samples of different projects that can be imported into Mulesoft's AnyPoint studio to illustrate the integration of Teradata JDBC connector with mulesoft. 

The samples are illustrated in a way the user can reproduce them by using AnyPoint Studio IDE, however, it is also possible to import the folders to the IDE.

## Table of contents

This repository contains the following samples.

* Basic Data Manipulation Language -DML- Operations with Teradata and Anypoint Studio
- SELECT
- INSERT
- DELETE

* Data flow with AnyPoint's `On Table Row` component.

## Basic Data Manipulation Language -DML- Operations with Teradata and Anypoint Studio

## Data flow with AnyPoint's `On Table Row` component.

### Description
* On this example we will be working with two sample tables.
* The tables are the following:
    * PendingHires
        * GlobalID,
        * FirstName,
        * LastName,
        * DateOfBirth,
        * DepartmentCode
    * Employees
        * GlobalID,
        * FirstName,
        * LastName,
        * DateOfBirth,
        * JoinedDate,
        * DepartmentCode
* For illustrative purposes we will insert some data in the PendingHires table.
* When a record with a certain Global Id is added the same record is deleted.
For simplicity we are using the `delete` component in the example. Any other DML component could be used in a similar way.

### Loading sample data
#### Optain a Teradata Vantage Instance:

* A teradata vantage instance can be obtained in [ClearScape Analytics Experience](http://teradata.com/experience){:target="_blank"}
    * When creating your account you can create up to two environments, each of which is power by a Teradata Vantage Instance. 
    * Remember the password used when creating your ClearScape Analytics Experience Environments, it is the password to your database instance.


All commands below shall be ran in your favorite database client.

* First we will create a database through the following command
```
-- create database
 CREATE DATABASE HR
   AS PERMANENT = 60e6, SPOOL = 120e6;
```
* With the database created we can create the two tables needed for the sample use case

```
CREATE SET TABLE HR.Employees (
   GlobalID INTEGER,
   FirstName VARCHAR(30),
   LastName VARCHAR(30),
   DateOfBirth DATE FORMAT 'YYYY-MM-DD',
   JoinedDate DATE FORMAT 'YYYY-MM-DD',
   DepartmentCode BYTEINT
 )
 UNIQUE PRIMARY INDEX ( GlobalID );

 CREATE SET TABLE HR.PendingHires (
   GlobalID INTEGER,
   FirstName VARCHAR(30),
   LastName VARCHAR(30),
   DateOfBirth DATE FORMAT 'YYYY-MM-DD',
   DepartmentCode BYTEINT
 )
 UNIQUE PRIMARY INDEX ( GlobalID );
```

* Next we will add a couple of records to the `PendingHires` table:
