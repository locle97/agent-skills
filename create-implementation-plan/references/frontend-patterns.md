# Frontend Architecture Patterns Reference

## Table of Contents
1. [Component Architecture](#component-architecture)
2. [State Management](#state-management)
3. [API Integration](#api-integration)
4. [Component Communication](#component-communication)
5. [Testing Strategy](#testing-strategy)
6. [Performance Patterns](#performance-patterns)

---

## Component Architecture

### Component Categories
| Type | Responsibility | State | Examples |
|------|---------------|-------|----------|
| **Page/Container** | Route handling, data fetching | Connected to store | `UserListPage`, `DashboardContainer` |
| **Feature** | Business logic, composition | Local + props | `UserCard`, `CheckoutForm` |
| **UI/Presentational** | Pure rendering | Props only | `Button`, `Modal`, `Input` |
| **Layout** | Structure, positioning | Minimal | `Sidebar`, `Grid`, `Header` |

### Investigation Checklist
```
[ ] Existing component folder structure
[ ] Naming conventions (PascalCase, kebab-case)
[ ] Shared component library location
[ ] Props typing approach (TypeScript, PropTypes)
[ ] Styling solution (CSS Modules, styled-components, Tailwind)
[ ] Component documentation (Storybook)
```

### Recommended Structure
```
src/
├── components/
│   ├── ui/              # Reusable UI primitives
│   ├── features/        # Feature-specific components
│   └── layouts/         # Layout components
├── pages/               # Route components
├── hooks/               # Custom hooks
├── stores/              # State management
├── services/            # API clients
├── utils/               # Helper functions
└── types/               # TypeScript definitions
```

---

## State Management

### State Categories
| Category | Location | Examples |
|----------|----------|----------|
| **Server state** | React Query/SWR/Apollo | API responses, cached data |
| **Global UI state** | Redux/Zustand/Context | Theme, sidebar open, modals |
| **Local UI state** | useState/useReducer | Form inputs, toggles |
| **URL state** | Router | Filters, pagination, tabs |
| **Form state** | React Hook Form/Formik | Validation, dirty state |

### Investigation Checklist
```
[ ] Current state management library
[ ] Store organization (by feature vs flat)
[ ] Server state caching strategy
[ ] Persistence requirements (localStorage)
[ ] DevTools usage
[ ] State normalization approach
```

### Store Organization
```
stores/
├── slices/
│   ├── auth.ts          # Authentication state
│   ├── ui.ts            # UI preferences
│   └── [feature].ts     # Feature-specific
├── hooks.ts             # Typed useSelector/useDispatch
└── index.ts             # Store configuration
```

---

## API Integration

### Data Fetching Patterns
```typescript
// React Query pattern
const useUsers = (filters: UserFilters) => {
  return useQuery({
    queryKey: ['users', filters],
    queryFn: () => userService.list(filters),
    staleTime: 5 * 60 * 1000,
  });
};

// Apollo Client pattern
const GET_USERS = gql`
  query GetUsers($filter: UserFilter) {
    users(filter: $filter) {
      id
      name
      email
    }
  }
`;
```

### Investigation Checklist
```
[ ] Data fetching library (fetch, axios, React Query, SWR, Apollo)
[ ] API client organization
[ ] Error handling strategy
[ ] Loading state patterns
[ ] Caching configuration
[ ] Optimistic updates usage
[ ] Request/response interceptors
```

### API Service Structure
```
services/
├── api/
│   ├── client.ts        # Axios/fetch instance
│   ├── interceptors.ts  # Auth, error handling
│   └── endpoints.ts     # URL constants
├── users/
│   ├── api.ts           # User API calls
│   ├── types.ts         # Request/response types
│   └── hooks.ts         # React Query hooks
└── index.ts
```

---

## Component Communication

### Communication Patterns
| Pattern | Direction | Use Case |
|---------|-----------|----------|
| **Props** | Parent → Child | Direct data/callbacks |
| **Context** | Ancestor → Descendants | Theme, auth, config |
| **Store** | Any → Any | Shared application state |
| **Events** | Child → Parent | User interactions |
| **Refs** | Parent → Child | Imperative control |
| **URL** | Any → Any | Shareable state |

### Investigation Checklist
```
[ ] Prop drilling depth (refactor threshold: 3+ levels)
[ ] Context usage and providers
[ ] Event bubbling patterns
[ ] Custom event system
[ ] Ref forwarding usage
```

### Anti-patterns to Note
- Excessive prop drilling (>3 levels)
- Overusing global state for local concerns
- Direct DOM manipulation without refs
- Circular dependencies between components

---

## Testing Strategy

### Test Pyramid
```
        /\
       /  \  E2E (Cypress, Playwright)
      /----\
     /      \  Integration (Testing Library)
    /--------\
   /          \  Unit (Jest, Vitest)
  /______________\
```

### Investigation Checklist
```
[ ] Testing framework (Jest, Vitest)
[ ] Component testing approach (Testing Library)
[ ] E2E framework (Cypress, Playwright)
[ ] Mock strategy (MSW, manual mocks)
[ ] Coverage thresholds
[ ] CI integration
```

### Test Organization
```
__tests__/
├── unit/
│   ├── utils/
│   └── hooks/
├── components/
│   └── [ComponentName].test.tsx
└── e2e/
    └── flows/
```

---

## Performance Patterns

### Optimization Techniques
| Technique | Tool | Use Case |
|-----------|------|----------|
| Memoization | `React.memo`, `useMemo` | Expensive renders |
| Code splitting | `lazy`, dynamic imports | Large bundles |
| Virtualization | `react-virtual` | Long lists |
| Image optimization | Next/Image, lazy loading | Media-heavy pages |
| Debouncing | `useDebouncedValue` | Search inputs |

### Investigation Checklist
```
[ ] Bundle analysis results
[ ] Core Web Vitals metrics
[ ] Render performance issues
[ ] Memory leak indicators
[ ] Network waterfall patterns
[ ] Lazy loading implementation
```
