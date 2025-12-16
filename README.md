# WorkPilot - Employee Management System

A comprehensive RESTful API backend for employee management built with Spring Boot 3.4.5. This production-ready application provides secure employee management, department organization, attendance tracking, salary management, and JWT-based authentication with OAuth2 support.

## Features

- **Employee Management**: Complete CRUD operations for employee records with pagination and sorting
- **Department Management**: Organize employees by departments with manager and worker assignments
- **Attendance Tracking**: Daily attendance records with check-in/check-out times and history
- **Salary Management**: Calculate, save, and track employee salary history with bonuses and deductions
- **JWT Authentication**: Secure token-based authentication with refresh token mechanism
- **OAuth2 Integration**: Support for OAuth2 client and resource server
- **Role-Based Access Control**: Multi-role authorization system
- **Auditing**: Automatic tracking of created/updated timestamps and users
- **API Documentation**: Interactive Swagger/OpenAPI documentation
- **Global Exception Handling**: Centralized error handling with detailed API responses
- **Input Validation**: Request validation using Jakarta Bean Validation
- **Actuator Endpoints**: Production-ready monitoring and health check endpoints

## Tech Stack

- **Framework**: Spring Boot 3.4.5
- **Language**: Java 21
- **Database**: MySQL 8.0+
- **ORM**: Spring Data JPA / Hibernate
- **Security**: Spring Security 6.5.0 + JWT (JJWT 0.11.5)
- **OAuth2**: Spring Security OAuth2 Client & Resource Server
- **API Documentation**: SpringDoc OpenAPI 2.8.8
- **Validation**: Jakarta Validation API
- **Object Mapping**: ModelMapper 3.1.1
- **Utilities**: Lombok
- **Build Tool**: Maven

## Prerequisites

Before running this application, ensure you have:

- Java 21 or higher
- Maven 3.8+
- MySQL 8.0+
- Git
- Postman or similar API testing tool (optional)

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/rushxbhh/WorkPilot-Project.git
cd WorkPilot-Project
```

### 2. Configure MySQL Database

Create a MySQL database:

```sql
CREATE DATABASE workpilot_db;
CREATE USER 'workpilot_user'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON workpilot_db.* TO 'workpilot_user'@'localhost';
FLUSH PRIVILEGES;
```

### 3. Configure Application Properties

Update `src/main/resources/application.properties`:

```properties
# Server Configuration
server.port=8080
server.servlet.context-path=/api

# MySQL Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/workpilot_db
spring.datasource.username=workpilot_user
spring.datasource.password=your_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA/Hibernate Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
spring.jpa.properties.hibernate.format_sql=true

# Enable JPA Auditing
spring.jpa.properties.hibernate.enable_lazy_load_no_trans=true

# JWT Configuration
jwt.secret=your_secret_key_here_minimum_256_bits
jwt.access-token-expiration=3600000
jwt.refresh-token-expiration=86400000

# Actuator Configuration
management.endpoints.web.exposure.include=health,info,metrics
management.endpoint.health.show-details=when-authorized

# Logging
logging.level.com.springbootweb=DEBUG
logging.level.org.springframework.security=DEBUG
logging.level.org.hibernate.SQL=DEBUG
```

### 4. Build the project

```bash
./mvnw clean install
```

Or on Windows:

```bash
mvnw.cmd clean install
```

### 5. Run the application

```bash
./mvnw spring-boot:run
```

The application will start on `http://localhost:8080/api`

## Project Structure

