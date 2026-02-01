# Frontend Architecture Patterns

## Detection Patterns

### React/Next.js
- Look for: `package.json` with `react`, `next`, `jsx/tsx` files
- Routing: `pages/`, `app/`, `react-router`, `@tanstack/router`
- State: `redux/`, `store/`, `zustand`, `jotai`, `recoil`, React Context
- Common structure: `components/`, `hooks/`, `pages/`, `features/`, `lib/`

### Vue/Nuxt
- Look for: `package.json` with `vue`, `nuxt`, `.vue` files
- Routing: `pages/`, `router/`, `vue-router`
- State: `stores/`, `pinia`, `vuex`
- Common structure: `components/`, `composables/`, `pages/`, `views/`

## Route-to-Component Mapping

### React Router
```
/users/:id → pages/Users.tsx or routes/users/$id.tsx
```
Search for: `path="/users"`, `Route path=`, `createBrowserRouter`

### Next.js App Router
```
/users/[id] → app/users/[id]/page.tsx
```
Search for: directory structure matches URL path

### Vue Router
```
/users/:id → views/UserDetail.vue or pages/users/[id].vue
```
Search for: `{ path: '/users/:id'`, route definitions in `router/index.ts`

### Nuxt
```
/users/:id → pages/users/[id].vue
```
File-based routing matches URL structure

## Analysis Checklist

1. **Entry Component**: Find the page/view handling the route
2. **Child Components**: Identify UI components used in the page
3. **Data Fetching**: Locate API calls, hooks, composables
4. **State Management**: Find relevant stores/slices/atoms
5. **Forms/Validation**: Identify form handling and validation logic
