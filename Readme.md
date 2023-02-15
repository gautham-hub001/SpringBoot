# Introduction
Spring Boot is a popular spring framework
You need to have jdk >=11 and Maven installed.
Spring supports Maven and Gradle

Spring framework provides comprehensive infrastructural support for Java applications.
Uses DRY (Don't Repeat Yourself) principle.

## Definitions:
1. POJO - Plain Old Java Object. Any class file that contains both attributes and methods. And these methods are not just getters and setters.
2. Java Beans - Simple objects with only getters and setters.
3. Spring Beans - POJOs that are configured by application context
4. DTO - Data Transfer Objects - Bean used to move state between logical layers of the application.

## Inversion of Control (IOC)
Bean Factory - IOC container. It serves the beans at runtime of the application.
1. It is a mechanism for dependency injection
2. Application context wraps the Bean Factory
3. Spring Boot provides auto-configuration of the Application context.

Uses of Spring Boot: web application, web service development, cron jobs, ETL applications, maintenance processes....

Features of spring boot:
1. Embedded tomcat (application server). In traditional JVM applications, we build a WAR file and drop it into application server.  But in 
   spring boot the application server exists in spring jar file.
2. Auto configuration of Application context (unlike in traditional spring)
3. Automatic servlet mapping. (No need to write any XML or java configuration)
4. Database support and Hibernate mapping/ JPA (Java Persistence API)

## Spring initializer - start.spring.io
**Steps:**
Search online for start.spring.io
configuration:
maven
group - com.gautham.spring
artifact - spring-practice
Package name - com.gautham.spring.spring-practice
packaging - jar
java - 19 - should be same as the one installed locally
spring boot 2.x . But downloaded 3.0.2 for now
dependencies: spring web

click on generate

unzip the folder
In Help.md
The original package name 'com.gautham.spring.spring-practice' is invalid and this project uses 'com.gautham.spring.springpractice' instead.

To run the project
cd spring-practice and type
1. For Build **mvn package**
2. For Run **java -jar target/spring-practice-0.0.1-SNAPSHOT.jar**
Tomcat is running on port 8080
3. localhost:8080  -> You get a 404 error page saying whitelabel error page, since you don't have any index.html and error page (/error)


In src/main/java/com/gautham/spring/springpractice > SpringPracticeApplication.java - Name given based on our artifact name

It has 2 imports - SpringApplication, SpringBootApplication
The annotation @SpringBootApplication tells the Application context to use this as a base for component scanning and auto-configuration
because it is @SpringBoot and not just @Configuration

In src/main/resources we have static and templates folders. These are generated because of Spring web dependency (package).
All the configuration of the Application context goes into application.properties file

mvnw and mvnw.cmd are present so that if maven is not installed in your machine, it will download it for you.

## pom.xml
It contains important details about the application like spring boot version, name of application, artifact, description, dependencies, plugins,...

External libraries shows the list of all the dependency libraries like logging (log4j, logback), json documentation (jackson core), testing (jsonpath),
J2EE(jakarta), embedded tomcat, unit testing (junit5) ...

# Create index.html
In src/main/resources/static create index.html file