```
WorkPilot-Project/
├── src/
│   ├── main/
│   │   ├── java/com/springbootweb/spring/boot/web/
│   │   │   ├── advices/                     # Global exception & response handling
│   │   │   │   ├── ApiError.java
│   │   │   │   ├── ApiResponse.java
│   │   │   │   ├── GlobalExceptionHandler.java
│   │   │   │   └── GlobalResponseHandler.java
│   │   │   ├── auth/                        # Auditing configuration
│   │   │   │   └── AuditorAwareImpl.java
│   │   │   ├── clients/                     # External API clients
│   │   │   │   ├── impl/
│   │   │   │   │   └── ProductClientImpl.java
│   │   │   │   └── ProductClient.java
│   │   │   ├── configs/                     # Application configurations
│   │   │   │   ├── Mapper.java
│   │   │   │   ├── RestClientConfig.java
│   │   │   │   └── WebSecurityConfig.java
│   │   │   ├── controllers/                 # REST controllers
│   │   │   │   ├── AttendanceController.java
│   │   │   │   ├── AuthController.java
│   │   │   │   ├── DeptController.java
│   │   │   │   ├── EmployeeController.java
│   │   │   │   └── SalaryController.java
│   │   │   ├── dto/                         # Data Transfer Objects
│   │   │   │   ├── AttendanceDTO.java
│   │   │   │   ├── DeptDTO.java
│   │   │   │   ├── EmployeeDTO.java
│   │   │   │   ├── LoginDTO.java
│   │   │   │   ├── LoginResponseDTO.java
│   │   │   │   ├── LogoutRequestDTO.java
│   │   │   │   ├── SalaryDTO.java
│   │   │   │   ├── SignUpDTO.java
│   │   │   │   └── SignupResponseDTO.java
│   │   │   ├── entities/                    # JPA entities
│   │   │   │   ├── AttendanceEntity.java
│   │   │   │   ├── AuditableEntity.java
│   │   │   │   ├── DeptEntity.java
│   │   │   │   ├── EmployeeEntity.java
│   │   │   │   ├── SalaryEntity.java
│   │   │   │   ├── SessionEntity.java
│   │   │   │   └── UserEntity.java
│   │   │   ├── enums/                       # Enumerations
│   │   │   │   └── Role.java
│   │   │   ├── filters/                     # Security filters
│   │   │   │   └── JwtAuthFilter.java
│   │   │   ├── handler/                     # OAuth2 handlers
│   │   │   │   └── Oauth2SuccessHandler.java
│   │   │   ├── repositories/                # JPA repositories
│   │   │   │   ├── AttendanceRepository.java
│   │   │   │   ├── DeptRepository.java
│   │   │   │   ├── EmployeeRepository.java
│   │   │   │   ├── SalaryRepository.java
│   │   │   │   ├── SessionRepository.java
│   │   │   │   └── UserRepository.java
│   │   │   ├── services/                    # Business logic
│   │   │   │   ├── AttendanceService.java
│   │   │   │   ├── AuthService.java
│   │   │   │   ├── DeptService.java
│   │   │   │   ├── EmployeeService.java
│   │   │   │   ├── JWTService.java
│   │   │   │   ├── SalaryService.java
│   │   │   │   ├── SessionService.java
│   │   │   │   └── UserService.java
│   │   │   └── SpringBootWebApplication.java
│   │   └── resources/
│   │       ├── application.properties
│   │       └── static/
│   └── test/
├── data/                                    # Sample data files
├── mvnw
├── mvnw.cmd
├── pom.xml
└── README.md
```

## API Documentation

### Swagger UI

Access the interactive API documentation at:
```
http://localhost:8080/api/swagger-ui.html
```

OpenAPI JSON specification:
```
http://localhost:8080/api/v3/api-docs
```

## API Endpoints

### Authentication Endpoints

#### User Signup
```http
POST /signup
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "username": "johndoe",
  "password": "SecurePass123!",
  "roles": ["USER"]
}
```

**Response:**
```json
{
  "employeeid": 1,
  "name": "John Doe",
  "email": "john.doe@example.com",
  "username": "johndoe"
}
```

#### User Login
```http
POST /login
Content-Type: application/json

{
  "username": "johndoe",
  "password": "SecurePass123!"
}
```

