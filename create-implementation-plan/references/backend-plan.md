# Backend Implementation Planning Guide

## DDD Structure Analysis

### Domain Layer Investigation

Before planning, investigate existing domain structure:

```bash
# Find domain entities and aggregates
find src -type d -name "domain" -o -name "entities" -o -name "aggregates"
grep -r "class.*Aggregate\|class.*Entity" --include="*.ts" --include="*.py"

# Find value objects
grep -r "class.*ValueObject\|readonly\|immutable" --include="*.ts"

# Find domain events
grep -r "DomainEvent\|extends.*Event\|@Event" --include="*.ts"
```

### DDD Component Patterns

#### Aggregate Root
```
- Owns entity lifecycle
- Enforces invariants
- Publishes domain events
- Single entry point for modifications
```

**Phase task example**:
| Task | Path | Notes |
|------|------|-------|
| Create OrderAggregate | `src/domain/aggregates/Order.ts` | Contains OrderItems, enforces max 10 items invariant |

#### Entity
```
- Has identity (ID)
- Mutable state
- Belongs to an aggregate
```

#### Value Object
```
- No identity
- Immutable
- Self-validating
- Equality by value
```

**Reusability checklist**:
- [ ] Check if similar VO exists (Money, Email, PhoneNumber)
- [ ] Can this VO be generalized for other contexts?
- [ ] Should this be a shared kernel component?

#### Domain Events
```
- Past tense naming (OrderCreated, PaymentProcessed)
- Immutable payload
- Contains aggregate ID and relevant data
```

## CQRS Pattern Implementation

### Command Investigation

```bash
# Find existing commands
find src -type d -name "commands"
grep -r "class.*Command\|@Command\|CommandHandler" --include="*.ts"
```

### Command Structure

```
Command:
  - Name: [Verb][Noun]Command (CreateOrderCommand)
  - Properties: Only data needed for the operation
  - Validation: Input validation in command itself

Handler:
  - Load aggregate from repository
  - Call aggregate method
  - Save aggregate
  - Publish events
```

**Phase breakdown**:

| Phase | Tasks |
|-------|-------|
| Command definition | Create command class with properties |
| Handler skeleton | Create handler with dependency injection |
| Aggregate interaction | Implement aggregate method calls |
| Event publishing | Add domain event emission |
| Unit tests | Test handler in isolation |

### Query Structure

```
Query:
  - Name: Get[Noun]Query, List[Noun]Query
  - Properties: Filter/pagination parameters

Handler:
  - Read from read model (can be different DB)
  - Return DTO, not domain entities
  - No side effects
```

### Event Handling

```bash
# Find event handlers
grep -r "EventHandler\|@OnEvent\|subscribe" --include="*.ts"
```

**Event handler phases**:
1. Create event class
2. Create handler (sync or async)
3. Register handler with event bus
4. Add integration tests

## Repository Pattern

### Investigation

```bash
# Find repository patterns
grep -r "Repository\|implements.*Repository" --include="*.ts"
grep -r "findById\|save\|delete" --include="*.ts" src/infrastructure
```

### Repository Tasks

| Task | Description |
|------|-------------|
| Define interface | In domain layer |
| Implement adapter | In infrastructure layer |
| Add unit of work | If using transactions |
| Create test doubles | For testing |

## Phase Structure Template

### Phase 1: Domain Layer (Foundation)
Focus: Core business logic, no external dependencies

Tasks:
1. Value Objects (2-3 per phase max)
2. Entities (1-2 per phase)
3. Aggregate Root (1 per phase)
4. Domain Events (as needed)

### Phase 2: Application Layer (Use Cases)
Focus: Orchestration, commands/queries

Tasks:
1. Command/Query DTOs
2. Handler implementations
3. Application services (if needed)
4. Event handlers

### Phase 3: Infrastructure Layer (Adapters)
Focus: External concerns

Tasks:
1. Repository implementations
2. Database migrations
3. External service adapters
4. Message queue setup

### Phase 4: API Layer (Interface)
Focus: HTTP/GraphQL interface

Tasks:
1. Controller/Resolver
2. Request/Response DTOs
3. Validation middleware
4. Error mapping

## Reusability Analysis

### Questions to ask:

1. **Does similar logic exist?**
   - Search for similar entity names
   - Check shared/common modules

2. **Can this be generalized?**
   - Will other features need this?
   - Should it be a shared kernel component?

3. **What abstractions are needed?**
   - Base classes (AggregateRoot, Entity, ValueObject)
   - Interfaces (Repository, EventPublisher)

### Reusability markers in plan:

```markdown
| Task | Path | Reusable |
|------|------|----------|
| Create Money VO | `src/shared/value-objects/Money.ts` | YES - shared kernel |
| Create OrderId | `src/domain/order/OrderId.ts` | NO - context specific |
```
