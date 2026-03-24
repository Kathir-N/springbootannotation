# springbootannotation
# Spring Boot Annotations Guide

A comprehensive reference project demonstrating all essential Spring Boot annotations with practical examples.

---

## 📁 Project Structure

```
src/main/java/com/learn/annotations/
│
├── SpringBootAnnotationsGuideApplication.java   # @SpringBootApplication
│
├── config/                # Configuration & Properties
│   └── AppConfig.java     # @Configuration, @Bean, @Value, @ConfigurationProperties
│
├── di/                    # Dependency Injection
│   └── NotificationService.java   # @Primary, @Qualifier
│
├── entity/                # JPA Entities
│   └── Note.java          # @Entity, @Id, @Column, Validation annotations
│
├── scope/                 # Bean Scopes
│   └── RequestScopedBean.java     # @RequestScope
│
├── stereotype/            # Component Stereotypes
│   ├── MyComponent.java   # @Component
│   ├── MyService.java     # @Service
│   └── MyRepository.java  # @Repository
│
├── transactional/         # Transaction Management
│   └── NoteService.java   # @Transactional
│
└── web/                   # REST Controllers
    └── GuideController.java   # @RestController, @RequestMapping, etc.
```

---

## 📚 Annotations Reference

### 1. Application Bootstrap

| Annotation | Purpose |
|------------|---------|
| `@SpringBootApplication` | Main entry point — combines `@Configuration`, `@EnableAutoConfiguration`, `@ComponentScan` |
| `@EnableAutoConfiguration` | Auto-configures beans based on classpath dependencies |
| `@ComponentScan` | Scans packages for components to register as beans |
| `@Configuration` | Marks class as source of bean definitions |indicating that class declared 1 or more beans that may be processed by spring conatiner

---

### 2. Component Stereotypes (Bean Discovery)

| Annotation | Layer | Use Case |
|------------|-------|----------|
| `@Component` | Generic | Base stereotype — use when no other fits | u cannot autowire any class if it is not marked with component......... turns class into spring beans at auto scan
| `@Service` | Business | Business logic, orchestration |
| `@Repository` | Data | Data access, persistence |
| `@Controller` | Presentation | MVC controllers (returns views) |
| `@RestController` | API | REST APIs (= `@Controller` + `@ResponseBody`) |

📍 **Location:** `com.learn.annotations.stereotype`

---

### 3. Dependency Injection

| Annotation | Purpose |
|------------|---------|
| `@Autowired` | Injects dependencies (constructor injection preferred) |
| `@Qualifier("beanName")` | Selects specific bean when multiple of same type exist |
| `@Primary` | Default bean when `@Qualifier` not specified |
| `@Value("${prop}")` | Injects value from `application.properties` |

📍 **Location:** `com.learn.annotations.di`, `com.learn.annotations.config`

---

### 4. Configuration

| Annotation | Purpose |
|------------|---------|
| `@Configuration` | Defines configuration class |
| `@Bean` | Registers method return value as Spring bean |
| `@ConfigurationProperties(prefix="app")` | Type-safe binding of properties |
| `@Value` | Property injection: `${app.name}` or SpEL `#{...}` |

📍 **Location:** `com.learn.annotations.config`

---

### 5. Web / REST Annotations

| Annotation | Purpose |
|------------|---------|
| `@RequestMapping` | Base URL for controller |
| `@GetMapping` | HTTP GET method |
| `@PostMapping` | HTTP POST method |
| `@PutMapping` | HTTP PUT method |
| `@DeleteMapping` | HTTP DELETE method |
| `@PathVariable` | Extract from URL: `/notes/{id}` |
| `@RequestParam` | Query parameter: `?name=value` |
| `@RequestBody` | Bind JSON request body to object |
| `@RequestHeader` | Extract HTTP header |
| `@ResponseStatus` | Set HTTP status code |
| `@Valid` | Trigger validation on object |

📍 **Location:** `com.learn.annotations.web`

---

### 6. JPA / Database

