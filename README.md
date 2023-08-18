# CrudOperationUsingSpringBootThemeLeaf
Demo Example provides crud operation using spring boot theme leaf from MySQL database

The project uses mysql database 

You have to download and install mysql 8.1

you have to create a database mydb which contains a table student

student table can be created by using following sql

CREATE TABLE `student` (
  `Id` int NOT NULL AUTO_INCREMENT,
  `name` varchar(45) NOT NULL,
  `department` varchar(45) DEFAULT NULL,
  `content` mediumblob,
  `updated_by` varchar(45) DEFAULT NULL,
  `updated_on` datetime(6) DEFAULT NULL,
   PRIMARY KEY (`Id`)
  );

add one row for sample

download and install spring tool suite 4

download and install java 8.0

run springtoolsuite4. it will create a workspace.

to create new project : File-> new-> project <-/

Select 'spring starter project' in 'spring boot' option

then select next

provide project name for example demo

select default location or provide location by using browse

select project type: Maven; packaging: jar

select java version: 8; Language: java

Write group name for example com.ucp; artifect: demo; version: 0.0.1-SNAPSHOT; package: com.ucp.student




  

