# ADR 0001: Modular monolith first

Status: accepted

## Context
One developer, limited budget before a proof of concept, and a domain still being proven.

## Decision
Build one deployable ASP.NET Core host with a module per bounded context. Each module owns its database schema and exposes a public Api project and domain events. Extract a module into a service only on evidence of need.

## Consequences
Simple to run and test. Boundaries are enforced by architecture tests, not by the network.
