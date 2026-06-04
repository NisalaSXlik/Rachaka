# Rachaka

Rachaka is a simple writing application built with:

- **Next.js** for the frontend
- **Laravel** for the backend
- **Axios** as the shared HTTP mediator between the frontend and backend
- **PostgreSQL** for primary data
- **Redis** for cache, queues, and background work

It also includes a modular learning skeleton for:

- **MCP (Model Context Protocol)** tool adapters inside the API
- **ML/AI agent workflows** built on top of the existing backend modules

## Current Architecture

```text
Rachaka/
├── apps/
│   ├── web/           # Next.js app
│   └── api/           # Laravel modular monolith API
├── agents/
│   ├── mcp/           # MCP learning and integration notes
│   └── ml-ai/         # ML/AI agent learning and experiments
└── docs/
    └── roadmap.md     # layered architecture and implementation roadmap
```

## How the stack fits together

- The Next.js app handles the editor and writing experience.
- Axios is the single request layer used by the frontend to talk to the API.
- Laravel owns the domain modules, validation, persistence, and background jobs.
- MCP and agent logic live inside the API as extension layers, not separate apps.