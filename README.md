## CrudOperationUsingSpringBootThemeLeaf
### Demo Example provides crud operation using spring boot theme leaf from MySQL database
### Download and install mysql 8.1
### create a database mydb and a table student by using following sql
```sql
CREATE TABLE `student` (
  `Id` int NOT NULL AUTO_INCREMENT,
  `name` varchar(45) NOT NULL,
  `department` varchar(45) DEFAULT NULL,
  `content` mediumblob,
  `updated_by` varchar(45) DEFAULT NULL,
  `updated_on` datetime(6) DEFAULT NULL,
   PRIMARY KEY (`Id`)
  );
```
### insert sample rows.
### download and install java 17 and spring tool suite 4
### run springtoolsuite4. to create new project : File-> new-> project <-/
### Select 'spring starter project' in 'spring boot' optiont. Then select next
### provide project name for example mydemo
### select default location or provide location by using browse
### select project type: Maven; packaging: jar; select java version: 17; Language: java
### Write group name for example com.ucp; artifect: mydemo; version: 0.0.1-SNAPSHOT; package: com.ucp.mydemo; 
### then select next
### select springboot version 3.1.3; select MYSQL Driver, Spring Data JPA, Spring Web
### under src.main.resources file application.properties should contain:
````
server.port=8080
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.password=root
spring.datasource.username=root
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
```
### edit pom.xml under mydemo so that it contains:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.1.3</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.ucp</groupId>
	<artifactId>mydemo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>mydemo</name>
	<description>project for crud operation using mysql Spring Boot themeleaf</description>
	<properties>
		<java.version>17</java.version>
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
    			<version>5.3.0</version>
		</dependency>
		<dependency>
    			<groupId>org.webjars.bower</groupId>
    			<artifactId>jquery</artifactId>
    			<version>3.7.0</version>
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
```
### Create  folders models, controllers, repos, services under com.ucp.mydemo
### create class HomeController under controllers folder, it should contain:
```java
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
```
### create index.html file under templates folder which contains:
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>demo spring crud app</title>
</head>
<body>
<h2>Everything Works so far</h2>
</body>
```
### now run as Spring Boot App and browse http://localhost:8080/
### you should see 'Everything Works so far'
### create class Student under models folder. it should contain:
```java
package com.ucp.mydemo.models;
import java.util.Date;
import org.springframework.format.annotation.DateTimeFormat;
import jakarta.persistence.Entity;

@Entity
public class Student {
	@jakarta.persistence.Id
	private Integer Id;
	private String name;
	private String department;
	private String updatedBy;
	private byte[] content;
	
	@DateTimeFormat(pattern="yyyy-MM-dd")
	private Date updatedOn;
	
	public Student() {
		
	}
	public Student(Integer id, String name, String department, String updatedBy, 
			Date updatedOn) {
		super();
		Id = id;
		this.name = name;
		this.department = department;
		this.updatedBy = updatedBy;
		this.updatedOn = updatedOn;
	}
	@Override
	public String toString() {
		return "Student [Id=" + Id + ", name=" + name + ", department=" + department + ", "
				+ "updatedBy=" + updatedBy + ", updatedOn=" + updatedOn + "]";
	}

	public Integer getId() {
		return Id;
	}

	public void setId(Integer id) {
		Id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getDepartment() {
		return department;
	}

	public void setDepartment(String department) {
		this.department = department;
	}

	public String getUpdatedBy() {
		return updatedBy;
	}

	public void setUpdatedBy(String updatedBy) {
		this.updatedBy = updatedBy;
	}
	
	public Date getUpdatedOn() {
		return updatedOn;
	}
	
	public void setUpdatedOn(Date dt) {
		updatedOn = dt;
	}
	
	public byte[] getContent() {
		return content;
	}
	
	public void setContent(byte[] content) {
		this.content = content;
	}
}
```

### create class StudentRepository under repos folder. it should contain:
```java
package com.ucp.mydemo.repos;
import org.springframework.data.repository.CrudRepository;
import com.ucp.mydemo.models.Student;
public interface StudentRepository extends CrudRepository<Student, Integer>{
	
} 
```
### create class StudentServices under services folder. it should contain:
```java
package com.ucp.mydemo.services;
import java.util.List;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import com.ucp.mydemo.models.Student;
import com.ucp.mydemo.repos.StudentRepository;

@Service
public class StudentService {
	@Autowired(required=true)
	StudentRepository studentRepository;

	public List<Student> getAll() {
		 return (List<Student>) studentRepository.findAll();
	}
	
	public Student getStudent(Integer id) {
		 return studentRepository.findById(id).get();
	}
	
	public void insert(Student student) {
		int max = 0;
		Iterable<Student> list = studentRepository.findAll();
		for(Student stud : list){
			if(stud.getId() > max) max = stud.getId();
		}
		student.setId(max + 1);
		studentRepository.save(student);
	}
	
