# TodoList Backend API
API REST para gestión de tareas desarrollada con Spring Boot y MySQL.

![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.4.2-green)
![MySQL](https://img.shields.io/badge/MySQL-8.0-blue)

## 🛠️ Tecnologías principales
- 🍃 Spring Boot 3.4.2
- 📦 Spring Data JPA
- 🗃️ MySQL 8.0
- 🛠️ Maven
- 🔄 Hibernate

## 🏗️ Arquitectura del Sistema

```mermaid
graph TD
    Client["Aplicaciones Cliente"] -->|"HTTP Requests"| TC["TodoController"]
    TC -->|"Operaciones CRUD"| TR["TodoRepository"]
    TR -->|"Métodos JPA"| DB["Base de Datos MySQL"]
    TE["Entidad Todo"] -->|"Mapeada por"| TR
    TC -->|"Utiliza"| TE
    AP["TodolistProyectApplication"] -->|"Inicializa"| TC
    AP -->|"Inicializa"| TR
    AP -->|"Configura"| Props["application.properties"]
    Props -->|"Configura"| DB
```

### Capas de la Arquitectura

```mermaid
graph TD
    subgraph "Capa de Presentación"
        A["TodoController<br>/api/todos"]
    end
    
    subgraph "Capa de Acceso a Datos"
        C["TodoRepository<br>Interfaz JPA"]
    end
    
    subgraph "Capa de Base de Datos"
        D["Base de Datos MySQL"]
    end
    
    subgraph "Modelo de Dominio"
        E["Entidad Todo<br>(id, text, date, time, completed)"]
    end
    
    A -->|"utiliza"| C
    C -->|"interactúa con"| D
    C -->|"gestiona"| E
    A -->|"transfiere"| E
```

## 📁 Estructura del Proyecto

```
todolistapp-backend/
├── src/
│   └── main/
│       ├── java/com/app/todolist/
│       │   ├── controller/                         # Controladores REST
│       │   │   └── TodoController.java
│       │   ├── entity/                             # Entidades de base de datos
│       │   │   └── Todo.java
│       │   ├── repository/                         # Repositorios JPA
│       │   │   └── TodoRepository.java
│       │   └── TodolistProyectApplication.java     # Clase main
│       └── resources/
│           └── application.properties              # Config DB
└── pom.xml                                         # Dependencias Maven
```

## 🔧 Componentes Principales

### 1. Aplicación Principal
**`TodolistProyectApplication`** - Punto de entrada de la aplicación Spring Boot 

### 2. Controlador REST
**`TodoController`** - Maneja las peticiones HTTP y define los endpoints de la API REST

### 3. Repositorio de Datos
**`TodoRepository`** - Interfaz JPA que proporciona operaciones de acceso a datos 

### 4. Entidad de Dominio
**`Todo`** - Modelo de dominio que representa un elemento de tarea 

## 🌐 Endpoints de la API

| Método | Endpoint       | Función | Descripción                    |
|--------|----------------|---------|--------------------------------|
| GET    | /api/todos     | `getAllTodos()` | Obtener todas las tareas       |
| POST   | /api/todos     | `createTodo()` | Crear nueva tarea              |
| PUT    | /api/todos/{id}| `toggleComplete()` | Actualizar estado completado   |
| DELETE | /api/todos/{id}| `deleteTodo()` | Eliminar tarea                 | 

### Flujo de Peticiones

```mermaid
sequenceDiagram
    participant Cliente
    participant TC as TodoController
    participant TR as TodoRepository
    participant DB as MySQL Database
    
    %% Flujo GET
    Cliente->>TC: GET /api/todos
    TC->>TR: findAll()
    TR->>DB: SELECT * FROM todo
    DB-->>TR: Registros Todo
    TR-->>TC: List<Todo>
    TC-->>Cliente: Respuesta JSON
    
    %% Flujo POST
    Cliente->>TC: POST /api/todos<br>{text, date, time, completed}
    TC->>TR: save(todo)
    TR->>DB: INSERT INTO todo
    DB-->>TR: Confirmación
    TR-->>TC: Todo guardado
    TC-->>Cliente: Respuesta JSON
```

## 🚀 Instalación y Ejecución

### Prerrequisitos
- Java 17+
- Maven 3.6+
- MySQL 8.0+

### Ejecutar la aplicación
```bash
mvn spring-boot:run
```

### La API estará disponible en:
- http://localhost:8080 

## 📝 Ejemplos de Uso

### Crear una nueva tarea (POST)
```json
{
  "text": "Toca pajita",
  "date": "2025-01-30",
  "time": "18:00:00",
  "completed": false
}
```

### Configuración CORS
La aplicación está configurada para permitir CORS desde `http://localhost:3000` para integración con aplicaciones frontend como Next.js. 

## Notes

El proyecto sigue una arquitectura multicapa estándar de Spring Boot con una estructura simplificada sin capa de servicio separada. La lógica de negocio se implementa directamente en el controlador, lo que es apropiado para una aplicación de este tamaño. La aplicación utiliza Spring Data JPA para el acceso a datos y aprovecha la auto-configuración de Spring Boot para la configuración de componentes.
