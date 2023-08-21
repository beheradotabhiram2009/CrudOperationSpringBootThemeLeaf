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

add one sample row.

download and install java 8.0 and spring tool suite 4

run springtoolsuite4. to create new project : File-> new-> project <-/

Select 'spring starter project' in 'spring boot' optiont. Then select next

provide project name for example demo

select default location or provide location by using browse

select project type: Maven; packaging: jar; select java version: 8; Language: java

Write group name for example com.ucp; artifect: demo; version: 0.0.1-SNAPSHOT; package: com.ucp.demo; then select next

select springboot version 2.7.14; select MYSQL Driver, Spring Data JPA, Spring Web

application.properties under src.main.resources should contain:

server.port=8080
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.password=root
spring.datasource.username=root
spring.datasource.url=jdbc:mysql://localhost:3306/mydb

edit pom.xml under demo so that it contains:

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.7.14</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.ucp</groupId>
	<artifactId>demo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>demo</name>
	<description>project for crud operation using mysql Spring Boot themeleaf</description>
	<properties>
		<java.version>1.8</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-thymeleaf</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
<dependency>
    		<groupId>org.webjars.bower</groupId>
    		<artifactId>bootstrap</artifactId>
    		<version>5.1.3</version>
		</dependency>
		<dependency>
    		<groupId>org.webjars.bower</groupId>
    		<artifactId>jquery</artifactId>
    		<version>3.6.0</version>
		</dependency>
		<dependency>
			<groupId>com.mysql</groupId>
			<artifactId>mysql-connector-j</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>
	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
</project>

Create  folders models, controllers, repos, services under com.ucp.demo

create class HomeController under controllers folder

HomeController.java should contail

package com.ucp.demo.controllers;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
@Controller
public class HomeController {
	@RequestMapping("/home")
	public String test() {
		return "index";
	}
}

create index.html file under templates folder which contains:

<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>demo spring crud app</title>
</head>
<body>
<h2>Everything Works so far</h2>
</body>

now run as Spring Boot App

you should see 'Everything Works so far'

create class Student under models folder

create class StudentRepository under repos folder

create class StudentServices under services folder







  