	public void update(int id, Student newStudent) {
		Student student =  studentRepository.findById(id).get();
		student.setName(newStudent.getName());
		student.setDepartment(newStudent.getDepartment());
		student.setUpdatedBy(newStudent.getUpdatedBy());
		student.setUpdatedOn(newStudent.getUpdatedOn());
		if(newStudent.getContent().length!=0)
			student.setContent(newStudent.getContent());
		studentRepository.save(student);
	}
	
	public void delete(int id) {
		Student student =  studentRepository.findById(id).get();
		studentRepository.delete(student);
	}
}
```
### create class StudentController under controlers folder. it should contain:
```java
package com.ucp.mydemo.controllers;

import java.io.IOException;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.repository.query.Param;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.multipart.MultipartFile;

import com.ucp.mydemo.models.Student;
import com.ucp.mydemo.services.StudentService;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletResponse;

@Controller
@RequestMapping("/students")
public class StudentController {

	@Autowired(required=true)
	private StudentService studentService;
	
	@GetMapping("/getAll")
	public String getAll(Model model) {
		List<Student> stlist = studentService.getAll();
		model.addAttribute("students", stlist);
		return "students";
	}
	
	@GetMapping("/addNew")
	public String newStudent(Model model) {
		Student student = new Student();
		model.addAttribute("student", student);
		return "add-student";
    }
	
	@GetMapping("/edit/{id}")
	public String editStudent(@PathVariable("id") int id, Model model, HttpServletResponse response) 
			throws IOException {
		Student student = studentService.getStudent(id);
		//student.setUpdatedOn(student.getUpdatedOn());
		model.addAttribute("student", student);
		return "edit-student";
    }
	
	@PostMapping("/delete/{id}")
	public String deleteStudent(@PathVariable("id") int id) {
		studentService.delete(id);
        return "redirect:/students/getAll";
    }
	
	@PostMapping("/saveNew")
	public String insertStudent(
			@ModelAttribute(value="student") Student student,
			@RequestParam("photo") MultipartFile file) throws IOException {
		if(file != null) student.setContent(file.getBytes());
		studentService.insert(student);
        return "redirect:/students/getAll";
    }
	
