# Employee Ledger #

Step-by-step instructions for creating and deploying a secure Spring Data REST application using Docker on AWS.

## Step 2 -- Add Swagger ##

* Add the Swagger repository to your Gradle configuration file (`build.gradle`) under `repositories`:

```groovy
repositories {
    mavenCentral()
    jcenter { url 'http://oss.jfrog.org/artifactory/oss-snapshot-local/' }
}
```

* Add Swagger .jars to the `dependencies` section:

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation 'org.springframework.boot:spring-boot-starter-data-rest'
    compileOnly 'org.projectlombok:lombok'
    runtimeOnly 'com.h2database:h2'
    compile "io.springfox:springfox-swagger2:3.0.0-SNAPSHOT"
    compile "io.springfox:springfox-data-rest:3.0.0-SNAPSHOT"
    compile "io.springfox:springfox-swagger-ui:2.9.2"
    annotationProcessor 'org.projectlombok:lombok'
    testImplementation('org.springframework.boot:spring-boot-starter-test') {
        exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
    }
}
```

*  Configure Swagger using Java config:

``src/main/java/com/abrahamserafino/employeeledger/SpringFoxConfig.java``:

```java
package com.abrahamserafino.employeeledger;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.data.rest.configuration.SpringDataRestConfiguration;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2WebMvc;

@Configuration
@EnableSwagger2WebMvc
@Import(SpringDataRestConfiguration.class)
public class SpringFoxConfig {
    @Bean
    public Docket api() {
        return new Docket(DocumentationType.SWAGGER_2)
                .select()
                .apis(RequestHandlerSelectors.any())
                .paths(PathSelectors.any())
                .build();
    }
}

```

* Restart your application with `Ctrl+C` followed by `./gradlew clean bootRun`

* Now when you navigate to
[http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html), you should see a
UI that will allow you to interact with the RESTful API you created in Step 1.

* Try creating a few employees, modifying, deleting, and querying them.

## Go Forward ##

[Step 3 - Secure Your API](https://github.com/abraham-serafino/employeeledger/tree/step3)

## Go Back ##

[Step 1 - Create Repositories](https://github.com/abraham-serafino/employeeledger/tree/step1)
