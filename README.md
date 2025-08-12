# Pharma_Project
# Pharma - Medication Management Application

Pharma is a web application developed with Spring Boot 3.4.5 allowing complete management of medications, suppliers, sales, users, as well as a statistical dashboard. The application also includes search, import/export features, and a secure authentication interface.

## Technologies Used

- Java 17
- Spring Boot 3.4.5
- Spring Data JPA
- Spring Security
- Spring Web
- Spring Validation
- Thymeleaf
- ModelMapper
- Lombok
- MySQL
- Maven

## Features

Authentication  
User registration and login

Role management (admin, user)

Securing sensitive pages with Spring Security

Medications  
Add, edit, delete, view

Search by name, reference, or category

Stock and quantity tracking

Suppliers  
Add, edit, delete, view

Link suppliers to medications

Search by name or location

Sales  
Record medication sales

Automatic calculation of total sale amount

Stock update after sales

Dashboard  
Overall statistics: monthly sales, low stock, top products

Graphical data visualization (to be integrated if needed)

Search  
Dynamic search on medications, suppliers, sales

Import / Export  
Data export in CSV or Excel formats

File import for bulk updates

## Application Containerization and Orchestration

### Objective  
This section presents the process of containerizing the application using Docker, as well as deploying and managing it with a container orchestrator, namely Docker Swarm. This approach ensures portability, scalability, and resilience of the Pharma application.

### Containerization with Docker  
Containerization packages the application with all its dependencies into an executable image called a container. This guarantees consistent execution across environments.

A Dockerfile has been created to build the pharma-app image.

This image is then used with Docker Compose to create the necessary containers:

- pharma-app: the web application container  
- pharma-db: the MySQL database container

### Orchestration with Docker Swarm  
Docker Swarm is Docker’s native container orchestration tool. It efficiently manages deployment, scaling, rolling updates, and fault tolerance.

Steps followed:

- Initialize Swarm:  
  `docker swarm init`

- Deploy the stack:  
  `docker stack deploy -c docker-compose.yml pharma_stack`

- Verify deployed services:  
  `docker stack services pharma_stack`

This system ensures high availability and load balancing among deployed services.

### Conclusion  
Thanks to Docker and Docker Swarm, the Pharma application is now containerized, easily deployable, and production-ready. This architecture allows centralized and efficient service management, better fault tolerance, and simplified scaling.

## Monitoring with Prometheus and Grafana  
The monitoring system was successfully implemented using Prometheus as a metrics collector and Grafana for visualization.

### Configuration  
Prometheus is configured to scrape metrics exposed by the Spring Boot application via its endpoint.  
Grafana is connected to Prometheus as a data source.  
The `up` metric confirms that the pharma-app instance is being monitored.

Example visible metric: ![t](https://github.com/user-attachments/assets/24ca9643-d061-480f-8433-cb5777db8770)

### Performance Visualization  
Custom dashboards have been created in Grafana to track key metrics:

- Average HTTP request latency  
- Request rates by status code (2xx, 4xx, 5xx)  
- Total request count over a given period

### Use of the rate() function  
Counters like `http_server_requests_seconds_count` are monotonically increasing. To extract meaningful data, the `rate()` function is used to get the variation over intervals.

## Applied Best Practices

- **Layered Architecture**  
  - Clear separation between `controllers`, `services`, `repositories`, and `models`.  
  - Facilitates maintenance, testing, and code comprehension.

- **Dependency Injection with Spring (@Autowired)**  
  - Promotes component decoupling.  
  - Simplifies unit testing.

- **Data Validation**  
  - Use of annotations like `@Valid`, `@NotEmpty`, `@Email` to ensure data quality.

- **Secure Password Management**  
  - Password encoding via `PasswordEncoder`.

- **Use of Lombok**  
  - Reduces boilerplate code (getters/setters, constructors).

---

## Design Patterns Used

- **Singleton (via @Service)**  
  - Spring services are instantiated once by the Spring container, ensuring a single instance.

- **Repository Pattern**  
  - Interfaces like `UserRepository` extend `JpaRepository` for abstract data access.

- **Dependency Injection**  
  - Dependencies are automatically injected by Spring, allowing loose coupling and easier testing.

---

## Unit Tests

This project includes unit tests to ensure reliability and quality of business logic.

Tested classes notably include:  
- `ClientServiceImpl`  
- `FournisseurServiceImpl`  
- `VenteServiceImpl`  

These tests cover main features of each service, such as:  
- Client management  
- Supplier management  
- Sales processing  

Tests are written using JUnit 5 and Mockito to mock dependencies.

---

To run tests, use the following Maven command:

mvn test


---
## Project Structure

src/

├── main/

│   ├── java/org/example/pharma/

│   │   ├── controllers/

│   │   ├── services/

│   │   ├── models/

│   │   ├── repositories/

│   │   └── PharmaApplication.java

│   └── resources/

│       ├── templates/

│       ├── static/

│       └── application.properties

└── test/

![ar](https://github.com/user-attachments/assets/a775b461-fd46-4a8c-a132-210713895cfa)


(https://github.com/user-attachments/assets/356a1883-6f8e-472f-9862-0dcd9ec7cce3)

## Database Configuration
Configure database connection information in the application.properties file:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/pharma_db
spring.datasource.username=root
spring.datasource.password=

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
server.port=8080
Running the Application
Clone the repository:
git clone https://github.com/ton-utilisateur/pharma.git
cd pharma


Run the application with Maven:
mvn spring-boot:run
Access the application:

http://localhost:8080/register

```





## Demonstration
link: https://youtu.be/J4Sg0SQTUhc

