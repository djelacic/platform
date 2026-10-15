# Platform

A multi-tenant, white-label business platform that Clients (for example travel insurers) rent and deliver under their own brand to their Customers. A common core exposes REST APIs and MCP servers, so vertical applications and AI agents use the same services with the same security and audit.

First vertical for the proof of concept: travel insurance.

## Status

Phase 0: foundations. See `docs/` for the design and the backlog.

## Stack

- .NET modular monolithic (ASP.NET Core), one deployable host
- PostgreSQL, one shared database with a Client id on every record and row-level security
- Azure (Container Apps, managed PostgreSQL), infrastructure as code
- GitHub Actions for CI and deployment
- MCP servers over streamable HTTP with OAuth

## Layout

| Path | Purpose |
| --- | --- |
| `docs/` | Domain model, MCP catalogue, backlog, architecture decision records |
| `contracts/` | API, MCP and event definitions |
| `src/` | Host, building blocks, modules, MCP servers, web apps |
| `tests/` | Architecture, isolation, ledger scenario, contract, agent evaluation and end-to-end tests |
| `infra/` | Infrastructure as code |
| `.github/` | Pipelines and dependency updates |

## Working agreements

Read `CLAUDE.md` for the rules that apply to every change. Decisions that are hard to reverse get a short record in `docs/adr/`.
