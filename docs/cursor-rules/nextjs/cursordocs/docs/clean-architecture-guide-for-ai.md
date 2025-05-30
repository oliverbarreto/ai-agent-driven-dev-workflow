# Clean Architecture Guide for AI-Assisted Development

## Table of Contents

1. Introduction
2. Architecture Overview
3. Guidelines for AI Tools
4. Developer's Guide to AI Interaction
5. Quality Assurance Checklist
6. Common Patterns and Best Practices

## 1. Introduction

This guide provides a framework for AI tools and developers to collaborate effectively while maintaining clean architecture principles in modern web applications. It focuses on creating maintainable, scalable, and testable code through clear separation of concerns and well-defined boundaries.

## 2. Architecture Overview

### Core Layers

#### Domain Layer (Core Business Rules)

- Pure business entities
- Value objects
- Domain interfaces
- Business rules and validation

#### Application Layer (Use Cases)

- Use case implementations
- Application services
- DTOs and mappers
- Orchestration of domain objects

#### Infrastructure Layer (External Concerns)

- Database implementations
- External service integrations
- Framework-specific code
- Technical concerns

#### Presentation Layer (UI/Interface)

- User interface components
- API endpoints/Server Actions
- Route handlers
- View models

### Key Principles

- Dependency Rule: Dependencies only point inward
- Isolation: Business rules isolated from external concerns
- Abstraction: Interfaces define boundaries between layers
- Single Responsibility: Each component has one reason to change

## 3. Guidelines for AI Tools

#### Entity Creation

```typescript
typescriptCopy // When creating entities, follow this template:
export interface EntityName {
  id: string
  // Required core properties
  requiredProp: PropType
  // Optional properties
  optionalProp?: PropType
  // Timestamps
  createdAt: Date
  updatedAt: Date
}

// Include validation rules
export const entityValidation = z.object({
  // Define validation rules
})
```

### Use Case Implementation

```typescript
// Use Case template
export class UseActionNameUseCase {
  constructor(
    private primaryRepository: IPrimaryRepository,
    private secondaryRepository?: ISecondaryRepository
  ) {}

  async execute(input: InputType): Promise<OutputType> {
    // 1. Validate input
    // 2. Apply business rules
    // 3. Persist changes
    // 4. Return result
  }
}
```

#### Repository Interface

```typescript
// Repository interface template
export interface IEntityRepository {
  create(entity: CreateEntityInput): Promise<Entity>
  findById(id: string): Promise<Entity | null>
  findMany(criteria: FindCriteria): Promise<Entity[]>
  update(id: string, data: UpdateEntityInput): Promise<Entity>
  delete(id: string): Promise<void>
  // Additional specific methods
}
```

## 4. Developer's Guide to AI Interaction

### Prompting Best Practices

#### 1. Initial Setup

```plaintext
"I need to create a new feature for [description]. Please help me:
1. Define the domain entities
2. Create the repository interface
3. Implement the use cases
4. Set up the infrastructure layer
5. Create the presentation layer"
```

#### 2. Adding New Features

```plaintext
"I want to add [feature] to the existing [domain].
Current entities: [list existing entities]
Required functionality: [list requirements]"
```

#### 3. Modifying Existing Code

```plaintext
"I need to modify [component] to support [new requirement].
Current implementation: [paste relevant code]
New requirements: [list changes needed]"
```

### Quality Checkpoints

When reviewing AI-generated code, verify:

#### 1. Domain Layer

- Entities contain only business properties
- No framework dependencies
- Clear validation rules
- Pure business logic

#### 2. Use Cases

- Single responsibility
- Clear input/output types
- Proper error handling
- Business rule enforcement

#### 3. Infrastructure

- Clean repository implementations
- Proper error handling
- Performance considerations
- Security measures

#### 4. Presentation

- Clear separation of concerns
- Proper state management
- Error boundary implementation
- Loading states handled

## 5. Quality Assurance Checklist

### Before Implementation

- Domain entities defined
- Use cases identified
- Repository interfaces designed
- Input/Output types specified
- Validation rules established

### During Implementation

- Dependencies point inward
- No business logic in infrastructure
- Proper error handling
- Type safety maintained
- Tests implemented

### After Implementation

- Code review checklist completed
- Tests passing
- Documentation updated
- Performance verified
- Security reviewed

## 6. Common Patterns and Best Practices

### Error Handling

```typescript
// Domain Errors
export class DomainError extends Error {
  constructor(message: string) {
    super(message)
    this.name = "DomainError"
  }
}

// Use Case Error Handling
try {
  // Execute business logic
} catch (error) {
  if (error instanceof DomainError) {
    // Handle domain errors
  }
  throw error
}
```

### Dependency Injection

```typescript
// Constructor Injection
export class UseCase {
  constructor(
    private readonly repository: IRepository,
    private readonly service: IService
  ) {}
}

// Factory Pattern
export const createUseCase = (repository: IRepository, service: IService) => {
  return new UseCase(repository, service)
}
```

### Type Safety

```typescript
// Input/Output Types
export interface UseCaseInput {
  // Input properties
}

export interface UseCaseOutput {
  // Output properties
}

// Use Case Type Safety
export class UseCase {
  async execute(input: UseCaseInput): Promise<UseCaseOutput> {
    // Implementation
  }
}
```