**Response:**
```json
{
  "data": {
    "employeeid": 1,
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

**Note:** Refresh token is also set as an HTTP-only cookie.

#### Refresh Token
```http
POST /refresh
Cookie: refreshToken=your_refresh_token_here
```

**Response:**
```json
{
  "data": {
    "accessToken": "new_access_token",
    "refreshToken": "new_refresh_token"
  }
}
```

#### Logout
```http
POST /logout
Content-Type: application/json
Authorization: Bearer <access_token>

{
  "refreshToken": "your_refresh_token_here"
}
```

**Response:**
```json
{
  "data": "Logged out successfully"
}
```

### Employee Endpoints

All employee endpoints require authentication. Include the JWT token in the Authorization header:
```
Authorization: Bearer <your_access_token>
```

#### Get All Employees (with Pagination)
```http
GET /employees?page=0&size=5&sortby=employeeid
```

**Query Parameters:**
- `page` (default: 0) - Page number
- `size` (default: 5) - Items per page
- `sortby` (default: employeeid) - Sort field

**Response:**
```json
[
  {
    "employeeid": 1,
    "name": "John Doe",
    "email": "john.doe@example.com",
    "age": 30,
    "isactive": true,
    "joining": "2024-01-15",
    "workerdepartment": {
      "departmentid": 1,
      "title": "IT Department"
    }
  }
]
```

#### Get Employee by ID
```http
GET /employees/{employeeid}
```

#### Create New Employee
```http
POST /employees
Content-Type: application/json

{
  "name": "Jane Smith",
  "email": "jane.smith@example.com",
  "age": 28,
  "isactive": true,
  "joining": "2024-02-01",
  "username": "janesmith",
  "password": "SecurePass456!",
  "roles": ["USER"]
}
```

#### Update Employee (Full Update)
```http
PUT /employees/{employeeid}
Content-Type: application/json

{
  "name": "Jane Smith Updated",
  "email": "jane.smith@example.com",
  "age": 29,
  "isactive": true
}
```

#### Partial Update Employee
```http
PATCH /employees/{employeeid}
Content-Type: application/json

{
  "age": 30,
  "isactive": true
}
```

#### Delete Employee
```http
DELETE /employees/{employeeid}
```

### Department Endpoints

#### Get All Departments
```http
GET /departments
```

#### Get Department by ID
```http
GET /departments/{departmentid}
```

#### Create Department
```http
POST /departments
Content-Type: application/json

{
  "title": "Human Resources",
  "isactive": true
}
```

#### Update Department
```http
PUT /departments/{departmentid}
Content-Type: application/json

{
  "title": "Human Resources Updated",
  "isactive": true
}
```

#### Partial Update Department
```http
PATCH /departments/{departmentid}
Content-Type: application/json

{
  "isactive": false
}
```

#### Delete Department
```http
DELETE /departments/{departmentid}
```

#### Assign Manager to Department
```http
PUT /departments/{departmentid}/manager/{employeeid}
```

#### Get Department by Manager
```http
GET /departments/assigned/{managerid}
```

#### Assign Worker to Department
```http
PUT /departments/{departmentid}/worker/{employeeid}
```

### Attendance Endpoints

#### Record Attendance
```http
POST /attendances
Content-Type: application/json

{
  "employeeid": 1,
  "attendanceDate": "2024-12-16",
  "isPresent": true,
  "checkInTime": "09:00:00",
  "checkOutTime": "17:30:00",
  "remarks": "On time"
}
```

#### Get Today's Attendance
```http
GET /attendances/tattendance/today/{employeeid}
```

**Response:**
```json
{
  "id": 1,
  "attendanceDate": "2024-12-16",
  "isPresent": true,
  "checkInTime": "09:00:00",
  "checkOutTime": "17:30:00",
  "remarks": "On time",
  "employee": {
    "employeeid": 1,
    "name": "John Doe"
  }
}
```

#### Get Attendance History
```http
GET /attendances/attendance/history/{employeeid}
```

**Response:**
```json
[
  {
    "id": 1,
    "attendanceDate": "2024-12-16",
    "isPresent": true,
    "checkInTime": "09:00:00",
    "checkOutTime": "17:30:00"
  },
  {
    "id": 2,
    "attendanceDate": "2024-12-15",
    "isPresent": true,
    "checkInTime": "08:45:00",
    "checkOutTime": "17:15:00"
  }
]
```

### Salary Endpoints

#### Calculate and Save Salary
```http
POST /salaries/calandsave
Content-Type: application/json

