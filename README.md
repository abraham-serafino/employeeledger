# Employee Ledger #

Step-by-step instructions for creating and deploying a secure Spring Data REST application using Docker on AWS.

## Step 4 -- Create a Docker Container ##

* Add the Jib Docker plugin to your Gradle build:

```groovy
plugins {
	id 'com.google.cloud.tools.jib' version '1.8.0' // <--
	id 'org.springframework.boot' version '2.2.6.RELEASE'
	id 'io.spring.dependency-management' version '1.0.9.RELEASE'
	id 'java'
}
// ...
```

*  Build the docker container:

``./gradlew jibDockerBuild --image=abrahamserafino/employeeledger``

* Test your docker container:

(You will need to install docker for this step - see
[https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)).

``docker run -p 8080:8080 -t abrahamserafino/employeeledger``

* Navigate to [http://localhost:8080](http://localhost:8080) and login with `test` and `password`.

* Go back and test the application with Swagger:

[http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html) 

## Go Forward ##

[Step 5 - Deploy to AWS](https://github.com/abraham-serafino/employeeledger/tree/step5)

## Go Back ##

[Step 3 - Secure Your Application](https://github.com/abraham-serafino/employeeledger/tree/step3)
