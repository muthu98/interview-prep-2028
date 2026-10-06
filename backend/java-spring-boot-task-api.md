# Beginner Java / Spring Boot Task API

## Day 21 — Hands-on Work Completed

Built and tested a substantial beginner Task API with Java 21, Maven, Spring Web, Spring Data JPA, Validation, and H2. CRUD requests were tested in Postman, as reported by the learner.

This is beginner hands-on practice: Java fundamentals and independent fluency remain in progress. It does not establish advanced Java mastery. These notes document the completed exercise; the original application source and Postman collection were not supplied in this update.

## Package Structure and Request Flow

The exercise covered separate responsibilities for entity/model, repository, service, controller, DTO, and exception handling. A representative structure is:

```text
task/
  TaskApplication.java
  entity/Task.java
  entity/TaskStatus.java
  repository/TaskRepository.java
  service/TaskService.java
  controller/TaskController.java
  dto/TaskRequest.java
  exception/TaskNotFoundException.java
  exception/GlobalExceptionHandler.java
```

Request → controller → service → repository → H2; the response returns through those layers. This structure illustrates the responsibilities studied rather than claiming exact original package names.

## Entity and Enum

- `TaskStatus` is an enum: a bounded set of allowed task states.
- `Task` is annotated with `@Entity` to map it to persistence.
- `@Id` identifies the primary key; `@GeneratedValue` delegates identifier generation.
- `@Enumerated` controls enum persistence. `EnumType.STRING` stores names rather than ordinal positions, avoiding dependence on enum order.
- Constructors initialize instances; JPA requires a public or protected no-argument constructor.
- Getters and setters expose and update entity properties. Understanding these remains part of learning Java classes.

## Repository

```java
public interface TaskRepository extends JpaRepository<Task, Long> {
}
```

`Task` is the entity type and `Long` the identifier type. Spring Data provides operations such as `findAll`, `findById`, `save`, and `delete`; the learner does not implement those CRUD methods manually.

## Service and Dependency Injection

`TaskService` implements CRUD operations and receives `TaskRepository` through its constructor. Spring supplies the dependency when creating the service.

- Create: construct an entity from the request and save it.
- Read: list tasks or look up an ID.
- Update: load an existing task, apply request fields, and save it.
- Delete: locate the task and delete it.
- Missing task: throw `TaskNotFoundException` rather than silently treating absence as a successful lookup.

Constructor injection makes the required dependency explicit. This was practiced at a beginner level, not as advanced dependency-injection design.

## Controller and Request DTO

`TaskController` exposes GET, POST, PUT, and DELETE operations. It handles HTTP input/output and delegates CRUD work to the service.

`TaskRequest` is the request DTO, separate from the persistence entity. Validation constraints describe accepted request fields; `@Valid` on the controller request body triggers validation. Illustrative constraints include `@NotBlank` for a required title and `@NotNull` for a required status; exact original fields and constraints are not asserted here.

## Exceptions and Validation

- `TaskNotFoundException` represents a missing requested task.
- `GlobalExceptionHandler`, annotated with `@RestControllerAdvice`, centralizes controller exception responses.
- Validation checks input constraints; exception handling decides how failures become HTTP responses. They are related responsibilities, not interchangeable concepts.
- Revision targets: explain 404 for missing resources and 400 for invalid requests, and trace how the exception reaches the handler.

## Postman and Next Revision

The API was tested in Postman during the learning session. No exported requests or response evidence were supplied, so this documentation update does not claim to rerun those tests or verify individual edge cases.

- Rebuild the flow from DTO to controller, service, repository, and entity without copying.
- Explain Java classes, constructors, methods, enum types, and generics used in the exercise.
- Recheck create, list/read, update, delete, missing IDs, and invalid input during revision.

