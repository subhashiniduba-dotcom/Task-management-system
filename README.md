[README.md](https://github.com/user-attachments/files/26165896/README.md)
# Task Management System 📋

A modular, console-based **Task Management System** built in Java using core **Object-Oriented Programming principles** and **SOLID design** — demonstrating clean architecture, layered separation, and software engineering best practices.

---

## OOP Principles Demonstrated

| Principle | Where Applied |
|-----------|--------------|
| **Encapsulation** | Private fields + controlled getters/setters in `Task`, `User`, `Comment` |
| **Abstraction** | `TaskRepository` and `UserRepository` interfaces hide implementation details |
| **Inheritance** | Custom exception hierarchy (`TaskNotFoundException`, `ValidationException`) |
| **Polymorphism** | `InMemoryTaskRepository` implements `TaskRepository` — swappable with any DB |
| **Builder Pattern** | `Task.Builder` for clean, readable object construction |
| **SOLID — SRP** | Each class has one responsibility (Task=data, TaskService=logic, UI=display) |
| **SOLID — OCP** | Services depend on interfaces — extend without modifying existing code |
| **SOLID — DIP** | Services receive repositories via constructor injection |
| **Immutability** | `Comment` fields are all final; `Task.id` and `createdAt` never change |
| **Defensive Copying** | `User.getTaskIds()` returns `Collections.unmodifiableList()` |

---

## Features

- **Full CRUD** — Create, Read, Update, Delete tasks
- **Priority Levels** — LOW, MEDIUM, HIGH, CRITICAL
- **Status Tracking** — TODO → IN_PROGRESS → ON_HOLD → COMPLETED / CANCELLED
- **Progress Tracking** — 0–100% with automatic status transitions
- **Due Date Management** — Overdue detection and day-countdown display
- **Assignee Management** — Assign tasks to team members
- **Category & Tags** — Organise tasks by project or type
- **Comments** — Add notes to any task
- **Search** — Full-text search by title and description
- **Filter** — By status, priority, or assignee
- **Overdue Alerts** — Instantly list all overdue tasks
- **Statistics Dashboard** — Counts, averages, completion rates
- **User Management** — Create users with roles (Admin, Manager, Developer, etc.)
- **Unit Tests** — 15+ JUnit 5 tests with Arrange-Act-Assert pattern

---

## Architecture — Multi-Layer Design

```
+---------------------------------------------------+
|  Presentation Layer    com.tms.ui                  |
|  ConsoleUI             Interactive text interface  |
+---------------------------------------------------+
|  Service Layer         com.tms.service             |
|  TaskService           Business logic, validation  |
|  UserService           User business rules         |
+---------------------------------------------------+
|  Repository Layer      com.tms.repository          |
|  TaskRepository        Interface (contract)        |
|  InMemoryTaskRepository  ConcurrentHashMap impl    |
|  UserRepository          Interface (contract)      |
|  InMemoryUserRepository  ConcurrentHashMap impl    |
+---------------------------------------------------+
|  Model Layer           com.tms.model               |
|  Task  User  Comment   Core domain entities        |
+---------------------------------------------------+
|  Util / Exception      com.tms.util / exception    |
|  ValidationUtil        Input validation helpers    |
|  DateUtil              Date formatting utilities   |
|  Custom Exceptions     TaskNotFound, Validation    |
+---------------------------------------------------+
```

---

## Project Structure

```
TaskManagementSystem/
├── src/com/tms/
│   ├── Main.java                          <- Entry point + DI wiring
│   ├── model/
│   │   ├── Task.java                      <- Core entity (Builder pattern)
│   │   ├── User.java                      <- User entity
│   │   └── Comment.java                   <- Immutable comment entity
│   ├── repository/
│   │   ├── TaskRepository.java            <- Interface (data contract)
│   │   ├── InMemoryTaskRepository.java    <- ConcurrentHashMap implementation
│   │   ├── UserRepository.java            <- Interface
│   │   └── InMemoryUserRepository.java    <- Implementation
│   ├── service/
│   │   ├── TaskService.java               <- Business logic (CRUD + search)
│   │   ├── UserService.java               <- User business logic
│   │   └── TaskServiceTest.java           <- JUnit 5 unit tests (15+ tests)
│   ├── ui/
│   │   └── ConsoleUI.java                 <- Interactive console interface
│   ├── util/
│   │   ├── ValidationUtil.java            <- Input validation
│   │   └── DateUtil.java                  <- Date formatting helpers
│   └── exception/
│       ├── TaskNotFoundException.java
│       ├── UserNotFoundException.java
│       └── ValidationException.java
└── README.md
```

---

## How to Run

### Compile and Run (Terminal)

```bash
# Navigate to project root
cd TaskManagementSystem

# Compile all Java files
find src -name "*.java" | xargs javac -d out

# Run the application
java -cp out com.tms.Main
```

### Run in IntelliJ IDEA

1. Open IntelliJ IDEA -> File -> Open -> select TaskManagementSystem/
2. Right-click src/com/tms/Main.java -> Run 'Main'

### Run Tests

```bash
# With IntelliJ: right-click TaskServiceTest.java -> Run Tests
# With Maven (add pom.xml): mvn test
```

---

## Demo — Sample Console Session

```
================================================================
  Task Management System — Main Menu
================================================================
  1. Create Task          5. Search Tasks
  2. View All Tasks       6. Filter Tasks
  3. Update Task          7. Overdue Tasks
  4. Delete Task          8. Statistics
  9. User Management      0. Exit

  Enter choice: 8

================================================================
  TASK STATISTICS
================================================================
  Total Tasks          : 5
  TODO                 : 1
  In Progress          : 2
  Completed            : 1
  Overdue              : 1
  Critical Priority    : 1
  Avg Completion       : 52.0%
================================================================
```

---

## Design Patterns Used

| Pattern | Class | Purpose |
|---------|-------|---------|
| **Builder** | `Task.Builder` | Readable multi-field object construction |
| **Repository** | `TaskRepository` | Decouple data access from business logic |
| **Dependency Injection** | `TaskService(TaskRepository)` | Testability and flexibility |
| **Utility Class** | `ValidationUtil`, `DateUtil` | Reusable static helpers |

---

## SDLC Practices Applied

| Phase | Practice |
|-------|---------|
| **Planning** | Clear requirements — CRUD, OOP, SOLID |
| **Design** | Multi-layer architecture, interface-based contracts |
| **Implementation** | Modular packages, single-responsibility classes |
| **Testing** | Unit tests (JUnit 5), Arrange-Act-Assert pattern |
| **Maintenance** | Interfaces allow swapping implementations without changes |

---

## Extending the Project

- **Database Layer** — Implement `DatabaseTaskRepository` using JDBC or Hibernate
- **REST API** — Add a Spring Boot controller layer over the existing services
- **GUI** — Build a JavaFX frontend using the same service classes
- **Authentication** — Add login with role-based access control
- **Export** — Export tasks to CSV or PDF reports

---

## Tech Stack

| Technology | Version | Purpose |
|-----------|---------|---------|
| Java | 11+ | Core language |
| JUnit 5 | 5.9+ | Unit testing |
| Java Collections | Built-in | In-memory storage |
| Java Time API | Built-in | Date/time handling |
| ConcurrentHashMap | Built-in | Thread-safe storage |

---

## License

MIT — free to use, modify, and build upon.

---

*Clean code. Solid design. One task at a time.*