| Annotation | Purpose |
|------------|---------|
| `@Entity` | Marks class as JPA entity (database table) |
| `@Table(name="x")` | Custom table name |
| `@Id` | Primary key |
| `@GeneratedValue` | Auto-generate ID |
| `@Column` | Column customization |
| `@Transactional` | Wrap method in database transaction |

📍 **Location:** `com.learn.annotations.entity`, `com.learn.annotations.transactional`

---

### 7. Validation (JSR-303/380)

| Annotation | Purpose |
|------------|---------|
| `@Valid` / `@Validated` | Trigger validation |
| `@NotNull` | Must not be null |
| `@NotBlank` | String not null/empty/whitespace |
| `@Size(min, max)` | Length constraints |
| `@Email` | Valid email format |
| `@Min` / `@Max` | Numeric range |

📍 **Location:** `com.learn.annotations.entity`

---

### 8. Bean Scope

| Annotation | Scope | Use Case |
|------------|-------|----------|
| *(default)* | Singleton | One instance per container |
| `@RequestScope` | Request | New bean per HTTP request |
| `@SessionScope` | Session | One per user session |
| `@Scope("prototype")` | Prototype | New instance each injection |

📍 **Location:** `com.learn.annotations.scope`

---

## 🚀 API Endpoints

### Test the Annotations in Action

| Method | URL | Demonstrates |
|--------|-----|--------------|
| `GET` | `/api/guide/greet/YourName` | `@PathVariable` |
| `GET` | `/api/guide/greet?name=Alice` | `@RequestParam` |
| `GET` | `/api/guide/headers` | `@RequestHeader` |
| `GET` | `/api/guide/scope/demo` | `@RequestScope` |
| `GET` | `/api/guide/notes` | `@Repository`, JPA |
| `POST` | `/api/guide/notes` | `@RequestBody`, `@Valid` |
| `GET` | `/api/guide/notes/{id}` | `@PathVariable` |
| `PUT` | `/api/guide/notes/{id}` | `@Valid` validation |
| `DELETE` | `/api/guide/notes/{id}` | `@ResponseStatus` |
| `GET` | `/api/guide/notify/email` | `@Primary` |
| `GET` | `/api/guide/notify/sms` | `@Qualifier` |

---
Relationship   | Example                  | Owner Side                     |
|----------------|--------------------------|--------------------------------|
| `@OneToOne`    | User → Profile           | Either (with `@JoinColumn`)    |
| `@OneToMany`   | Department → Employees   | `@ManyToOne` side              |
| `@ManyToOne`   | Employees → Department   | This side (has FK)             |
| `@ManyToMany`  | Students ↔ Courses       | Either (with `@JoinTable`)     |


```

┌─────────────────────────────────────────────────────────────┐
│              SPRING BOOT ANNOTATIONS CHEAT SHEET            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  BOOTSTRAP                                                  │
│    @SpringBootApplication  → Main class                     │
│    @Configuration          → Config class                   │
│    @Bean                   → Register bean                  │
│                                                             │
│  COMPONENTS                                                 │
│    @Component   → Generic bean                              │
│    @Service     → Business logic                            │
│    @Repository  → Data access                               │
│    @Controller  → MVC controller                            │
│    @RestController → REST API                               │
│                                                             │
│  INJECTION                                                  │
│    @Autowired   → Inject dependency                         │
│    @Qualifier   → Select specific bean                      │
│    @Primary     → Default bean                              │
│    @Value       → Inject property                           │
│                                                             │
│  WEB                                                        │
│    @GetMapping / @PostMapping / @PutMapping / @DeleteMapping│
│    @PathVariable  → /users/{id}                             │
│    @RequestParam  → ?name=value                             │
│    @RequestBody   → JSON body                               │
│                                                             │
│  JPA                                                        │
│    @Entity        → Database table                          │
│    @Id            → Primary key                             │
│    @Transactional → DB transaction                          │
│                                                             │
│  VALIDATION                                                 │
│    @Valid      → Trigger validation                         │
│    @NotNull    → Required field                             │
│    @NotBlank   → Required string                            │
│    @Size       → Length limit                               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
--------------------- **Custom Annotation**-------------
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Indexed
public @interface Component {
}


## 📄 License

This project is open source and available under the [MIT License](LICENSE).
