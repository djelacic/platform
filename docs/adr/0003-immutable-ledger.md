# ADR 0003: Immutable ledger with change transactions

Status: accepted

## Context
Financial outcomes must be explainable, reproducible and auditable, and closed accounting periods must not move.

## Decision
The ledger is append-only. Full allocation is calculated at event time. Every later change (settlement difference, cancellation, clawback, FX difference) is a new transaction of a change type, linked to its parent and root. There is no back-dating: posting date must fall in an open period, and changes to items in closed periods post in the current period with a reference to the original. Provisional items at period end stay as posted, with no accruals. Each transaction pins the rule and template versions it used.

## Consequences
Balances are projections of the transaction history. The accounting feed needs no restatement logic. Ripple effects default to delta only going forward.
