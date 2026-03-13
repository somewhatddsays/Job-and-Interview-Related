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

### What's the difference between @Value and @ConfigurationProperties?
- **@Value** &mdash; For individual properties:
    ```java
    @Component
    public class MyService{
        @Value("${app.name}")
        private String appName;
        
        @Value("${app.timeout:30}")
        private int timeout; //Default value: 30
    }
    ```
- **@ConfigurationProperties** &mdash; For grouped properties

    ```java
    @ConfigurationProperties(prefix = "app")
    @Component
    public class AppProperties {
        private String name;
        private int timeout;
        private Database database;
    
        // Getters and setters
        public static class Database {
            private String url;
            private String username;
            // Getters and setters
        }
    }
    ```
**When to use**:
* `@Value`: Simple, individual properties.
* `@ConfigurationProperties`: Complex, hierarchical configuration with validation.


### How do you handle different environments (dev/test/prod)?
Use Spring Profiles:
```
# application .ymL (default)
spring:
    profiles :
        active: dev
                
---

# application -dev.yml
spring:
    datasource:
        url: jdbc
logging:
    level :
        com.myapp: DEBUG

---

# application-prod.ymL
spring:
    datasource:
        url: jdbc :mysql : //prod-server:3306/proddb
logging:
    level :
        com.myapp: UARN
```
**Active Profiles:**

| Method                 | Value                                |
|:-----------------------|:-------------------------------------|
| `Command line`         | --spring.profiles.active=prod        |
| `Environment variable` | SRPING_PROFILES_ACTIVE=prod          |
| `Code`                 | @ActiveProfiles("test")(for testing) |

### How do you validate configuration properties?
Use **Bean Validation annotations**:

```
@Configuration Properties (prefix "app")
@Validated
@Component
public class AppProperties {
    @NotBlank
    private String name;
    
    @Min(1)
    @Max(3600)
    private int timeout;
    
    @Email
    private String admin Email;
    
    @Valid
    private Database database;
    
    // Getters and setters
}
```

## Data Access & JPA
### What is Spring Data JPA and how does it work?
Spring Data JPA is a layer on top of JPA that provides:

| Feature                  | Description                        |
|:-------------------------|:-----------------------------------|
| `Repository abstraction` | Eliminates boilerplate code        |
| `Query derivation`       | Creates queries from method names. |
| `Custom queries`         | Support for JPQL and native SQL    |
| `Pagination and sorting` | Built-in support                   |

```
@Entity
@Table(name = "users")
public class User {
   @Id
   @GeneratedValue(strategy GenerationType. IDENTITY)
   private Long id;
   @Column(nullable false, unique true)
   private String email;
        
   private String firstName;
   private String lastName;
        
   // Constructors, getters, setters
}
    
public interface UserRepository extends JpaRepository<User, Long> {
   //Query derivation
   List<User> findByFirstNameAndLastName (String firstName, String lastName);
  
   // Custom query
   @Query("SELECT u FROM User u WHERE u.email LIKE %:domain%")
   List<User> findByEmailDomain (@Param("domain") String domain);
  
   // Native query
   @Query (value = "SELECT FROM users WHERE created_date> ?1", nativeQuery = true)
   List<User> findRecentUsers (LocalDateTime date);
}
```

### What are the different types of relationships in JPA?
PA supports four relationship types:
* One-to-One:

```aiignore
@Entity
public class User{
    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "profile_id")
    private UserProfile profile;
}
```

* One-to-Many

```aiignore
@Entity
public class Department{
    @OneToMany (mappedBy = "department", cascade = CascadeType.ALL)
    private List<Employee>  employees;
}
```

* Many-to-One

```aiignore
@Entity
public class Employee{
    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;
}
```

* Many-to-Many:

```aiignore
@Entity
public class Student{
    @ManyToMany
    @JoinTable{
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    }
    private Set<Course> courses;
}
```

### How do you handle transactions in Spring Boot?
Use the @Transactional annotation:

```java
@Service
@Transactional
public class UserService {

    @Transactional(readOnly = true)
    public User findById(Long id) {
        return userRepository.findById(id)
                .orElseThrow(() -> new UserNotFoundException(id));
    }

    @Transactional(rollbackFor = Exception.class)
    public User createUser(User user) {
        validateUser(user);
        return userRepository.save(user);
    }

    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void auditUserAction(String action) {
        // This runs in a separate transaction
        auditRepository.save(new AuditLog(action));
    }
}
```
**Transactional Attributes**

| Method        | Use                                      |
|:--------------|:-----------------------------------------|
| `readOnly`    | Optimization for read-only operations    |
| `rollbackFor` | Specify exceptions that trigger rollback |
| `propagation` | Control transaction boundaries           |
| `isolation`   | Set isolation level                      |
| `timeout`     | Transaction timeout                      |


## Security & Authentication

