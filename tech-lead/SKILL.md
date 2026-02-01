---
name: tech-lead
description: |
  Provide high-level implementation guidance for full-stack features. Analyzes backend (REST API, GraphQL, DDD, CQRS) and frontend (React, Vue, Next.js, Nuxt) codebases to create architecture overviews with Mermaid diagrams.

  Use when: (1) Given a feature request, user story, or requirement to analyze, (2) Need to understand how a feature flows through frontend and backend, (3) Want architecture overview before implementation, (4) Need to identify affected components across separate frontend/backend repos, (5) User asks "how would we implement X" or "what's involved in building Y".
---

# Tech Lead Guidance

Analyze full-stack projects and provide architecture overview for implementing features.

## Workflow

### 1. Gather Context

Ask user for:
- **Requirement**: Feature description, user story, or ticket
- **Frontend repo path**: Path to React/Vue/Next.js/Nuxt codebase
- **Backend repo path**: Path to API codebase

If paths not provided, scan current directory for `package.json`, `go.mod`, `requirements.txt`, etc.

### 2. Detect Architecture

**Backend** - Identify pattern by searching for:
| Pattern | Search for |
|---------|-----------|
| REST | `routes/`, `controllers/`, `@Get/@Post`, `express.Router` |
| GraphQL | `schema.graphql`, `resolvers/`, `@Query/@Mutation` |
| DDD | `domain/`, `aggregates/`, `entities/`, `repositories/` |
| CQRS | `commands/`, `queries/`, `handlers/`, `CommandBus` |

**Frontend** - Identify framework:
| Framework | Search for |
|-----------|-----------|
| React | `package.json` → `react`, `.tsx/.jsx` files |
| Vue | `package.json` → `vue`, `.vue` files |
| Next.js | `next.config`, `app/` or `pages/` directory |
| Nuxt | `nuxt.config`, `pages/` with `.vue` files |

See `references/backend-patterns.md` and `references/frontend-patterns.md` for detection details.

### 3. Gap Analysis (Critical Step)

For the given requirement, perform a thorough gap analysis:

#### 3.1 Identify What EXISTS
Search the codebase for related components:
- **Backend**: Existing endpoints, services, entities, repositories
- **Frontend**: Existing pages, components, hooks, stores

#### 3.2 Identify What's MISSING on Backend
Check for gaps - the backend often needs NEW:
- **Endpoints/Resolvers**: Does the API endpoint exist? Search routes/controllers
- **DTOs/Types**: Are request/response types defined?
- **Services**: Is business logic layer present?
- **Entities/Aggregates**: Do domain models exist?
- **Repositories**: Is data access layer ready?
- **Commands/Queries** (CQRS): Are handlers defined?
- **Validation**: Are validators in place?

#### 3.3 Identify What's MISSING on Frontend
Check for gaps:
- **Pages/Views**: Does the route component exist?
- **UI Components**: Are required components available?
- **API Integration**: Do API hooks/services exist?
- **State Management**: Is store/slice needed?
- **Forms**: Are form handlers ready?

#### 3.4 Integration Requirements
Define what connects frontend to backend:
- **API Contract**: Endpoint URL, method, request/response shape
- **Authentication**: Token handling, permissions
- **Error Handling**: Error codes and UI responses
- **Real-time**: WebSocket/SSE requirements if any

### 4. Trace Feature Flow

For the given requirement:

1. **Find entry points**
   - Frontend: Route/page handling the feature URL
   - Backend: API endpoint, resolver, or command handler

2. **Map data flow**
   - Frontend → API call → Backend handler → Database
   - Identify DTOs, request/response shapes

3. **Identify affected components**
   - Frontend: Pages, components, hooks/composables, stores
   - Backend: Controllers, services, repositories, entities

### 4. Generate Architecture Overview

Write the output to a markdown file in the current working directory:
- Filename: `architecture-[feature-name-kebab-case].md`
- Example: `architecture-user-authentication.md`

Output format:

```markdown
## Feature: [Name]

### Problem/Feature Summary
[2-3 sentences describing what the feature does and why it's needed. Focus on the user value and business context.]

### Overview
[1-2 sentence summary of implementation approach]

### Architecture Diagram

​```mermaid
sequenceDiagram
    participant U as User
    participant FE as Frontend
    participant API as Backend API
    participant DB as Database

    U->>FE: [User action]
    FE->>API: [API call]
    API->>DB: [Database operation]
    DB-->>API: [Response]
    API-->>FE: [Response]
    FE-->>U: [UI update]
​```

### Frontend Components
| Component | Path | Purpose |
|-----------|------|---------|
| [Page] | `src/pages/...` | Entry point |
| [Component] | `src/components/...` | UI element |

### Backend Components
| Component | Path | Purpose |
|-----------|------|---------|
| [Handler] | `src/handlers/...` | Request handler |
| [Service] | `src/services/...` | Business logic |

### Data Flow
1. User triggers [action] in [component]
2. Frontend calls [endpoint/resolver]
3. Backend processes via [handler/service]
4. Database [operation] on [entity]

### Key Considerations
- [Architecture decisions]
- [Potential challenges]
- [Dependencies between components]
```

### 5. Route-Based Component Discovery

When requirement mentions a route (e.g., `/users/profile`):

**React/Next.js**:
```bash
# App router
find app -path "*users*profile*" -name "page.tsx"
# Pages router
find pages -path "*users*profile*"
# React Router - search route definitions
grep -r "path.*users.*profile" --include="*.tsx"
```

**Vue/Nuxt**:
```bash
# File-based routing
find pages -path "*users*profile*" -name "*.vue"
# Vue Router
grep -r "path.*users.*profile" --include="*.ts"
```

**Backend**:
```bash
# REST endpoints
grep -r "users/profile\|/users/:id/profile" --include="*.ts" --include="*.py"
# GraphQL
grep -r "userProfile\|user.*profile" --include="*.graphql"
```

## Output Guidelines

- **Write output to markdown file** - Always save the architecture overview to `architecture-[feature-name].md`
- Keep guidance **high-level** - team members investigate details
- Focus on **what** components are involved, not **how** to code them
- Use Mermaid diagrams to visualize flow
- List files/paths so team can navigate directly
- Highlight integration points between frontend and backend
- Note architectural patterns being used (DDD, CQRS, etc.)
