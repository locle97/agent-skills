---
name: create-implementation-plan
description: Senior full-stack team lead that creates detailed, multi-phase implementation plans. Use when receiving a feature request or requirement that needs to be broken down for frontend and backend developers. Performs thorough codebase investigation across separate repos, analyzes existing patterns (CQRS, DDD, GraphQL, component architecture, state management), and produces a structured markdown plan with phases, tasks, acceptance criteria, and owner assignments. Triggers on requests like "plan the implementation of...", "create a plan for...", "break down this feature...", "how should we implement...", or when receiving requirements that need technical planning before development.
---

# Implementation Plan Creator

Act as a senior full-stack technical lead. Investigate codebases thoroughly, then produce structured implementation plans that frontend and backend developers can execute independently.

## Workflow

### Phase 1: Gather Requirements

Clarify the requirement with the user:
- What is the feature/change needed?
- Which repositories are involved? (get paths)
- Any constraints, deadlines, or dependencies?
- Who are the team members? (for task assignment)

### Phase 2: Backend Investigation

Explore the backend codebase systematically:

```
1. Project Structure
   - Identify architecture pattern (monolith, microservices, modular monolith)
   - Map folder organization and module boundaries
   - Note dependency injection/IoC patterns

2. Domain Analysis
   - Find relevant aggregates, entities, value objects
   - Identify existing domain events
   - Map repository interfaces and implementations

3. API Layer
   - Catalog existing endpoints (REST/GraphQL)
   - Note authentication/authorization patterns
   - Review request/response DTOs
   - Check validation approaches

4. Data Layer
   - Review database schema and migrations
   - Identify read models vs write models (CQRS)
   - Note caching strategies

5. Testing Patterns
   - Identify test organization
   - Note mocking strategies
   - Review coverage requirements
```

For pattern details, see: [references/backend-patterns.md](references/backend-patterns.md)

### Phase 3: Frontend Investigation

Explore the frontend codebase systematically:

```
1. Project Structure
   - Map component organization
   - Identify shared vs feature components
   - Note routing structure

2. State Management
   - Identify state solution (Redux, Zustand, Context, etc.)
   - Map store organization
   - Note server state handling (React Query, SWR, Apollo)

3. API Integration
   - Review API client setup
   - Identify data fetching patterns
   - Note error handling approaches

4. Component Patterns
   - Identify component categories (page, feature, UI)
   - Note styling solution
   - Review props patterns and typing

5. Testing Patterns
   - Identify testing frameworks
   - Note component testing approach
   - Review E2E coverage
```

For pattern details, see: [references/frontend-patterns.md](references/frontend-patterns.md)

### Phase 4: Design Decisions

Before writing the plan, determine:

**Backend Decisions:**
- Which service/domain owns this feature?
- New aggregate or extend existing?
- CQRS needed? (separate read/write models)
- API style? (REST endpoint, GraphQL mutation, or both)
- Event-driven aspects?

**Frontend Decisions:**
- Which components need creation vs modification?
- State management approach for this feature?
- API integration pattern?
- Component communication strategy?

**Cross-cutting:**
- Integration points between frontend and backend
- Shared types/contracts
- Feature flag requirements
- Migration/rollout strategy

### Phase 5: Write Implementation Plan

Create a markdown file using the template structure. Save to a logical location (e.g., `docs/plans/[feature-name]-implementation-plan.md`).

Template: [references/plan-template.md](references/plan-template.md)

**Plan Requirements:**
1. Break into 2-5 phases based on complexity
2. Each phase has clear goal and prerequisites
3. Tasks marked for Backend or Frontend owner
4. Acceptance criteria for every task
5. Integration points explicitly documented
6. Testing strategy per phase

## Investigation Commands

Quick reference for codebase exploration:

```bash
# Find architecture patterns
Glob: "**/src/**/{commands,queries,handlers}/**"
Glob: "**/src/**/{aggregates,entities,domain}/**"
Glob: "**/src/**/{components,features,pages}/**"

# Find API definitions
Grep: "router\.|@Controller|@Query|@Mutation"
Grep: "createApi|useQuery|useMutation"

# Find state management
Grep: "createSlice|createStore|create\(|defineStore"
Grep: "useContext|createContext|Provider"

# Find test patterns
Glob: "**/*.{test,spec}.{ts,tsx,js,jsx}"
Grep: "describe\(|it\(|test\("
```

## Output Checklist

Before delivering the plan, verify:

- [ ] All relevant existing code has been reviewed
- [ ] Architecture decisions are justified
- [ ] Phases have logical dependencies
- [ ] Backend tasks are complete and self-contained
- [ ] Frontend tasks are complete and self-contained
- [ ] Integration points are explicit
- [ ] Testing requirements are specified
- [ ] Risks and open questions documented
- [ ] File paths reference actual codebase locations
