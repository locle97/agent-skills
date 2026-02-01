# Frontend Implementation Planning Guide

## Component Architecture Investigation

### Project Structure Analysis

```bash
# Identify framework and patterns
cat package.json | grep -E "react|vue|next|nuxt"

# Find component organization
ls -la src/components/
find src -type d -name "components" -o -name "features" -o -name "ui"

# Find state management
grep -r "createStore\|createSlice\|defineStore\|create(" --include="*.ts" src/
```

## Component Hierarchy

### Atomic Design Levels

```
1. Atoms (UI primitives)
   └── Button, Input, Icon, Badge

2. Molecules (Simple combinations)
   └── SearchInput, FormField, Card

3. Organisms (Complex features)
   └── UserCard, ProductList, NavigationBar

4. Templates (Page layouts)
   └── DashboardLayout, AuthLayout

5. Pages (Route components)
   └── HomePage, UserProfilePage
```

### Component Responsibility Matrix

| Level | State | API Calls | Business Logic |
|-------|-------|-----------|----------------|
| UI (Atoms) | No | No | No |
| Feature | Local only | Through props/hooks | Minimal |
| Container | Connects to store | Through services | Orchestration |
| Page | Route params | Initial data fetch | None |

## Phase Structure Template

### Phase 1: UI Components (Atoms/Molecules)

Focus: Reusable, stateless, styled components

**Investigation**:
```bash
# Find existing UI components
ls src/components/ui/
grep -r "interface.*Props" --include="*.tsx" src/components/ui/
```

**Task template**:
| Component | Path | Props | Existing? |
|-----------|------|-------|-----------|
| Button | `src/components/ui/Button.tsx` | `variant, size, disabled, onClick` | Extend existing |
| Input | `src/components/ui/Input.tsx` | `type, placeholder, error, onChange` | Create new |

**Reusability checklist**:
- [ ] Does similar component exist?
- [ ] Can we extend existing component with new variant?
- [ ] Is the API consistent with other components?
- [ ] Are props properly typed?
- [ ] Is component documented/storybook entry added?

### Phase 2: Feature Components (Organisms)

Focus: Feature-specific, may have local state

**Investigation**:
```bash
# Find existing feature patterns
ls src/components/features/
grep -r "useState\|useReducer" --include="*.tsx" src/components/features/
```

**Task template**:
| Component | Path | Responsibility | Dependencies |
|-----------|------|----------------|--------------|
| UserProfileCard | `src/components/features/UserProfileCard.tsx` | Display user info | Avatar, Badge, Button |
| EditProfileForm | `src/components/features/EditProfileForm.tsx` | Handle form state | Input, Button, useForm |

**Composition pattern**:
```
FeatureComponent
├── Uses: UI components (via import)
├── Props: Data + callbacks
├── Local state: Form state, UI state only
└── Emits: Events to parent (onSubmit, onChange)
```

### Phase 3: Service Layer

Focus: API communication, data transformation

**Investigation**:
```bash
# Find existing service patterns
ls src/services/
grep -r "fetch\|axios\|api\." --include="*.ts" src/services/
```

**Task template**:
| Service | Path | Methods | Endpoints |
|---------|------|---------|-----------|
| UserService | `src/services/user.service.ts` | `getProfile, updateProfile` | GET /users/:id, PUT /users/:id |

**Service structure**:
```typescript
// Pattern to follow
interface UserService {
  getProfile(id: string): Promise<UserDTO>;
  updateProfile(id: string, data: UpdateProfileDTO): Promise<UserDTO>;
}

// Implementation connects to API
// Returns DTOs, not raw responses
// Handles error transformation
```

### Phase 4: State Management

Focus: Global state, async operations

**Investigation**:
```bash
# Find store patterns (Redux)
ls src/store/
grep -r "createSlice\|createAsyncThunk" --include="*.ts" src/store/

# Find store patterns (Zustand/Pinia)
grep -r "create\(|defineStore" --include="*.ts" src/stores/
```

**Task template**:
| Store/Slice | Path | State | Actions |
|-------------|------|-------|---------|
| userSlice | `src/store/slices/userSlice.ts` | `{ profile, loading, error }` | fetchProfile, updateProfile |

**State flow**:
```
Component → dispatch(action) → Store → Service → API
                                  ↓
Component ← selector ← State update ← Response
```

### Phase 5: Page Integration

Focus: Route handling, data orchestration

**Investigation**:
```bash
# Find page/route structure
ls src/pages/ src/app/
grep -r "getServerSideProps\|loader\|useLoaderData" --include="*.tsx"
```

**Task template**:
| Page | Path | Data Requirements | Components |
|------|------|-------------------|------------|
| UserProfilePage | `src/pages/users/[id].tsx` | User profile, preferences | ProfileCard, EditForm |

**Page responsibilities**:
```
- Route parameter handling
- Initial data fetching
- Layout selection
- Component composition
- Error boundaries
```

## Data Flow Documentation

### Workflow Pattern

Document the data flow for each feature:

```
1. User Action
   └── Click "Save Profile" button

2. Component Handler
   └── EditProfileForm.onSubmit()

3. Store Action
   └── dispatch(updateProfile(data))

4. Service Call
   └── userService.updateProfile(id, data)

5. API Request
   └── PUT /api/users/:id

6. State Update
   └── Store receives response, updates state

7. UI Update
   └── Components re-render with new data
```

## Reusability Analysis

### Questions to ask:

1. **Does this component exist?**
   - Check ui/, components/, features/
   - Can we add a variant instead of new component?

2. **Is the API consistent?**
   - Follow existing prop naming conventions
   - Use same event handler patterns

3. **Can this be abstracted?**
   - Create base component for variations
   - Use composition over prop explosion

### Flexibility markers:

```markdown
| Component | Flexibility | Notes |
|-----------|-------------|-------|
| Button | High | Uses variant system, composable |
| UserCard | Medium | Specific but accepts render props |
| CheckoutFlow | Low | Highly specific to checkout feature |
```

## Component Checklist

For each new component:
- [ ] Props interface defined and exported
- [ ] Default props where applicable
- [ ] Ref forwarding if needed
- [ ] Accessibility attributes
- [ ] Responsive design considered
- [ ] Loading/error states if applicable
- [ ] Unit tests
- [ ] Storybook entry (if using)
