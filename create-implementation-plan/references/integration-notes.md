# Frontend/Backend Integration Guide

## API Contract Definition

### Endpoint Documentation Template

For each endpoint, document:

```markdown
### [Feature Name] - [Action]

**Endpoint**: `[METHOD] /api/v1/[resource]`

**Request**:
```typescript
interface RequestDTO {
  // properties with types
}
```

**Response**:
```typescript
interface ResponseDTO {
  // properties with types
}
```

**Error Responses**:
| Status | Code | Description |
|--------|------|-------------|
| 400 | VALIDATION_ERROR | Invalid input |
| 404 | NOT_FOUND | Resource not found |
| 409 | CONFLICT | Business rule violation |

**Frontend Usage**:
- Service: `src/services/[feature].service.ts`
- Method: `[methodName]()`
- Store action: `[actionName]`
```

## Type Sharing Strategy

### Option 1: Shared Types Package
```
packages/
├── shared-types/
│   ├── src/
│   │   ├── user.ts
│   │   └── order.ts
│   └── package.json
├── frontend/
└── backend/
```

### Option 2: API Schema Generation
```bash
# From OpenAPI/Swagger
npx openapi-typescript api/openapi.yaml -o src/types/api.ts

# From GraphQL
npx graphql-codegen
```

### Option 3: Manual Sync (Document which to update first)
```markdown
| Type | Backend Path | Frontend Path | Source of Truth |
|------|--------------|---------------|-----------------|
| UserDTO | `src/api/dto/user.dto.ts` | `src/types/user.ts` | Backend |
| CreateUserRequest | `src/api/dto/create-user.dto.ts` | `src/types/user.ts` | Backend |
```

## Integration Phases

### Phase 1: Contract Agreement
Tasks:
- [ ] Define request/response DTOs
- [ ] Document error codes
- [ ] Agree on pagination format
- [ ] Define authentication headers

### Phase 2: Backend Implementation
Tasks:
- [ ] Implement endpoint
- [ ] Add validation
- [ ] Add error handling
- [ ] Write integration tests
- [ ] Document in OpenAPI/Swagger

### Phase 3: Frontend Service Layer
Tasks:
- [ ] Create/update service methods
- [ ] Add type definitions
- [ ] Handle error mapping
- [ ] Add loading states

### Phase 4: Frontend Integration
Tasks:
- [ ] Connect store to service
- [ ] Update components
- [ ] Test with mock server (optional)
- [ ] E2E testing

## Error Handling Alignment

### Backend Error Format
```typescript
interface ApiError {
  code: string;        // Machine-readable: "VALIDATION_ERROR"
  message: string;     // Human-readable: "Email is invalid"
  details?: object;    // Additional context
}
```

### Frontend Error Mapping
```typescript
// Map API errors to UI messages
const errorMessages: Record<string, string> = {
  'VALIDATION_ERROR': 'Please check your input',
  'NOT_FOUND': 'Resource not found',
  'UNAUTHORIZED': 'Please log in again',
};
```

## Real-time Integration (if applicable)

### WebSocket Events
```markdown
| Event | Direction | Payload | Frontend Handler |
|-------|-----------|---------|------------------|
| order.updated | Server→Client | `{orderId, status}` | `useOrderUpdates` hook |
| user.typing | Client→Server | `{roomId, userId}` | `sendTypingIndicator()` |
```

### Server-Sent Events
```markdown
| Stream | Endpoint | Event Types | Frontend Hook |
|--------|----------|-------------|---------------|
| notifications | `/api/sse/notifications` | `new`, `read` | `useNotificationStream` |
```

## Integration Checklist

### Before Development
- [ ] API contract documented
- [ ] Error codes defined
- [ ] Types shared/generated
- [ ] Auth mechanism agreed

### During Development
- [ ] Backend: Endpoints return correct DTOs
- [ ] Backend: Validation returns proper errors
- [ ] Frontend: Service handles all response types
- [ ] Frontend: Error states displayed correctly

### Before Deployment
- [ ] E2E tests passing
- [ ] CORS configured correctly
- [ ] Rate limiting considered
- [ ] Logging/monitoring in place

### Post-Integration
- [ ] API documentation updated
- [ ] Frontend types regenerated (if using codegen)
- [ ] Performance testing done
- [ ] Error tracking configured

## Common Integration Issues

### CORS
```
Solution: Backend must include frontend origin in allowed origins
```

### Date/Time Formats
```
Agreement: Use ISO 8601 strings (e.g., "2024-01-15T10:30:00Z")
Frontend: Parse with date library (date-fns, dayjs)
```

### Pagination
```
Standard format:
{
  data: T[],
  meta: {
    total: number,
    page: number,
    pageSize: number,
    totalPages: number
  }
}
```

### File Uploads
```
Agreement: Use multipart/form-data
Backend: Parse with multer/formidable
Frontend: Use FormData API
```
