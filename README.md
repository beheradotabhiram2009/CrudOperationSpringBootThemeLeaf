# CrudOperationUsingSpringBootThemeLeaf
Demo Example provides crud operation using spring boot theme leaf from MySQL database
The project uses mysql database mydb which contains a table student
student table can be created by using following sql
CREATE TABLE `student` (
  `Id` int NOT NULL AUTO_INCREMENT,
  `name` varchar(45) NOT NULL,
  `department` varchar(45) DEFAULT NULL,
  `content` mediumblob,
  `updated_by` varchar(45) DEFAULT NULL,
  `updated_on` datetime(6) DEFAULT NULL,
   PRIMARY KEY (`Id`),
  );