	@PostMapping("/update/{id}")
	public String updateStudent(
			@PathVariable("id") int id, 
			@ModelAttribute(value="student") Student student,
			@RequestParam("photo") MultipartFile file) throws IOException
	{
		if(file != null) student.setContent(file.getBytes());
		studentService.update(id, student);
        return "redirect:/students/getAll";
    }
	
	  
	 @GetMapping("/getPhoto")
	 public void getStudentPhoto(HttpServletResponse response, @Param("id") int id) 
			 throws ServletException, IOException 
	 {
		 response.setContentType("jpeg, jpg, png");
		 Student student = studentService.getStudent(id);
		 response.getOutputStream().write(student.getContent());
		 response.getOutputStream().close();
	 }	
}
```
### create students.html under templates folder. it should contain:
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<link href="/webjars/bootstrap/5.3.0/dist/css/bootstrap.css" rel="stylesheet"/>
<script type="text/javascript" src="/webjars/bootstrap/5.3.0/dist/js/bootstrap.min.js"></script>
<script type="text/javascript" src="/webjars/jquery/3.7.0/dist/jquery.min.js"></script>
<title>spring crud app</title>
</head>
<body>
<button class="btn btn-outline-dark">
<a th:href="@{addNew}">Add Student<i class="fas fa-wrench"></i></a>
</button>

<table class="table table-stripped">
<thead>
<tr>
<td>Id</td><td>Name</td><td>Department</td><td>Updated By</td><td>Updated On</td><td>Photo</td><td>Change</td><td>Remove</td>
</tr>
</thead>
<tr th:each="student:${students}">
<form action="#" method="post" th:action="@{delete/__${student.Id}__}">
<td th:text="${student.Id}"></td>
<td th:text="${student.name}"></td>
<td th:text="${student.department}"></td>
<td th:text="${student.updatedBy}"></td>
<td th:text="${student.updatedOn}"></td>
<td><img th:src="@{getPhoto?id=__${student.Id}__}"	alt="" width="50px" height="50px"/></td>
<td> <button class="btn btn-outline-dark" type="button">
         <a th:href="@{edit/__${student.Id}__}">Edit</a>
      </button>
</td>
<td>
	<button class="btn btn-outline-dark" type="submit" Style="color:blue;text-decoration:underline">
    	Delete
	</button>
</td>
</form >
</tr>
</table>
</body>
```
### now run as Spring Boot App and browse http://localhost:8080/students/getAll
### it should give lit of students.
### create add-student.html under templates folder. it should contain:
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
	<head>
		<meta charset="ISO-8859-1">
		<link href="/webjars/bootstrap/5.3.0/dist/css/bootstrap.css" rel="stylesheet"/>
		<script type="text/javascript" src="/webjars/bootstrap/5.3.0/dist/js/bootstrap.min.js"></script>
		<script type="text/javascript" src="/webjars/jquery/3.7.0/dist/jquery.min.js"></script>
		<title>Student</title>
	</head>
	<body>
		<div align="center">
    		<form action="#" th:object="${student}" method="post" th:action="@{saveNew}" enctype="multipart/form-data">
    		<div class="project-list single">
    		   <fieldset>
                   <h3><u>Enter New Student Information</u></h3>
                   <table><tr><td width="200" align="right">
                   		<label for="name">Name:</label></td >
                       <td align="left" width="300">
                       	<input type="text" th:field="*{name}" autofocus="false"/>
                    </td></tr>
                    <tr><td width="200" align="right">
                    <label for="name">Department:</label></td >
                        <td align="left" width="300">
                        	<input type="text" th:field="*{department}" autofocus="false"/>
                    </td ></tr>
                    <tr><td width="200" align="right">
                    <label for="name">Updated By:</label></td >
                        <td align="left" width="300">
                        	<input type="text" th:field="*{updatedBy}" autofocus="false"/>
                    </td ></tr>
                    <tr><td width="200" align="right">
                    <label for="name">Updated On:</label></td >
                        <td align="left" width="300">
                        	<input type="date" th:field="*{updatedOn}"  autofocus="false" />
                    </td></tr><tr>
                    <tr><td align="right"><label for="photo">Photo:</label></td  ></td>
                    <td><input type="file" name="photo"/></td>
                    </tr><td align="center" colspan="3">
                    		<input class="btn btn-outline-dark" type="submit" Style="color:blue; text-decoration: underline"/>                    		
                    		<input class="btn btn-outline-dark" type="reset"  Style="color:blue; text-decoration: underline"/>
                    		<button class="btn btn-outline-dark" type="button">
                    			<a th:href="@{\students\getAll}">Cancel</a>
                    		</button>
                       </td ></tr></table>            
                 </fieldset>
    		    </div>
              </form>
          </div>
       </body>
  </html>
```
 ### create edit-student.html under templates folder. it should contain:
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
	<head>
		<meta charset="ISO-8859-1">
		<link href="/webjars/bootstrap/5.3.0/dist/css/bootstrap.css" rel="stylesheet"/>
		<script type="text/javascript" src="/webjars/bootstrap/5.3.0/dist/js/bootstrap.min.js"></script>
		<script type="text/javascript" src="/webjars/jquery/3.7.0/dist/jquery.min.js"></script>
		<title>Student</title>
	</head>
	<body>
		<div align="center">
    		<form action="#" th:object="${student}" method="post" enctype="multipart/form-data" th:action="@{/students/update/__${student.Id}__}">
    		<div class="project-list single">
       		   <fieldset>
                  <h3><u>Edit Student Information</u></h3>
                   <table><tr><td width="200" align="right">
                   		<label for="name">Name:</label></td >
                       <td align="left" width="300">
                       	<input type="text" th:field="*{name}" autofocus="false"/>
                    </td></tr>
                    <tr><td width="200" align="right">
                    <label for="name">Department:</label></td >
                        <td align="left" width="300">
                        	<input type="text" th:field="*{department}" autofocus="false"/>
                    </td ></tr>
                    <tr><td width="200" align="right">
                    <label for="name">Updated By:</label></td >
                        <td align="left" width="300">
                        	<input type="text" th:field="*{updatedBy}" autofocus="false"/>
                    </td ></tr>
                    <tr><td width="200" align="right">
                    <label for="name">Updated On:</label></td >
                        <td align="left" width="300">
                        	<input type="date" th:field="*{updatedOn}"  autofocus="false" />
                    </td></tr><tr>
                    <tr><td align="right"><label for="photo">Photo:</label></td  ></td>
                    <td><input type="file" name="photo"/></td>
                    <td><img th:src="@{/students/getPhoto?id=__${student.Id}__}" alt="" width="100px" height="100px"/></td></tr>
                    	<td align="center" colspan="3">
                    		<input class="btn btn-outline-dark" type="submit" Style="color:blue; text-decoration: underline"/>                    		
                    		<input class="btn btn-outline-dark" type="reset"  Style="color:blue; text-decoration: underline"/>
                    		<button class="btn btn-outline-dark" type="button">
                    			<a th:href="@{\students\getAll}">Cancel</a>
                    		</button>
                       </td ></tr></table>
                    </fieldset>
                 </div>
              </form>
          </div>
       </body>
  </html>
```
# now run as Spring Boot App and browse http://localhost:8080/students/getAll and test
