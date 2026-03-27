# FlowRange — GitHub Copilot Instructions

This file guides GitHub Copilot on the architecture, conventions, and constraints of the FlowRange project.

---

## Project

**FlowRange** is a web-based project management application combining kanban boards, time tracking, and dashboards.

- **Backend**: C# (.NET 9) — Minimal API, simple architecture without CQRS or MediatR
- **Frontend**: Vue.js 3 with Composition API (`<script setup>`) and TypeScript
- **Persistence**: Entity Framework Core InMemory (SQLite acceptable for production)
- **Communication**: REST JSON (no GraphQL, no SignalR for now)

---

## Backend Conventions (C#)

- Use **Minimal API** (`app.MapGet`, `app.MapPost`, etc.) — no controllers
- Endpoints are organized by file in `/Endpoints/` (e.g. `TaskEndpoints.cs`, `DashboardEndpoints.cs`)
- Data models go in `/Models/` — simple classes with auto-properties
- Use **record types** for request/response DTOs
- Naming: PascalCase for classes, camelCase for JSON properties (`JsonPropertyName`)
- Always return `Results.Ok()`, `Results.NotFound()`, `Results.BadRequest()` — never raw status codes
- CORS must allow `http://localhost:5173` (default Vite port)
- No authentication in this version
- IDs are `Guid`

### Backend folder structure
```
/backend
  Program.cs
  /Models
    FlowTask.cs
    Project.cs
    TeamMember.cs
  /Endpoints
    TaskEndpoints.cs
    DashboardEndpoints.cs
  /Data
    FlowRangeDbContext.cs
```

---

## Frontend Conventions (Vue.js / TypeScript)

- Vue 3 with `<script setup lang="ts">` — no Options API
- State management: **Pinia** (not Vuex)
- Routing: **Vue Router**
- Styles: **Tailwind CSS** — utility classes directly in templates
- Component naming: PascalCase (`KanbanBoard.vue`, `TaskCard.vue`)
- One component = one file in `/src/components/`
- API calls in `/src/services/api.ts` — use native `fetch` with named functions
- TypeScript types in `/src/types/index.ts`
- Brand primary color: `#FF7900` (Expertime/Orange brand color)

### Frontend folder structure
```
/frontend
  /src
    /components
      KanbanBoard.vue
      KanbanColumn.vue
      TaskCard.vue
    /views
      BoardView.vue
      DashboardView.vue
    /stores
      taskStore.ts
    /services
      api.ts
    /types
      index.ts
    App.vue
    main.ts
```

---

## Reference Data Model

```typescript
// Task
interface Task {
  id: string           // Guid
  title: string
  description?: string
  status: 'todo' | 'in-progress' | 'done'
  priority: 'low' | 'medium' | 'high'
  createdAt: string    // ISO 8601
  updatedAt: string
}

// Coming in future waves:
// assigneeId?: string
// estimatedHours?: number
// timeEntries?: TimeEntry[]
```

---

## UI / Style Constraints

- UI labels, buttons, and messages must be in **French**
- Clean and modern design — no skeuomorphism
- Desktop-only responsive layout (no mobile for now)
- Always display a clean empty state (e.g. "Aucune tâche pour l'instant")
- Error messages must be explicit and visible

---

## What Copilot must NOT do

- Do not add JWT authentication unless explicitly asked
- Do not use third-party libraries not listed here (no Axios, no Vuetify, no PrimeVue)
- Do not create abstract service/repository classes — keep it simple
- Do not add structured logging (e.g. Serilog) — `Console.WriteLine` is fine for demos
- Do not generate unit tests unless explicitly requested
