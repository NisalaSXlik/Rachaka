# Rachaka

Rachaka is a novel-writing application designed as a modular, multi-service platform for writing, organizing, and managing long-form fiction. The project combines a modern web interface with backend services, asynchronous processing, and AI-assisted features.

The application is being developed as a practical exploration of software architecture and cross-language system development, with different components responsible for specific areas of the platform.

## Technology Stack

- **Next.js / React** — frontend and writing interface
- **Laravel / PHP** — core backend, API, business logic, authentication, and data management
- **C# / .NET** — supporting application services
- **Java** — supporting backend/service components
- **C++** — performance-oriented and system-level components
- **Python** — ML/AI processing and intelligent writing features
- **PostgreSQL** — primary relational database
- **Redis** — caching, queues, and background processing
- **RabbitMQ** — asynchronous communication between services
- **Axios** — frontend API communication
- **Docker** — containerized development and service deployment
- **MCP (Model Context Protocol)** — integration of AI tools and external capabilities

## Architecture

```text
Rachaka
│
├── Web Application
│   └── Next.js / React
│
├── Core API
│   └── Laravel / PHP
│
├── Supporting Services
│   ├── C# / .NET
│   ├── Java
│   └── C++
│
├── AI / ML Services
│   └── Python
│
├── Messaging
│   ├── Redis
│   └── RabbitMQ
│
└── Data
    └── PostgreSQL
