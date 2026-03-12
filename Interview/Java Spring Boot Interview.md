# Java Spring Boot Interview Cheat Sheet

## Table of Contents
1. Core Concepts & Annotations
2. Configuration & Properties
3. Data Access & JPA
4. Security & Authentication
5. Testing Strategies

---

## Core Concepts & Annotations
Spring Boot is an opi1nionated framework built on top of Spring Framework
that simplifies application development through:
- **Auto-configuration**: Automatically configures beans based on classpath.
- **Starter dependencies**:Pre-configured dependency bundles.
- **Embedded servers**:Built-in Tomcat, Jetty, or Undertow.
- **Production-ready features**: Actuator endpoints for monitoring.

**Key Difference**: Spring requires extensive XML/ Java configuration, while Spring Boot
provides sensible defaults and auto-configuration.

### Explain the `@SpringBootApplication` annotation.
@SpringBootApplication is a composite annotation that combines three
essential annotations:

 ```bash
 @SpringBootApplication
 // Equivalent to:
 // @Configuration + @EnableAutoConfiguration + @ComponentScan
 public class MyApplication{
   public static void main(String args[]){
     SpringApplication.run(MyApplication.class, args);
   }
 }
 ```

- **@Configuration**: Marks the class as a configuration class 
- **@EnableAutoConfiguration**: Enables Spring Boot's auto-configuration 
- **@ComponentScan**: Scans for components in the current package and sub-packages

## What are the most important Spring Boot Annotations?
Essential annotations categorized by purpose:

#### Core Annotation:
- **@SpringBootAppIication** - Main application class
- **@Component** - Generic Spring-managed component
- **@Service** • Business logic layer
- **@Repository** - Data access layer
- **@Controller** - Web layer (returns Views)
- **@RestController** - REST API layer (returns JSON/XML)

#### Dependencies:
* **@Autowired** -  Automatic dependency injection
* **@Qualifier** - Specify which bean to inject
* **@Primary** - Preferred bean when multiple candidates exist

#### Configuration:
* **@Configuration** - Configuration class
* **@Bean** - Method-level bean definition
* **@Value** - Inject property values
* **@ConfigurationProperties** - Bind properties to objects

### How does Spring Boot autoconfiguration work?
Autoconfiguration works through:
1. **Conditional annotations**:@ConditionalOnClass, @ConditionalOnMissingBean
2. **Configuration classes**: Located in spring-boot-autoconfiguration.jar
3. **spring.factories file**: Lists autoconfiguration classes
4. **Classpath scanning**: Detects dependencies and configures accordingly

```bash
@Configuration
@ConditionalOnClass(DataSource.class)
@ConditionalOnMissingBean(DataSource.class)
public class DataSourceAutoConfiguration{
//Auto-configuration Logic
}
```

---

### What is the difference between @Component, @Service, @Repository, and @Controller?
All are specialization of @Component with sematic meaning:

| Annotation    | Purpose                | Additional Feature       |
|:--------------|:-----------------------|:-------------------------|
| `@Component`  | Generic stereotype     | Basic component Scanning |
| `@Service `   | Business logic layer   | Semantic clarity         |
| `@Repository` | Data access layer      | Exception translation    |
| `@Controller` | Web layer              | Request mapping support  |

## Configuration & Properties
### How do you externalize configuration in Spring Boot?
Spring Boot supports multiple configuration sources in order of precedence:
* Command line arguments
* Environment variables
* application.properties/yml files
* @PropertySource annotations
* Default properties

\# _application.yml_
```

server:
    port: 8080
spring:
    datasource:
        url: jdbc: mysql://localhost:3306/mydb
        username: ${DB_USER:root}
        password: ${DB_PASSWORD:password}
```

## Data Access & JPA
## Security & Authentication
## Testing Strategies