{
  "employeeid": 1,
  "baseSalary": 75000.00,
  "bonuses": 5000.00,
  "deductions": 2000.00
}
```

**Response:**
```json
{
  "id": 1,
  "baseSalary": 75000.00,
  "bonuses": 5000.00,
  "deductions": 2000.00,
  "finalSalary": 78000.00,
  "employee": {
    "employeeid": 1,
    "name": "John Doe"
  }
}
```

#### Get Latest Salary
```http
GET /salaries/latest/{employeeid}
```

#### Get Salary History
```http
GET /salaries/history/{employeeid}
```

**Response:**
```json
[
  {
    "id": 2,
    "baseSalary": 80000.00,
    "bonuses": 6000.00,
    "deductions": 2500.00,
    "finalSalary": 83500.00
  },
  {
    "id": 1,
    "baseSalary": 75000.00,
    "bonuses": 5000.00,
    "deductions": 2000.00,
    "finalSalary": 78000.00
  }
]
```

## Database Schema

### Employees Table
```sql
CREATE TABLE employees (
    employeeid BIGINT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    age INT,
    isactive BOOLEAN DEFAULT TRUE,
    joining DATE,
    username VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    worker_dept_id BIGINT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    created_by VARCHAR(255),
    updated_by VARCHAR(255),
    FOREIGN KEY (worker_dept_id) REFERENCES departments(departmentid)
);
```

### Departments Table
```sql
CREATE TABLE departments (
    departmentid BIGINT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    isactive BOOLEAN DEFAULT TRUE,
    manager_id BIGINT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    created_by VARCHAR(255),
    updated_by VARCHAR(255),
    FOREIGN KEY (manager_id) REFERENCES employees(employeeid)
);
```

### Attendances Table
```sql
CREATE TABLE attendances (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    attendance_date DATE NOT NULL,
    is_present BOOLEAN NOT NULL,
    check_in_time TIME,
    check_out_time TIME,
    remarks VARCHAR(255),
    employee_id BIGINT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    created_by VARCHAR(255),
    updated_by VARCHAR(255),
    FOREIGN KEY (employee_id) REFERENCES employees(employeeid)
);
```

### Salaries Table
```sql
CREATE TABLE salaries (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    base_salary DOUBLE NOT NULL,
    bonuses DOUBLE,
    deductions DOUBLE,
    final_salary DOUBLE NOT NULL,
    employee_id BIGINT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    created_by VARCHAR(255),
    updated_by VARCHAR(255),
    FOREIGN KEY (employee_id) REFERENCES employees(employeeid)
);
```

### Sessions Table (JWT Refresh Tokens)
```sql
CREATE TABLE sessions (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    refresh_token VARCHAR(500) UNIQUE NOT NULL,
    user_id BIGINT NOT NULL,
    expires_at TIMESTAMP NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES employees(employeeid)
);
```

### Roles (Stored as ElementCollection)
```sql
CREATE TABLE employees_roles (
    employee_employeeid BIGINT NOT NULL,
    roles VARCHAR(50) NOT NULL,
    FOREIGN KEY (employee_employeeid) REFERENCES employees(employeeid)
);
```

## Security Configuration

### JWT Authentication Flow

1. **User Login**: User sends credentials to `/login`
2. **Token Generation**: Server validates credentials and generates:
   - Access Token (short-lived, e.g., 1 hour)
   - Refresh Token (long-lived, e.g., 24 hours)
3. **Token Storage**: 
   - Access token returned in response body
   - Refresh token set as HTTP-only cookie
4. **Authenticated Requests**: Client includes access token in Authorization header
5. **Token Refresh**: When access token expires, use refresh token to get new tokens
6. **Logout**: Invalidate refresh token session

### Security Features

- **Password Encryption**: BCrypt hashing algorithm
- **JWT Token Validation**: Signature verification and expiration check
- **HTTP-Only Cookies**: Secure refresh token storage
- **Role-Based Access**: Different permissions for different roles
- **Session Management**: Server-side session tracking for refresh tokens
- **CORS Configuration**: Configurable cross-origin resource sharing
- **CSRF Protection**: Token-based CSRF protection

### Roles

The system supports multiple roles defined in the `Role` enum:
- `USER` - Standard employee access
- `ADMIN` - Administrative access
- `HR` - Human resources access
- `MANAGER` - Department manager access

## Testing

### Unit Tests

Run unit tests:
```bash
./mvnw test
```

### Integration Tests

Run integration tests:
```bash
./mvnw verify
```

### Test Coverage

Generate test coverage report:
```bash
./mvnw test jacoco:report
```

View report at `target/site/jacoco/index.html`

### Manual Testing with cURL

**Login:**
```bash
curl -X POST http://localhost:8080/api/login \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "password": "SecurePass123!"
  }' \
  -c cookies.txt
