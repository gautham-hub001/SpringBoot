# Introduction
Spring Boot is a popular spring framework
Aspect-oriented programming model
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
Bean Factory - IOC container. It serves the beans at runtime of the application. It maintains the class dependencies.
From the IOC container, objects can be injected as dependencies to other classes at startup or at runtime. It is mostly done at
startup, as they're added to the bean factory.
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

## To run the project
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

Note: You can also manually add dependencies to pom.xml using <dependency> tag. First fill <artifactId> then it will suggest you groupId
eg.
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
eg. h2 database
<dependency>
   <groupId>com.h2database</groupId>
   <artifactId>h2</artifactId>
</dependency>


External libraries shows the list of all the dependency libraries like logging (log4j, logback), json documentation (jackson core), testing (jsonpath),
J2EE(jakarta), embedded tomcat, unit testing (junit5) ...

# Create index.html
In src/main/resources/static create index.html file

## IOC Dependency Management
IOC container is triggered by main class
It builds specific objects only (only the objects which are referenced in main and the objects which are referenced 
from those objects). IOC container does the injection of specific classes into the parent class.

Generally, we do not interact with the IOC container. But we can using hooks like BeanFactory post processor/ bean processor.
Spring handles object intialization and instantiation based on the dependencies. Beans are instantiated in proper order by the bean factory.
If you create two beans which depend on each other, then spring will give you warnings during compilation.
Application context is what you interact with.

## Annotations
Natively present in Java. Not specially introduced in spring.
They provide metadata for our code
Often used for compile time or runtime instructions
eg. @test -> runtime instruction to inform test framework that it is a method for testing. 

## Proxies
Beans are proxied by one or more abstracts by spring
Annotations drive proxies
Proxy classes have to be called through the proxy itself for the behaviour to be added
If you have a method A that has transactional boundaries around it and another method B that also has different transactional boundaries around it.
If you call A and A calls B then the proxy only gets applied to A and not B because A is calling B locally, so it does not go through proxy interface again.


## Practice problem CH2-2 (Embedding a database into our application):
copy data.sql, schema.sql from Ex_Files_Learning_Spring_with_Spring_Boot/Exercise Files/CH02/02_02/02_02_begin/learning_spring/bin folder to src/main/resources folder

**application.properties**
Add this to help us visualize when the application gets started:
logging.level.org.springframework.jdbc.datasource.init.ScriptUtils=debug
Since we have written our own schema, we need to add this is **application.properties**
spring.jpa.hibernate.ddl-auto=none
Because by default, when we run application spring will import the schema and the data via scriptUtils from schema.sql and data.sql
and then, hibernate will remove those data tables and add new ones because it thinks it is controlling the schema.

In the logs you get when you run the application, HikariPool means thread pool is turned on.

Create a folder(package) called data in springpractice folder and create a file Room.java 