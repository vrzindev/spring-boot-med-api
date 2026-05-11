# MediSchedule - Medical Appointment Scheduling API

A robust backend REST API for managing medical appointments and user scheduling. Connects patients and doctors efficiently and securely.

**Read this in other languages:** [Português (Brasil)](README.pt-br.md)

## 📋 Prerequisites

- **Java 21+**
- **Maven 3.8+**
- **MySQL 8.0+**
- **Git**

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/vrzindev/spring-boot-med-api.git
cd spring-boot-med-api
```

### 2. Configure environment variables

Create a `.env` file or set system variables:

```bash
DB_URL=jdbc:mysql://localhost:3306/estalinho
DB_USER=your_username
DB_PASSWORD=your_password
```

Or edit `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/estalinho
spring.datasource.username=root
spring.datasource.password=your_password
```

### 3. Install dependencies and compile

```bash
mvn clean install
```

### 4. Run the application

```bash
mvn spring-boot:run
```

The application will be available at `http://localhost:8080`

## 📚 API Endpoints

### Users

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/user/` | List all users |
| POST | `/user/` | Create a new user |
| PUT | `/user/` | Update user |
| DELETE | `/user/{id}` | Delete user |

### Appointments

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/appointment/` | List all appointments |
| POST | `/appointment/` | Create a new appointment |
| PUT | `/appointment/` | Update appointment |
| DELETE | `/appointment/{id}` | Delete appointment |

## 📊 Data Model

### User (TB_USUARIOS)
```json
{
  "id": "long",
  "cpf": "string (required)",
  "nome": "string (required)",
  "email": "string (required, valid email)",
  "senha": "string (required)",
  "tipoUsuarioEnum": "MEDICO or PACIENTE",
  "estadoUsuarioEnum": "ATIVO or INATIVO",
  "dataInclusao": "LocalDate",
  "dataAlteracao": "LocalDate"
}
```

### Appointment (TB_CONSULTAS)
```json
{
  "id": "long",
  "fkMedico": "long (required)",
  "fkPaciente": "long (required)",
  "dataConsulta": "LocalDateTime (required)",
  "estadoConsultaEnum": "AGENDADA, REALIZADA, CANCELADA",
  "dataInclusao": "LocalDate",
  "dataAlteracao": "LocalDate"
}
```

## 🏗️ Project Architecture

```
src/main/java/Estalinho/estalinho/
├── EstalinhoApplication.java     # Main application class
├── controller/                   # REST Controllers
│   ├── UserController.java
│   └── AppointmentController.java
├── service/                      # Business logic
│   ├── UserService.java
│   └── AppointmentService.java
├── repository/                   # Data access layer (JPA)
│   ├── UserRepository.java
│   └── AppointmentRepository.java
├── domain/
│   └── user/
│       ├── entity/              # JPA Entities
│       │   ├── User.java
│       │   └── Appointment.java
│       ├── dto/                 # Data Transfer Objects
│       │   ├── user/
│       │   └── appointment/
│       └── Enum/                # Enumerations
│           ├── TipoUsuarioEnum.java
│           ├── EstadoUsuarioEnum.java
│           └── EstadoConsultaEnum.java
├── config/                      # Configuration classes
│   ├── CorsConfig.java
│   └── SecurityConfig.java
└── exception/                   # Exception handling
    ├── GlobalExceptionHandler.java
    ├── AlreadyExistException.java
    ├── DisableException.java
    ├── InvalidCredentialsException.java
    ├── InvalidParameterException.java
    └── NotFoundException.java
```

## 🛠️ Technologies

- **Spring Boot 3.4.4** - Web framework
- **Spring Data JPA** - ORM for data persistence
- **Spring Security** - Authentication and authorization
- **MySQL** - Relational database
- **Lombok** - Reduces boilerplate code
- **Jakarta Validation** - Input validation
- **Maven** - Dependency manager

## 🔐 Security Features

- Spring Security configuration in `SecurityConfig.java`
- Input validation with DTOs and Jakarta annotations
- CORS configuration in `CorsConfig.java`
- Centralized exception handling

## 💡 Usage Examples

### Create a user
```bash
curl -X POST http://localhost:8080/user/ \
  -H "Content-Type: application/json" \
  -d '{
    "cpf": "123.456.789-00",
    "nome": "Dr. John Smith",
    "email": "john@example.com",
    "senha": "password123",
    "tipoUsuarioEnum": 0,
    "estadoUsuarioEnum": 0,
    "dataInclusao": "2024-05-10"
  }'
```

### Create an appointment
```bash
curl -X POST http://localhost:8080/appointment/ \
  -H "Content-Type: application/json" \
  -d '{
    "fkMedico": 1,
    "fkPaciente": 2,
    "dataConsulta": "2024-05-15T14:30:00",
    "estadoConsultaEnum": 0,
    "dataInclusao": "2024-05-10"
  }'
```

## 🧪 Running Tests

Execute tests with:
```bash
mvn test
```

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👤 Author

Developed as a learning project for Spring Boot and REST API architecture.

## 📞 Support

For questions or suggestions, please open an issue on the repository.

---

**Other languages:** [Português (Brasil)](README.pt-br.md)
