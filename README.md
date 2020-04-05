# Employee Ledger #

Step-by-step instructions for creating and deploying a secure Spring Data REST application using Docker on AWS.

## Step 0 -- Required Ingredients ##

To begin building this project, you will need:

* [OpenJDK 11](https://adoptopenjdk.net/)
* [An IDE](https://www.jetbrains.com/idea/download) -- you can also use Eclipse

Once you have downloaded and installed the necessary tools, 

* Go to [start.spring.io](http://start.spring.io).
* Choose a Gradle Project with Java as the language.
* Enter a Group and Artifact ID (I chose "com.abrahamserafino" and "employeeledger").
* Choose Jar packaging and Java version 11, and Spring Boot version 2.2.6.
* Add the following dependencies:
    * Rest Repositories
    * Lombok
    * Spring Data JPA
    * H2 Database
* Click the "Generate" bottom at the bottom of the page to download a .zip file containing the Spring Boot starter
project.
* Unzip the file into a local folder of your choice.
* Go to the folder in a command terminal and issue the following command:

    ```./gradlew clean bootRun```

* Navigate to [http://localhost:8080](http://localhost:8080) to ensure something is running there. 

## Next Step ##

[Step 1](https://bitbucket.org/kungfuandjavascript/employeeledger/src/step1)
