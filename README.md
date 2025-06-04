# WishWhiz - User Authentication Service

This repository contains a Spring Boot application that demonstrates JWT-based user authentication and integrates with a Eureka server for service discovery. The project follows standard Maven structure and relies on Spring Security, Spring Data JPA, and other common Spring Boot components.

## Project Structure

```
WishWhiz/
├── pom.xml                # Maven build file
├── mvnw, mvnw.cmd         # Maven wrapper scripts
└── src/
    ├── main/
    │   ├── java/com/app/auth/user_authentication_service/
    │   │   ├── config/      # Security and data initialization
    │   │   ├── controller/  # REST endpoints for authentication
    │   │   ├── dto/         # AuthRequest and AuthResponse objects
    │   │   ├── model/       # JPA entity representing a user
    │   │   ├── repository/  # Spring Data repository interface
    │   │   ├── service/     # Service interface and implementation
    │   │   ├── util/        # JWT utility for token generation/validation
    │   │   └── UserAuthenticationServiceApplication.java
    │   └── resources/
    │       └── application.yml
    └── test/
        └── java/com/app/auth/user_authentication_service/
            └── UserAuthenticationServiceApplicationTests.java
```

## Key Components

- **Spring Boot Application**: `UserAuthenticationServiceApplication` boots the service and registers with Eureka using `@EnableDiscoveryClient`.
- **Model & Repository**: `User` is a simple JPA entity and `UserRepository` provides CRUD operations via `JpaRepository`.
- **DTOs**: `AuthRequest` and `AuthResponse` carry login credentials and JWT tokens.
- **Service Layer**: `AuthService` and `AuthServiceImpl` handle authentication and token generation.
- **Controller**: `AuthController` exposes endpoints under `/auth` for login, token issuance, and demo admin/user routes.
- **Security & Configuration**: `SecurityConfig` configures Spring Security with in-memory users and form login. `DataInitializerConfig` optionally seeds the database with default users at startup.
- **JWT Utility**: `JwtUtil` builds and validates JWT tokens using a Base64-encoded secret key. Replace this key with a secure value for production environments.
- **Configuration File**: `application.yml` sets server port, MySQL database details, Eureka client settings, actuator endpoints, and Feign/HTTP client properties.
- **Testing**: The project currently includes a single context-loading test (`UserAuthenticationServiceApplicationTests`).

## Getting Started

1. **Database Setup**: Ensure a MySQL instance is running and update the connection details in `src/main/resources/application.yml` if necessary.
2. **Run with Maven**:
   ```bash
   ./mvnw spring-boot:run
   ```
3. **Access Endpoints**:
   - `POST /auth/login` – authenticate with username and password.
   - `POST /auth/authenticate` – alternative endpoint that returns a JWT.
   - `GET /auth/admin` – sample admin-only page (requires role `ADMIN`).
   - `GET /auth/user` – sample user page (requires role `USER`).

The application registers itself with Eureka (see `application.yml` for the Eureka URL). By default it listens on port `8080`.

## Future Improvements

- Add more robust tests covering authentication flows and role-based access.
- Consolidate in-memory and database user management approaches.
- Create additional documentation about deploying with Eureka and using Feign clients.

This repository serves as a starting point for exploring Spring Boot authentication using JWTs in a microservices environment.
