# Student CRUD API

A simple RESTful API for managing student records built with Go and SQLite.

## Features

- **Create Student** - POST `/api/students`
- **Get Student by ID** - GET `/api/students/{id}`
- **Get All Students** - GET `/api/students`
- **Update Student** - PUT `/api/students/{id}`
- **Delete Student** - DELETE `/api/students/{id}`

## Tech Stack

- **Go 1.25.1** - Programming language
- **SQLite** - Database
- **Clean Architecture** - Repository pattern with storage interface
- **Validation** - Request validation using `go-playground/validator`
- **Configuration** - YAML-based configuration with environment variables

## Project Structure

```
cmd/student-crud-go/          # Application entry point
├── main.go                  # Server setup and route registration
internal/
├── config/                  # Configuration management
│   └── config.go
├── http/handlers/student/   # HTTP handlers
│   └── student.go
├── storage/                 # Storage interface
│   └── storage.go
├── storage/sqlite/          # SQLite implementation
│   └── sqlite.go
└── types/                   # Data types
    └── types.go
```

## Getting Started

### Prerequisites

- Go 1.25.1 or higher
- SQLite

### Installation

1. Clone the repository
2. Install dependencies:
   ```bash
   go mod download
   ```

### Configuration

Create a configuration file (e.g., `config/local.yaml`):

```yaml
env: "local"
storage_path: "path/to/your/database.db"
http_server:
  address: ":8080"
```

### Running the Application

1. Set the configuration path:

   ```bash
   export CONFIG_PATH=config/local.yaml
   ```

2. Run the application:
   ```bash
   go run cmd/student-crud-go/main.go
   ```

The server will start on the address specified in your configuration file.

## API Endpoints

### Create Student

- **POST** `/api/students`
- **Request Body**:
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "age": 20
  }
  ```

### Get Student by ID

- **GET** `/api/students/{id}`
- **Response**: Student object

### Get All Students

- **GET** `/api/students`
- **Response**: Array of student objects

### Update Student

- **PUT** `/api/students/{id}`
- **Request Body**: Complete student object (all fields required)

### Delete Student

- **DELETE** `/api/students/{id}`
- **Response**: 204 No Content on success

## Data Model

```go
type Student struct {
    Id    int64  `json:"id"`
    Name  string `json:"name" validate:"required"`
    Email string `json:"email" validate:"required"`
    Age   int    `json:"age" validate:"required"`
}
```

## Architecture

The application follows clean architecture principles:

1. **Handler Layer** - HTTP request/response handling
2. **Storage Interface** - Abstraction for data operations
3. **Repository Layer** - SQLite database implementation

This separation allows for easy testing and potential database switching.