```

**Get Employees:**
```bash
curl -X GET http://localhost:8080/api/employees \
  -H "Authorization: Bearer <your_access_token>"
```

**Create Attendance:**
```bash
curl -X POST http://localhost:8080/api/attendances \
  -H "Authorization: Bearer <your_access_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "employeeid": 1,
    "attendanceDate": "2024-12-16",
    "isPresent": true,
    "checkInTime": "09:00:00",
    "checkOutTime": "17:30:00"
  }'
```

## Monitoring & Health Checks

### Actuator Endpoints

Health check:
```http
GET /actuator/health
```

Application info:
```http
GET /actuator/info
```

Metrics:
```http
GET /actuator/metrics
```

## Configuration

### Environment Variables

For production deployment, use environment variables instead of hardcoded values:

```bash
export DB_URL=jdbc:mysql://production-db:3306/workpilot_db
export DB_USERNAME=prod_user
export DB_PASSWORD=secure_password
export JWT_SECRET=your_256_bit_secret_key
export JWT_ACCESS_EXPIRATION=3600000
export JWT_REFRESH_EXPIRATION=86400000
```

Update `application.properties`:
```properties
spring.datasource.url=${DB_URL}
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}
jwt.secret=${JWT_SECRET}
jwt.access-token-expiration=${JWT_ACCESS_EXPIRATION}
jwt.refresh-token-expiration=${JWT_REFRESH_EXPIRATION}
```

### Production Configuration

Create `application-prod.properties`:

```properties
# Production Database
spring.datasource.url=${DB_URL}
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}

# JPA Production Settings
spring.jpa.hibernate.ddl-auto=validate
spring.jpa.show-sql=false
spring.jpa.properties.hibernate.format_sql=false

# Logging
logging.level.com.springbootweb=INFO
logging.level.org.springframework=WARN

# Actuator
management.endpoints.web.exposure.include=health,info
```

Run with production profile:
```bash
java -jar target/spring-boot-web-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod
```

## Deployment

### Docker Deployment

Create `Dockerfile`:

```dockerfile
FROM openjdk:21-jdk-slim
WORKDIR /app
COPY target/spring-boot-web-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

Build and run:

```bash
# Build image
docker build -t workpilot-api .

# Run container
docker run -p 8080:8080 \
  -e DB_URL=jdbc:mysql://host.docker.internal:3306/workpilot_db \
  -e DB_USERNAME=root \
  -e DB_PASSWORD=password \
  -e JWT_SECRET=your_secret_key \
  workpilot-api
```

