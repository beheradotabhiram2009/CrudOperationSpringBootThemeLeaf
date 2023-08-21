# CrudOperationUsingSpringBootThemeLeaf
Demo Example provides crud operation using spring boot theme leaf from MySQL database

You have to download and install mysql 8.1

create a database mydb and a table student

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

download and install java 8.0 and spring tool suite 4

run springtoolsuite4. to create new project : File-> new-> project <-/

Select 'spring starter project' in 'spring boot' optiont. Then select next

provide project name for example demo

select default location or provide location by using browse

select project type: Maven; packaging: jar; select java version: 8; Language: java

Write group name for example com.ucp; artifect: demo; version: 0.0.1-SNAPSHOT; package: com.ucp.demo; then select next

select springboot version 2.7.14; select MYSQL Driver, Spring Data JPA, Spring Web

run as Spring Boot App

you should see 'Everything Works so far'

Create  folders models, controllers, repos, services under com.ucp.demo

create class Student under models folder

create class StudentRepository under repos folder

create class StudentServices under services folder

create class HomeController and StudentController under controllers folder









  

