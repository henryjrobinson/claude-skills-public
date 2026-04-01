---
name: architecture-diagram
description: Generate and update Mermaid architecture diagrams for any project by analyzing the codebase.
---

# Architecture Diagram Generator

Analyze the current codebase and generate Mermaid diagrams that document the system architecture.

## Trigger
`/architecture-diagram` or `/architecture-diagram [type]`

Types: `system`, `agents`, `data-flow`, `database`, `user-flow`, `all`

## Instructions

When this skill is invoked:

### 1. Analyze Codebase Structure

Explore the project to understand its architecture:

```bash
# Discover project structure
ls -R --depth=2

# Find route/endpoint definitions
grep -rn "router\.\|app\.\|@app\.\|@router\." --include="*.ts" --include="*.py" --include="*.js"

# Find database schemas/models
find . -name "*.sql" -o -name "models.*" -o -name "schema.*" | head -20

# Find service/module boundaries
find . -type d -name "services" -o -name "modules" -o -name "packages" -o -name "apps"

# Find config for external services
grep -rn "API_KEY\|DATABASE_URL\|REDIS_URL\|S3_BUCKET" --include="*.env*" --include="*.yaml" --include="*.toml"
```

Adapt discovery commands to the project's language and framework.

### 2. Generate Diagrams

Create/update `docs/ARCHITECTURE_DIAGRAMS.md` with the following sections (include only those relevant to the project):

#### System Overview
High-level diagram showing all major components and their connections:
- Frontend(s) and hosting
- Backend services and APIs
- Databases and storage
- External APIs and third-party services
- Message queues, caches, CDNs

Use `graph TB` with subgraphs for logical grouping (e.g., "Frontend", "Backend", "Data Layer", "External Services").

#### Data Flow
How data moves through the system from input to storage:
- Entry points (user input, API calls, webhooks, file uploads)
- Processing steps (validation, transformation, enrichment)
- Storage destinations (databases, object storage, caches)

Use `flowchart LR` to show left-to-right data flow.

#### Database Schema (ERD)
Entity-relationship diagram for the data model:
- Tables/collections and their key fields
- Relationships (one-to-many, many-to-many)
- Foreign keys and indexes

Use `erDiagram` with proper relationship notation.

#### User Flow
How users navigate through the application:
- Entry points (landing page, deep links)
- Authentication flow
- Core user journeys
- Decision points and branches

Use `flowchart TD` for top-down user navigation.

#### Agent/Pipeline Diagram (if applicable)
For projects with AI agents, background workers, or multi-step pipelines:
- Agent/worker sequence and responsibilities
- Async vs sync operations
- Data handoff between stages

Use `sequenceDiagram` for ordered interactions or `flowchart` for parallel pipelines.

### 3. Diagram Guidelines

- **Label everything** — nodes should have descriptive names, not just "Service A"
- **Show protocols** — label edges with REST, gRPC, SSE, WebSocket, etc.
- **Include tech stack** — add framework/database names in node labels (e.g., `API[Express API]`, `DB[(PostgreSQL)]`)
- **Keep it readable** — if a diagram has more than ~15 nodes, split into sub-diagrams
- **Use standard shapes** — `[]` for services, `[()]` for databases, `(())` for external APIs, `[/  /]` for user-facing pages

### 4. Diagram Locations

Save all diagrams to: `docs/ARCHITECTURE_DIAGRAMS.md`

Optionally embed key diagrams in:
- `README.md` — system overview only
- Relevant architecture docs if they exist

### 5. Verification

After generating, verify diagrams:
- Check Mermaid syntax is valid (no unclosed brackets, valid node IDs)
- Ensure all referenced components actually exist in the codebase
- Cross-reference with any existing architecture documentation
- Flag any components found in code but missing from diagrams

## Output

1. Show all generated diagrams
2. Ask: "Should I save these to docs/ARCHITECTURE_DIAGRAMS.md?"
3. Ask: "Should I embed the system overview in README.md?"
4. List any architectural questions that came up during analysis
