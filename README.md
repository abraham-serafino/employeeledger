# Employee Ledger #

Step-by-step instructions for creating and deploying a secure Spring Data REST application using Docker on AWS.

## Step 3 -- Secure Your API ##

* Add Spring Security to your Gradle Build (`build.gradle`):

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation 'org.springframework.boot:spring-boot-starter-data-rest'
    implementation 'org.springframework.boot:spring-boot-starter-security'
    implementation 'org.springframework.security:spring-security-test'
    // ...
```

*  Configure Spring Security using Java config:

``src/main/java/com/abrahamserafino/employeeledger/WebSecurityConfig.java``:

```java
package com.abrahamserafino.employeeledger;

import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.formLogin();

        http.authorizeRequests()
                .antMatchers("/*")
                    .hasRole("user");
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .inMemoryAuthentication()
            .withUser("test")
            .password("{noop}password")
            .roles("user");
    }
}

```

* Restart your application with `Ctrl+C` followed by `./gradlew clean bootRun`

* Now you will be asked to login with `test` and `password` before you can navigate to
[http://localhost:8080](http://localhost:8080).

* After logging in, you can go back to Swagger:
[http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html) 

## Go Forward ##

[Step 4 - Create a Docker Container](https://bitbucket.org/kungfuandjavascript/employeeledger/src/step4)

## Go Back ##

[Step 2 - Secure Your API](https://bitbucket.org/kungfuandjavascript/employeeledger/src/step2)