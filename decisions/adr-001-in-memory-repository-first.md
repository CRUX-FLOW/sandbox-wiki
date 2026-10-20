---
type: decision
status: active
date: 2026-09-15
tags: [adr, storage]
---

# ADR-001: In-memory repository first

## Context

The service is a prototype for one branch library. We want to validate the lending
rules ([[concepts/loan]], [[concepts/late-fee]], [[features/reservations-queue]]) before
choosing a database.

## Decision

- Store every entity in a generic `InMemoryRepository<T>` backed by a `Map`.
- Copy items on read and write (`structuredClone`) so callers cannot mutate stored state.
- The service depends only on the repository methods `get`, `list`, `save`, `delete`, so
  a database-backed implementation can replace it without touching the use cases.

## Consequences

- Data is lost on restart; acceptable for the prototype.
- No transactions: a use case that saves several entities can leave them inconsistent
  if it throws halfway. Keep validation before the first `save`.
- Ids are `prefix_N` counters, unique per process only.

See [[conventions/coding-conventions]] for the layering this relies on.
