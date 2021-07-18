[4yourears DDD approach.docx](https://github.com/chandrasekhar2525/4yourearsMS/files/6836318/4yourears.DDD.approach.docx)
[4yourears DDD approach.docx](https://github.com/chandrasekhar2525/4yourearsMS/files/6836321/4yourears.DDD.approach.docx)
# 4yourearsMS
4yourearsMicroservice
4yourears DDD approach:
Solution approach:

4yourears selling - CD ,audio books 

Suppliers: Medium-size suppliers, Large suppliers
•	A Domain Layer
The Domain Layer contains the real business logic, but does not contain any infrastructure specific code. The infrastructure specific implementation is provided by the Infrastructure Layer. The Domain Model should be designed as described by the CQS(Command-Query-Separation) principle. There can be query methods which do just return data without affecting state, and there are command methods, which affect state but do not return anything.

•	An Infrastructure Layer
The Infrastructure Layer provides the infrastructure dependent parts for all other layers, like a Hibernate or JPA backed implementation. Aggregate data can be stored in an RDMBS like Oracle or MySQL, or it can be stored as XML/JSON or even Google ProtocolBuffers serialized objects in a key-value or document based NoSQL engine. This is up to you, as long the storage provides transaction control and guarantees consistency. Infrastructure can be best described as “Everything around the domain model”, so databases, file system resources or even Web Service consumers if we interact with other systems.

•	 an Application Layer
The Application Layer takes commands from the User Interface Layer and translates these commands to use case invocations on the domain layer. The Application Layer also provides transaction control for business operations. The application layer is responsible to translate Aggregate data into the client specific presentation model by a Mediator or Data Transformer pattern.

Circiutbreakup Pattern  usage in our service:
 

@EnableCircuitBreaker
@RestController
@SpringBootApplication
public class 4yourearsyourears {
 
  @Autowired
  private SellingService sellingService;
 
  @Bean
  public RestTemplate rest(RestTemplateBuilder builder) {
    return builder.build();
  }
 
  @RequestMapping("/to-track")
  public String toTrack() {
    return sellingService.getStats();
  }
 
  public static void main(String[] args) 
SpringApplication.run(4yourearsyourears.class, args);
  }
}
Logical Architecture:

 4yourears India ,Europe and US
               |
Selling application CD and books
|
Suppliers Medium and large
|
Target audience 1,000,000
|
Visitors can access daily


Technical Architecture:
application.properties
--------------------

 Applicationn context name
server.contextPath=/springbootds

spring.datasource.url=jdbc:mysql://localhost/Database
spring.datasource.username=4yourears
spring.datasource.password=4yourears
spring.datasource.driver-class-name=com.mysql.jdbc.Driver

pom.xml:
-----------

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.4yourears</groupId>
  <artifactId>SpringBoot4yourears</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  
  	<parent>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-parent</artifactId>
	    <version>1.5.6.RELEASE</version>
	</parent>
	
	<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
         </dependency>    
	    <dependency>
	        <groupId>org.springframework.boot</groupId>
	        <artifactId>spring-boot-starter-web</artifactId>
	    </dependency>
		<dependency>
		    <groupId>mysql</groupId>
		    <artifactId>mysql-connector-java</artifactId>
		</dependency>
	</dependencies>
	
	<properties>
	 <java.version>1.8</java.version>
	</properties> 
  
</project>


SpringBootApp.java

----------------------

package com.4yourears.app;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class 4yourears {
   public static void main(String[] args) {
     SpringApplication.run(4yourears.class, args);
   }
}


Spring4yourearssController.java:
--------------------------------
package com.4yourears.app.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.4yourears.app.repository.Spring4yourearsDAO;
import com.4yourears.model.Customer;

@RestController
public class Spring4yourearssController {

    @Autowired
    public Spring4yourearsDAO dao;

    @RequestMapping("/getcustInfo")
    public List<Customer> customerInformation() {
        List<Customer> customers = dao.isData(); 
        return customers;
    }
}

Spring4yourearsDAO
---------------------

package com.4yourears.app.repository;

import java.util.ArrayList;
import java.util.List;
import java.util.Map;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;

import com.4yourears.model.Customer;

@Repository
public class Spring4yourearsDAO {

     @Autowired
     private JdbcTemplate jdbcTemplate;

     private static final String SQL = "select * from customers";

     public List<Customer> isData() {

          List<Customer> customers = new ArrayList<Customer>();
          List<Map<String, Object>> rows = jdbcTemplate.queryForList(SQL);

          for (Map<String, Object> row : rows) 
          {
               Customer customer = new Customer();
               customer.setCustNo((int)row.get("Cust_id"));
               customer.setCustName((String)row.get("Cust_name"));
               customer.setCountry((String)row.get("Country"));

               customers.add(customer);
           }

         return customers;
     }
}

Customer.java
----------------

package com.4yourears.model;

public class Customer {

    private int custNo;
    private String custName;
    private String country;

    public Customer() {
    }

    public Customer(int custNumber, String custName, String country) {
        this.custNo = custNumber;
        this.custName = custName;
        this.country = country;
    }

    public int getCustNo() {
       return custNo;
    }

    public void setCustNo(int custNo) {
       this.custNo = custNo;
    }

    public String getCustName() {
       return custName;
    }

    public void setCustName(String custName) {
       this.custName = custName;
    }

    public String getCountry() {
       return country;
    }

    public void setCountry(String country) {
       this.country = country;
    }
}


JUNIT TESTING:
POM.XML:
ADD DEPENDENCY

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>

package com.4yourears.test;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SpringBoot4yourearsTests {

	@Test
	public void contextLoads() {
	}
TESTMETHOD MOCKING
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

import org.junit.Before;
import org.junit.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import org.springframework.web.context.WebApplicationContext;

public class TestWebApp extends SpringBoot4yourearsTests {

	@Autowired
	private WebApplicationContext webApplicationContext;

	private MockMvc mockMvc;

	@Before
	public void setup() {
		mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext).build();
	}

	@Test
	public void testEmployee() throws Exception {
		mockMvc.perform(get("/Customer")).andExpect(status().isOk())
				.andExpect(content().contentType("application/json;charset=UTF-8"))
				.andExpect(jsonPath("$.name").value("custName")).andExpect(jsonPath("$.no").value("custNo"))
				.andExpect(jsonPath("$.country").value("US")));

	}

}


AGILE METHODOLOGY APPROACH:


DESIGNING for 4YOUREARS
DEVELOPMENT
DEPLOYMEMNT
TESTING’


SPRING DURATION WE TOOK AROUND 3 WEEKS

