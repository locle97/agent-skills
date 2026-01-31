# Implementation Plan Template

Use this template structure when generating implementation plans.

---

# [Feature Name] Implementation Plan

**Created:** [Date]
**Status:** Draft | In Review | Approved
**Estimated Phases:** [N]

## Executive Summary

[2-3 sentences describing what will be built and the high-level approach]

---

## 1. Context & Requirements

### 1.1 Business Requirements
- [Requirement 1]
- [Requirement 2]

### 1.2 Technical Requirements
- [Requirement 1]
- [Requirement 2]

### 1.3 Out of Scope
- [Explicitly excluded item 1]
- [Explicitly excluded item 2]

---

## 2. Current State Analysis

### 2.1 Backend
| Aspect | Current State | Notes |
|--------|---------------|-------|
| Relevant Services | | |
| Database Schema | | |
| API Endpoints | | |
| Existing Patterns | | |

### 2.2 Frontend
| Aspect | Current State | Notes |
|--------|---------------|-------|
| Relevant Components | | |
| State Management | | |
| API Integration | | |
| Routing | | |

### 2.3 Dependencies & Risks
| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| | Low/Med/High | Low/Med/High | |

---

## 3. Technical Design

### 3.1 Architecture Overview
[High-level architecture description or diagram]

### 3.2 Backend Design
#### Domain Model
[Key entities, aggregates, value objects]

#### API Contracts
```
[Endpoint definitions or GraphQL schema]
```

#### Database Changes
```sql
-- Migration: [description]
```

### 3.3 Frontend Design
#### Component Hierarchy
```
PageComponent
├── FeatureContainer
│   ├── ComponentA
│   └── ComponentB
└── SharedComponent
```

#### State Design
[State shape and management approach]

---

## 4. Implementation Phases

### Phase 1: [Name] - Foundation
**Goal:** [What this phase achieves]
**Prerequisites:** None

#### Backend Tasks
| # | Task | Owner | Acceptance Criteria |
|---|------|-------|---------------------|
| 1.1 | | Backend | |
| 1.2 | | Backend | |

#### Frontend Tasks
| # | Task | Owner | Acceptance Criteria |
|---|------|-------|---------------------|
| 1.3 | | Frontend | |
| 1.4 | | Frontend | |

#### Definition of Done
- [ ] Unit tests passing
- [ ] Code reviewed
- [ ] [Additional criteria]

---

### Phase 2: [Name] - Core Features
**Goal:** [What this phase achieves]
**Prerequisites:** Phase 1

#### Backend Tasks
| # | Task | Owner | Acceptance Criteria |
|---|------|-------|---------------------|
| 2.1 | | Backend | |

#### Frontend Tasks
| # | Task | Owner | Acceptance Criteria |
|---|------|-------|---------------------|
| 2.2 | | Frontend | |

#### Integration Points
- [How backend and frontend connect in this phase]

#### Definition of Done
- [ ] Integration tests passing
- [ ] [Additional criteria]

---

### Phase 3: [Name] - Polish & Integration
**Goal:** [What this phase achieves]
**Prerequisites:** Phase 2

[Continue pattern...]

---

## 5. Testing Strategy

### 5.1 Unit Testing
| Component | Coverage Target | Key Scenarios |
|-----------|-----------------|---------------|
| | | |

### 5.2 Integration Testing
| Integration Point | Test Approach |
|-------------------|---------------|
| | |

### 5.3 E2E Testing
| User Flow | Priority |
|-----------|----------|
| | High/Med/Low |

---

## 6. Rollout Strategy

### 6.1 Feature Flags
| Flag | Purpose | Default |
|------|---------|---------|
| | | |

### 6.2 Migration Steps
1. [Step 1]
2. [Step 2]

### 6.3 Rollback Plan
[How to revert if issues arise]

---

## 7. Open Questions

| Question | Owner | Status |
|----------|-------|--------|
| | | Open/Resolved |

---

## Appendix

### A. Relevant Files
**Backend:**
- `path/to/file.ts` - [Purpose]

**Frontend:**
- `path/to/component.tsx` - [Purpose]

### B. Reference Links
- [Design doc]
- [API documentation]
- [Related PRs]
