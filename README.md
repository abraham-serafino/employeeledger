# Employee Ledger #

Step-by-step instructions for creating and deploying a secure Spring Data REST application using Docker on AWS.

## Step 1 -- Create REST Repository ##

* First create a JPA entity:

``src/main/java/com/abrahamserafino/employeeledger/Employee.java``

```java
package com.abrahamserafino.employeeledger;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import java.math.BigDecimal;

import lombok.Getter;
import lombok.Setter;
import lombok.ToString;
import lombok.AllArgsConstructor;
import lombok.NoArgsConstructor;

@Entity
@Getter
@Setter
@ToString
@AllArgsConstructor
@NoArgsConstructor
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;

    private String name;
    private BigDecimal salary;

}

```

* Next comes the Spring Data JPA repository, a simple interface that will be implemented by Spring behind
the scenes to create REST endpoints and HTTP request handlers that can query and manipulate a 
database table based on the Entity definition you created above.

``src/main/java/com/abrahamserafino/employeeledger/EmployeeRepository.java``

```java
package com.abrahamserafino.employeeledger;

import java.util.List;

import org.springframework.data.repository.PagingAndSortingRepository;
import org.springframework.data.repository.query.Param;
import org.springframework.stereotype.Repository;

@Repository
public interface EmployeeRepository extends PagingAndSortingRepository<Employee, Long> {
    List<Employee> findByName(@Param("name") String name);
}

```

* Kill any running instances of your Spring Boot application using Ctrl+C, then restart 

    ```./gradlew clean bootRun```

* Navigate to [http://localhost:8080/employees](http://localhost:8080/employees). Now you should see something like this: 

```json
{
  "_embedded" : {
    "employees" : [ ]
  },
  "_links" : {
    "self" : {
      "href" : "http://localhost:8080/employees{?page,size,sort}",
      "templated" : true
    },
    "profile" : {
      "href" : "http://localhost:8080/profile/employees"
    },
    "search" : {
      "href" : "http://localhost:8080/employees/search"
    }
  },
  "page" : {
    "size" : 20,
    "totalElements" : 0,
    "totalPages" : 0,
    "number" : 0
  }
}
``

Notice that your REST endpoint includes HATEOAS links which are provided by Spring Data REST for free.

## Go Forward ##

[Step 2 - Add Swagger](https://bitbucket.org/kungfuandjavascript/employeeledger/src/step2)

## Go Back ##

[Step 0 - Required Ingredients](https://bitbucket.org/kungfuandjavascript/employeeledger/src/step0)