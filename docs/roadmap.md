Your roadmap should describe the system you are already building, not three separate systems. The clean way to do that is to treat the app as one monorepo with a thin client mediator and one modular backend.

---

# 1. Current architecture

You are building:

> one product with a single frontend, a single API, and clear extension points

```txt id="core1"
apps/web   -> Next.js UI
apps/api   -> Laravel modular monolith API
PostgreSQL -> primary data store
Redis      -> cache, queues, async work
Axios      -> request mediator between web and api
```

Axios is the client-side mediator. The frontend talks to Laravel through a shared HTTP layer instead of calling endpoints ad hoc from every component.

---

# 2. What the roadmap should represent

The roadmap is not a sequence of separate architectures. It is a layered product plan:

```txt id="layers"
Layer 1: Core domain
- documents
- users
- drafts
- comments
- revisions

Layer 2: API integration
- Axios client
- Laravel endpoints
- validation and auth
- request/response mapping

Layer 3: Workflow and intelligence
- AI actions
- MCP-style tool adapters
- agent workflows
- queue-driven automation
```

---

# 3. Phase 1 = Core product layer

This is the actual writing app.

### Backend modules

```txt id="p1"
Modules/
  Documents/
  Users/
  Comments/
  Drafts/
  Revisions/
```

### Frontend routes

```txt id="p1f"
Next.js
  /editor
  /documents
  /dashboard
```

### Communication pattern

The UI reads and writes through Axios, which handles the API boundary consistently.

Example usage:

```txt id="axios1"
UI action -> Axios request -> Laravel controller -> module service -> database
```

### Result

You already have a usable writing platform with a clean client-server split.

---

# 4. Phase 2 = Tool layer inside the API

MCP should not be treated as a separate system. In this roadmap, it is a tool interface pattern inside the Laravel API.

```txt id="mcp1"
Modules/AI/
  MCP/
    Clients/
    Tools/
    Adapters/
```

### What this means

* AI capabilities are exposed as backend services
* external tools are wrapped in adapters
* the frontend still goes through Axios and Laravel endpoints

### Example endpoint

```txt id="mcp2"
POST /api/ai/run
```

That endpoint can trigger a rewrite, summarize a document, generate an outline, or call any supported tool without changing the frontend architecture.

---

# 5. Phase 3 = Workflow layer on top of the API

Agents are not separate apps. They are backend workflows that use the existing modules, queues, and tool adapters.

```txt id="agent1"
Modules/AI/
  Agents/
    WritingAgent.php
    ReviewAgent.php
```

### What they use

* Laravel services and module state
* Redis queues and background jobs
* MCP-style tool adapters
* stored drafts and revisions

### Example flow

```txt id="agentflow"
User edits text
   ↓
Draft saved through Axios
   ↓
Laravel dispatches a queued job
   ↓
Agent runs tool calls
   - grammar check
   - rewrite
   - tone adjustment
   ↓
Suggestions are stored
   ↓
Frontend fetches results through Axios
```

---

# 6. What changes in implementation

### Do

* keep the monorepo split between `apps/web` and `apps/api`
* use Axios as the single HTTP mediator in the frontend
* keep Laravel modular from the start
* introduce Redis and queues early
* isolate AI logic in a dedicated module

### Do not

* build separate MCP infrastructure
* split AI into a separate backend
* let components call Laravel endpoints directly in inconsistent ways
* redesign the system for each roadmap phase

---

# 7. Final structure

```txt id="final"
Monorepo

apps/
  web (Next.js editor UI)
  api (Laravel modular monolith)
    Modules/
      Documents/
      Users/
      Comments/
      Drafts/
      Revisions/
      AI/
        MCP/
        Agents/

infra/
  docker/
  redis/
  postgres/
```

---

# 8. Core insight

The roadmap is not sequential. It is one architecture that expands by modules.

Axios is the mediation layer between the frontend and the API. MCP and agents are implementation layers inside Laravel, not separate systems that require a rebuild later.
