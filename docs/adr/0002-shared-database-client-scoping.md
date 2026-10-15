# ADR 0002: One shared database, Client id on every record

Status: accepted

## Context
The platform is rented to many Clients and delivered under each Client's brand. Every transaction must link to a Client.

## Decision
Use one PostgreSQL database for multiple Clients. Every Client-owned table has a mandatory client id, row-level security keyed to the Client in the caller's token, and composite keys that include the client id. Route each Client to a database through a lookup so a Client can later move to a dedicated database or region. Use per-Client encryption keys for sensitive fields.

## Consequences
Low cost and simple operations. Isolation depends on tested row-level security, so isolation tests run in CI and the application database role cannot bypass it. Per-Client restore needs a per-Client export design.