### Docker Compose

Create `docker-compose.yml`:

```yaml
version: '3.8'

services:
  mysql:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: workpilot_db
      MYSQL_USER: workpilot_user
      MYSQL_PASSWORD: workpilot_pass
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql

  workpilot-api:
    build: .
    ports:
      - "8080:8080"
    environment:
      DB_URL: jdbc:mysql://mysql:3306/workpilot_db
      DB_USERNAME: workpilot_user
      DB_PASSWORD: workpilot_pass
      JWT_SECRET: your_256_bit_secret_key_here
    depends_on:
      - mysql

volumes:
  mysql_data:
```

Run with Docker Compose:
```bash
docker-compose up -d
```

### Cloud Deployment (AWS/Azure/GCP)

**Build JAR:**
```bash
./mvnw clean package -DskipTests
```

**Deploy to:**
- **AWS Elastic Beanstalk**: Upload JAR file
- **Azure App Service**: Deploy via Azure CLI
- **Google Cloud Run**: Deploy containerized application
- **Heroku**: Use Heroku CLI with Procfile

## Error Handling

The API uses standardized error responses:

```json
{
  "timestamp": "2024-12-16T10:30:00",
  "status": 400,
  "error": "Bad Request",
  "message": "Validation failed",
  "path": "/api/employees",
  "errors": [
    {
      "field": "email",
      "message": "Email must be valid"
    }
  ]
}
```

### Common HTTP Status Codes

| Code | Description |
|------|-------------|
| 200 | OK - Request successful |
| 201 | Created - Resource created successfully |
| 400 | Bad Request - Invalid input |
| 401 | Unauthorized - Authentication required |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found - Resource not found |
| 500 | Internal Server Error - Server error |

## Best Practices

### Security
- Always use HTTPS in production
- Never commit sensitive credentials
- Rotate JWT secrets regularly
- Implement rate limiting
- Use strong password policies
- Enable CORS selectively
- Keep dependencies updated

### Performance
- Use pagination for large datasets
- Implement caching where appropriate
- Optimize database queries
- Use connection pooling
- Monitor with Actuator endpoints

### Development
- Follow REST API conventions
- Write comprehensive tests
- Document API changes
- Use meaningful commit messages
- Code review before merging

## Troubleshooting

### Common Issues

**Issue: "Access Denied" error**
- **Solution:** Verify JWT token is valid and not expired. Check user roles.

**Issue: Database connection refused**
- **Solution:** Ensure MySQL is running and credentials are correct.

**Issue: "Bean creation error"**
- **Solution:** Check for circular dependencies or missing @Component annotations.

**Issue: 401 Unauthorized on protected endpoints**
- **Solution:** Include `Authorization: Bearer <token>` header in requests.

**Issue: Refresh token not found**
- **Solution:** Ensure cookies are enabled and refresh token cookie is sent.

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Future Enhancements

- [ ] Email notifications for important events
- [ ] Leave management system
- [ ] Performance review module
- [ ] Document management
- [ ] Real-time notifications with WebSocket
- [ ] Export reports to PDF/Excel
- [ ] Mobile app integration
- [ ] Multi-tenancy support
- [ ] Advanced analytics dashboard
- [ ] Integration with third-party HR systems

## License

This project is open source and available under the [MIT License](LICENSE).

## Contact

For questions or support:
- GitHub: [@rushxbhh](https://github.com/rushxbhh)
- Repository: [WorkPilot-Project](https://github.com/rushxbhh/WorkPilot-Project)

---

**⚠️ Production Checklist:**
- [ ] Change default JWT secret
- [ ] Use environment variables for sensitive data
- [ ] Enable HTTPS/SSL
- [ ] Set up database backups
- [ ] Configure proper CORS policies
- [ ] Implement rate limiting
- [ ] Set up logging aggregation
- [ ] Enable monitoring and alerts
- [ ] Review security configurations
- [ ] Test all endpoints thoroughly
