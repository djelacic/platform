# Platform

Multi-tenant, white-label platform for insurers (Clients). .NET modular monolith, PostgreSQL, Azure. Exposes REST APIs and MCP servers over the same core services.

## Terms

- Platform operator: runs the platform and rents it to Clients.
- Client: an enterprise renting the platform (for example a travel insurer). Owns its products, pricing, Partners, Dealers, Customers and ledger.
- Customer: the end consumer. Roles on a subscription: subscriber, beneficiary, payer.
- Partner: a service provider (assistance, medical, repair) paid under a rate schedule.
- Dealer: an intermediary that sells a Client's products and earns commission.
- Offer: a product made available through a channel (direct, dealer-sold, corporate scheme).

Use these names in code, tests and documents.

## Rules

- Modules call only another module's Api project and subscribe to its events. Architecture tests enforce this.
- Every command and query runs with a Client id from the caller's token. Row-level security enforces it. Never bypass it.
- The ledger is append-only. Every change is a new transaction linked to its parent and root. No updates, deletes or back-dating. Posting date must fall in an open period.
- Allocation is calculated in full at event time. Settlement adjusts through change transactions. Commission lines are created at sale.
- Products, pricing, funding and commission are versioned, effective-dated data, never code branches.
- Idempotency key on every state-changing operation, unique per Client.
- SQL migrations per module, expand then contract, run by the pipeline and never at application startup.
- MCP tools are hand-designed and intent-level. Risk classes: R0, R1, W1, W2 (preview then commit), W3 (proposal only).

## Commands

- Build: `dotnet build`
- Test: `dotnet test`

Add migration, run and local database commands here once the solution exists.

## Working agreements

- One thin vertical slice per pull request. Plan first, then implement.
- Show the diff for review before changing row-level security policies, authentication, ledger constraints or migrations.
- Write a short ADR in `docs/adr/` for decisions that are hard to reverse.
- Keep the documents in `docs/` in step with the code.