### How do you secure a Spring Boot Application?

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(authz -> authz
                .requestMatchers("/api/public/**").permitAll()
                .requestMatchers("/api/admin/**").hasRole("ADMIN")
                .anyRequest().authenticated()
            )
            .oauth2Login(oauth2 -> oauth2
                .loginPage("/login")
            )
            .jwt(jwt -> jwt
                .jwtAuthenticationConverter(jwtAuthenticationConverter())
            );

        return http.build();
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```
### What are the different authentication mechanism in Spring Security?
Spring Security supports multiple authentication mechanisms:

| Type                          | Description                                   |
|:------------------------------|:----------------------------------------------|
| **Form-based**                | Traditional username/ password                |
| **HTTP Basic Authentication** | Base64 encoded credentials                    |
| **JWT Tokens**                | Stateless token-based authentication          |
| **OAuth 2.0**                 | Third-party authentication (Google, Facebook) |
| **SAML 2.0**                  | Enterprise single sign-on                     |
| **X.509 certificates**        | Certificate-based authentication              |

### How do you implement JWT authentication?

JWT implementation involves token generation and validation.

```java
@Service
public class JwtService {

    private final String SECRET_KEY = "mySecretKey";

    public String generateToken(UserDetails userDetails) {
        return Jwts.builder()
                .setSubject(userDetails.getUsername())
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + 1000 * 60 * 60 * 10))
                .signWith(SignatureAlgorithm.HS256, SECRET_KEY)
                .compact();
    }

    public Boolean validateToken(String token, UserDetails userDetails) {
        final String username = extractUsername(token);
        return (username.equals(userDetails.getUsername()) &&
                !isTokenExpired(token));
    }
}

@Component
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain filterChain) throws ServletException, IOException {

        String authHeader = request.getHeader("Authorization");
        if (authHeader != null && authHeader.startsWith("Bearer ")) {
            String token = authHeader.substring(7);
            String username = jwtService.extractUsername(token);

            if (username != null &&
                SecurityContextHolder.getContext().getAuthentication() == null) {
                UserDetails userDetails =
                    userDetailsService.loadUserByUsername(username);
                if (jwtService.validateToken(token, userDetails)) {
                    UsernamePasswordAuthenticationToken authToken =
                        new UsernamePasswordAuthenticationToken(
                            null, userDetails.getAuthorities());
                    SecurityContextHolder.getContext().setAuthentication(authToken);
                }
            }
        }
        filterChain.doFilter(request, response);
    }
}
```

## Testing Strategies

### What are the different types of tests in Spring Boot?
Spring Boot supports multiple testing layers:

* **Unit Tests**

  ```java
  @ExtendWith(MockitoExtension.class)
  class UserServiceTest {
  
      @Mock
      private UserRepository userRepository;
  
      @InjectMocks
      private UserService userService;
  
      @Test
      void shouldCreateUser() {
          // Given
          User user = new User("john@example.com", "John", "Doe");
          when(userRepository.save(any(User.class))).thenReturn(user);
  
          // When
          User result = userService.createUser(user);
  
          // Then
          assertThat(result.getEmail()).isEqualTo("john@example.com");
          verify(userRepository).save(user);
      }
  }
  ```


* **Integration Tests**

  ```java
  @SpringBootTest
  @AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
  @Testcontainers
  class UserRepositoryIntegrationTest {
  
      @Container
      static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:13")
              .withDatabaseName("testdb")
              .withUsername("test")
              .withPassword("test");
  
      @Autowired
      private UserRepository userRepository;
  
      @Test
      void shouldFindUserByEmail() {
          // Given
          User user = new User("test@example.com", "Test", "User");
          userRepository.save(user);
  
          // When
          Optional<User> found =
              userRepository.findByEmail("test@example.com");
  
          // Then
          assertThat(found).isPresent();
          assertThat(found.get().getFirstName()).isEqualTo("Test");
      }
  }
  ```

### What are Spring Boot test slices?
Test slices load only specific parts of the application context:

| Annotation   | Purpose                   | Loaded Components                   |
|:-------------|:--------------------------|:------------------------------------|
| @WebMvcTest  | Test controllers          | Web layer, MockMvc                  |
| @DataJpaTest | Test repositories         | JPA repositories, TestEntityManager |
| @JsonTest    | Test JSON serialization   | JSON mappers                        |
| @WebFluxTest | Test reactive controllers | WebFlux components                  |

```java
@WebMvcTest(UserController.class)
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    void shouldReturnUser() throws Exception {
        // Given
        User user = new User("john@example.com", "John", "Doe");
        when(userService.findById(1L)).thenReturn(user);

        // When & Then
        mockMvc.perform(get("/api/users/1"))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.email").value("john@example.com"))
                .andExpect(jsonPath("$.firstName").value("John"));
    }
}
```


### How do you test security in Spring Boot?
Use security test annotations:
```java
@SpringBootTest
@AutoConfigureTestDatabase
class SecurityIntegrationTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    @WithMockUser(roles = "ADMIN")
    void shouldAllowAdminAccess() throws Exception {
        mockMvc.perform(get("/api/admin/users"))
                .andExpect(status().isOk());
    }

    @Test
    @WithMockUser(roles = "USER")
    void shouldDenyUserAccess() throws Exception {
        mockMvc.perform(get("/api/admin/users"))
                .andExpect(status().isForbidden());
    }

    @Test
    void shouldRequireAuthentication() throws Exception {
        mockMvc.perform(get("/api/users"))
                .andExpected(status().isUnauthorized());
    }
}
```





**Original Poster**: [coding.sight](https://www.instagram.com/coding.sight/)