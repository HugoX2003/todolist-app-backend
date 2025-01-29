# TodoList Backend API

API REST para gestión de tareas desarrollada con Spring Boot y MySQL.

![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.4.2-green)
![MySQL](https://img.shields.io/badge/MySQL-8.0-blue)

## Tecnologías principales
- 🍃 Spring Boot
- 📦 Spring Data JPA
- 🗃️ MySQL
- 🛠️ Maven
- 🔄 Hibernate


## Estructura del proyecto
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

## Ejecutar la aplicación
- mvn spring-boot:run


## La API estará disponible en:
- http://localhost:8080


# Endpoints de la API

| Método | Endpoint       | Descripción                    |
|--------|----------------|--------------------------------|
| GET    | /api/todos     | Obtener todas las tareas       |
| POST   | /api/todos     | Crear nueva tarea              |
| PUT    | /api/todos/{id}| Actualizar estado completado   |
| DELETE | /api/todos/{id}| Eliminar tarea                 |


# Ejemplo de cuerpo para POST:
```
{
  "text": "Toca pajita",
  "date": "2025-01-30",
  "time": "18:00:00",
  "completed": false
}
```
