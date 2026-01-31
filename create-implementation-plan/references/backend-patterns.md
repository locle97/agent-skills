# Backend Architecture Patterns Reference

## Table of Contents
1. [CQRS Pattern](#cqrs-pattern)
2. [DDD Tactical Patterns](#ddd-tactical-patterns)
3. [API Design](#api-design)
4. [GraphQL Patterns](#graphql-patterns)
5. [Microservice Boundaries](#microservice-boundaries)
6. [Unit Testing Strategy](#unit-testing-strategy)

---

## CQRS Pattern

### When to Apply
- Read/write ratio heavily skewed (10:1 or more)
- Complex domain logic on writes, simple reads
- Need for different scaling strategies
- Event sourcing requirements

### Investigation Checklist
```
[ ] Identify existing command handlers (Create*, Update*, Delete*)
[ ] Identify query handlers (Get*, List*, Search*)
[ ] Check for existing event bus/message queue
[ ] Review current data access patterns
[ ] Note any read models or projections
```

### Implementation Structure
```
src/
├── application/
│   ├── commands/
│   │   ├── handlers/
│   │   └── validators/
│   └── queries/
│       ├── handlers/
│       └── read-models/
├── domain/
│   ├── aggregates/
│   ├── events/
│   └── value-objects/
└── infrastructure/
    ├── persistence/
    └── messaging/
```

---

## DDD Tactical Patterns

### Aggregate Design Rules
1. Protect business invariants within aggregate boundaries
2. Design small aggregates (prefer single entity when possible)
3. Reference other aggregates by ID only
4. Use eventual consistency between aggregates

### Investigation Checklist
```
[ ] Map existing entities and their relationships
[ ] Identify transaction boundaries
[ ] Find business rules that span entities
[ ] Note existing validation logic locations
[ ] Check for domain events
```

### Bounded Context Indicators
Look for:
- Different terminology for same concept
- Different validation rules by context
- Teams with distinct responsibilities
- Separate deployment needs

---

## API Design

### REST Endpoint Patterns
```
GET    /resources          → List (with pagination)
GET    /resources/:id      → Get single
POST   /resources          → Create
PUT    /resources/:id      → Full update
PATCH  /resources/:id      → Partial update
DELETE /resources/:id      → Delete
POST   /resources/:id/actions/:action → Custom action
```

### Investigation Checklist
```
[ ] Current API versioning strategy
[ ] Authentication/authorization patterns
[ ] Error response format
[ ] Pagination implementation
[ ] Rate limiting approach
[ ] API documentation (OpenAPI/Swagger)
```

---

## GraphQL Patterns

### Schema Design
```graphql
# Query naming: noun-based
type Query {
  user(id: ID!): User
  users(filter: UserFilter, pagination: Pagination): UserConnection
}

# Mutation naming: verb + noun
type Mutation {
  createUser(input: CreateUserInput!): CreateUserPayload!
  updateUser(id: ID!, input: UpdateUserInput!): UpdateUserPayload!
}
```

### Investigation Checklist
```
[ ] Existing schema structure
[ ] Resolver organization (by type vs by feature)
[ ] DataLoader usage for N+1 prevention
[ ] Subscription requirements
[ ] Custom scalar types
[ ] Federation/stitching needs
```

---

## Microservice Boundaries

### Decomposition Strategies
1. **By business capability** - Align with business functions
2. **By subdomain** - Follow DDD bounded contexts
3. **By data ownership** - Single source of truth per service

### Investigation Checklist
```
[ ] Current service boundaries
[ ] Inter-service communication (sync vs async)
[ ] Shared databases (anti-pattern indicator)
[ ] Service discovery mechanism
[ ] Circuit breaker patterns
[ ] Distributed tracing
```

### Communication Patterns
| Pattern | Use When |
|---------|----------|
| REST/HTTP | Simple request/response, external APIs |
| gRPC | Internal services, high performance |
| Message Queue | Async processing, event-driven |
| Event Bus | Domain events, eventual consistency |

---

## Unit Testing Strategy

### Test Organization
```
tests/
├── unit/
│   ├── domain/          # Pure domain logic
│   ├── application/     # Use case handlers
│   └── infrastructure/  # Adapters with mocks
├── integration/
│   ├── api/             # HTTP endpoints
│   └── persistence/     # Database operations
└── e2e/
    └── workflows/       # Full user journeys
```

### Coverage Guidelines
| Layer | Target | Focus |
|-------|--------|-------|
| Domain | 90%+ | Business rules, invariants |
| Application | 80%+ | Use case orchestration |
| Infrastructure | 70%+ | Adapter contracts |
| API | Key paths | Request/response contracts |

### Investigation Checklist
```
[ ] Current testing framework
[ ] Test organization pattern
[ ] Mocking/stubbing approach
[ ] Test data management
[ ] CI pipeline integration
[ ] Coverage thresholds
