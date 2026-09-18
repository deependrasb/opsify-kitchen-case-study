# Architecture Diagrams

This folder contains high-level architecture views for **Opsify Kitchen**.

| File | Description |
|------|-------------|
| [system-architecture.md](system-architecture.md) | System context — users, app, data, integrations (Mermaid) |
| [application-architecture.md](application-architecture.md) | Application modules and request flow (Mermaid) |
| [system-architecture.svg](system-architecture.svg) | Static system diagram suitable for README embeds |

## Reading guide

- Diagrams show **logical** components only.
- No hostnames, account IDs, API keys, or private network topology are included.
- Payment, messaging, and compliance boxes represent **integration categories**, not specific production endpoints.

## Suggested README embed

```markdown
![Opsify Kitchen system architecture](architecture/system-architecture.svg)
```
