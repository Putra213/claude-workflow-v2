---
name: architecture-patterns
description: Provides guidance on software architecture patterns and design decisions. Use when designing systems, choosing patterns, structuring projects, or when asked about architectural approaches.
---

# Architecture Patterns Skill

## Pattern Selection Guide

### By Project Size

| Size | Recommended Pattern |
|------|---------------------|
| Small (<10K LOC) | Simple MVC/Layered |
| Medium (10K-100K) | Clean Architecture |
| Large (>100K) | Modular Monolith or Microservices |

### By Team Size

| Team | Recommended |
|------|-------------|
| 1-3 devs | Monolith with clear modules |
| 4-10 devs | Modular Monolith |
| 10+ devs | Microservices (if justified) |

## Common Patterns

### 1. Layered Architecture
```
┌─────────────────────────────┐
│       Presentation          │  ← UI, API Controllers
├─────────────────────────────┤
│       Application           │  ← Use Cases, Services
├─────────────────────────────┤
│         Domain              │  ← Business Logic, Entities
├─────────────────────────────┤
│      Infrastructure         │  ← Database, External APIs
└─────────────────────────────┘
```
**Use when**: Simple CRUD apps, small teams, quick prototypes

### 2. Clean Architecture
```
┌─────────────────────────────────────┐
│            Frameworks & Drivers      │
│  ┌─────────────────────────────┐    │
│  │     Interface Adapters       │    │
│  │  ┌─────────────────────┐    │    │
│  │  │   Application       │    │    │
│  │  │  ┌─────────────┐    │    │    │
│  │  │  │   Domain    │    │    │    │
│  │  │  └─────────────┘    │    │    │
│  │  └─────────────────────┘    │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
```
**Use when**: Complex business logic, long-lived projects, testability is key

### 3. Hexagonal (Ports & Adapters)
```
        ┌──────────┐
        │ HTTP API │
        └────┬─────┘
             │ Port
    ┌────────▼────────┐
    │                 │
    │   Application   │
    │     Core        │
    │                 │
    └────────┬────────┘
             │ Port
        ┌────▼─────┐
        │ Database │
        └──────────┘
```
**Use when**: Need to swap external dependencies, multiple entry points

### 4. Event-Driven Architecture
```
Producer → Event Bus → Consumer
              │
              ├─→ Consumer
              │
              └─→ Consumer
```
**Use when**: Loose coupling needed, async processing, scalability

### 5. CQRS (Command Query Responsibility Segregation)
```
┌─────────────┐      ┌─────────────┐
│  Commands   │      │   Queries   │
│  (Write)    │      │   (Read)    │
└──────┬──────┘      └──────┬──────┘
       │                    │
       ▼                    ▼
  Write Model          Read Model
       │                    │
       └────────┬───────────┘
                ▼
           Event Store
```
**Use when**: Different read/write scaling, complex domains, event sourcing

## Directory Structure Patterns

### Feature-Based (Recommended for medium+)
```
src/
├── features/
│   ├── users/
│   │   ├── api/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   └── types/
│   └── orders/
│       ├── api/
│       ├── components/
│       └── ...
├── shared/
│   ├── components/
│   ├── hooks/
│   └── utils/
└── app/
    └── ...
```

### Layer-Based (Simple apps)
```
src/
├── controllers/
├── services/
├── models/
├── repositories/
└── utils/
```

## Decision Framework

When making architectural decisions, consider:

1. **Simplicity** - Start simple, evolve when needed
2. **Team Skills** - Match architecture to team capabilities
3. **Requirements** - Let business needs drive decisions
4. **Scalability** - Consider growth trajectory
5. **Maintainability** - Optimize for change

### Trade-off Analysis Template
```markdown
## Decision: [What we're deciding]

### Options Considered
1. Option A: [Description]
2. Option B: [Description]

### Trade-offs
| Criteria | Option A | Option B |
|----------|----------|----------|
| Complexity | Low | High |
| Scalability | Medium | High |
| Team familiarity | High | Low |

### Decision
We chose [Option] because [reasoning].

### Consequences
- [What this enables]
- [What this constrains]
```
