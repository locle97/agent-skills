# Backend Architecture Patterns

## Detection Patterns

### REST API
- Look for: `routes/`, `controllers/`, `@Get`, `@Post`, `@Put`, `@Delete`, `express.Router()`, `app.get()`, `FastAPI`, `@app.route`
- Common files: `routes.ts`, `api.ts`, `controller.ts`, `endpoints.py`

### GraphQL
- Look for: `schema.graphql`, `resolvers/`, `typeDefs`, `@Query`, `@Mutation`, `@Resolver`, `graphql-yoga`, `apollo-server`
- Common files: `schema.graphql`, `resolvers.ts`, `typedefs.ts`

### DDD (Domain-Driven Design)
- Look for: `domain/`, `aggregates/`, `entities/`, `value-objects/`, `repositories/`, `services/`
- Patterns: Aggregate roots, domain events, bounded contexts
- Common files: `*Aggregate.ts`, `*Entity.ts`, `*Repository.ts`, `*Service.ts`

### CQRS (Command Query Responsibility Segregation)
- Look for: `commands/`, `queries/`, `handlers/`, `@CommandHandler`, `@QueryHandler`, `CommandBus`, `QueryBus`
- Patterns: Separate read/write models, event sourcing
- Common files: `*Command.ts`, `*Query.ts`, `*Handler.ts`, `*Projection.ts`

## Analysis Checklist

1. **Entry Points**: Find route definitions, GraphQL resolvers, or command handlers
2. **Business Logic**: Locate services, domain entities, use cases
3. **Data Layer**: Identify repositories, ORMs, database models
4. **Middleware**: Auth, validation, logging, error handling
5. **Events/Messages**: Event emitters, message queues, pub/sub
