# MediSchedule - Sistema de Agendamento de Consultas Médicas

Plataforma backend de API REST para agendamento e gerenciamento de consultas médicas. Conecta pacientes e médicos de forma eficiente e segura.

## 📋 Pré-requisitos

- **Java 21+**
- **Maven 3.8+**
- **MySQL 8.0+**
- **Git**

## 🚀 Como Rodar o Projeto

### 1. Clone o repositório
```bash
git clone <url-do-repositorio>
cd estalinho-back
```

### 2. Configure as variáveis de ambiente

Crie um arquivo `.env` na raiz do projeto ou configure as variáveis do sistema:

```bash
DB_URL=jdbc:mysql://localhost:3306/estalinho
DB_USER=seu_usuario
DB_PASSWORD=sua_senha
```

Ou edite o arquivo `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/estalinho
spring.datasource.username=root
spring.datasource.password=sua_senha
```

### 3. Instale as dependências e compile

```bash
mvn clean install
```

### 4. Execute a aplicação

```bash
mvn spring-boot:run
```

A aplicação estará disponível em `http://localhost:8080`

## 📚 Endpoints da API

### Usuários

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/user/` | Listar todos os usuários |
| POST | `/user/` | Criar novo usuário |
| PUT | `/user/` | Atualizar usuário |
| DELETE | `/user/{id}` | Deletar usuário |

### Agendamentos

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/appointment/` | Listar todos os agendamentos |
| POST | `/appointment/` | Criar novo agendamento |
| PUT | `/appointment/` | Atualizar agendamento |
| DELETE | `/appointment/{id}` | Deletar agendamento |

## 📊 Modelo de Dados

### Usuário (TB_USUARIOS)
```json
{
  "id": "long",
  "cpf": "string (obrigatório)",
  "nome": "string (obrigatório)",
  "email": "string (obrigatório, válido)",
  "senha": "string (obrigatório)",
  "tipoUsuarioEnum": "MEDICO ou PACIENTE",
  "estadoUsuarioEnum": "ATIVO ou INATIVO",
  "dataInclusao": "LocalDate",
  "dataAlteracao": "LocalDate"
}
```

### Agendamento (TB_CONSULTAS)
```json
{
  "id": "long",
  "fkMedico": "long (obrigatório)",
  "fkPaciente": "long (obrigatório)",
  "dataConsulta": "LocalDateTime (obrigatório)",
  "estadoConsultaEnum": "AGENDADA, REALIZADA, CANCELADA",
  "dataInclusao": "LocalDate",
  "dataAlteracao": "LocalDate"
}
```

## 🏗️ Arquitetura do Projeto

```
src/main/java/Estalinho/estalinho/
├── EstalinhoApplication.java     # Classe principal
├── controller/                   # Controllers REST
│   ├── UserController.java
│   └── AppointmentController.java
├── service/                      # Lógica de negócio
│   ├── UserService.java
│   └── AppointmentService.java
├── repository/                   # Acesso a dados (JPA)
│   ├── UserRepository.java
│   └── AppointmentRepository.java
├── domain/
│   └── user/
│       ├── entity/              # Entidades JPA
│       │   ├── User.java
│       │   └── Appointment.java
│       ├── dto/                 # DTOs (Data Transfer Objects)
│       │   ├── user/
│       │   └── appointment/
│       └── Enum/                # Enumerações
│           ├── TipoUsuarioEnum.java
│           ├── EstadoUsuarioEnum.java
│           └── EstadoConsultaEnum.java
├── config/                      # Configurações
│   ├── CorsConfig.java
│   └── SecurityConfig.java
└── exception/                   # Tratamento de exceções
    ├── GlobalExceptionHandler.java
    ├── AlreadyExistException.java
    ├── DisableException.java
    ├── InvalidCredentialsException.java
    ├── InvalidParameterException.java
    └── NotFoundException.java
```

## 🛠️ Tecnologias Utilizadas

- **Spring Boot 3.4.4** - Framework web
- **Spring Data JPA** - ORM para persistência
- **Spring Security** - Autenticação e autorização
- **MySQL** - Banco de dados relacional
- **Lombok** - Redução de boilerplate
- **Jakarta Validation** - Validação de entrada
- **Maven** - Gerenciador de dependências

## 🔐 Segurança

- Spring Security configurado em `SecurityConfig.java`
- Validação de entrada com DTOs e anotações Jakarta
- CORS configurado em `CorsConfig.java`
- Tratamento centralizado de exceções

## 📝 Exemplo de Uso

### Criar um usuário
```bash
curl -X POST http://localhost:8080/user/ \
  -H "Content-Type: application/json" \
  -d '{
    "cpf": "123.456.789-00",
    "nome": "Dr. João Silva",
    "email": "joao@example.com",
    "senha": "senha123",
    "tipoUsuarioEnum": 0,
    "estadoUsuarioEnum": 0,
    "dataInclusao": "2024-05-10"
  }'
```

### Criar um agendamento
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

## 🧪 Testes

Execute os testes com:
```bash
mvn test
```

## 📄 Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo LICENSE para detalhes.

## 👤 Autor

Desenvolvido como projeto de aprendizado em Spring Boot e arquitetura REST.

## 📞 Suporte

Para dúvidas ou sugestões, abra uma issue no repositório.
