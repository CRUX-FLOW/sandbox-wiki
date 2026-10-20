---
type: index
status: active
date: 2026-10-12
tags: [index]
---

# library-lending wiki

The spec for the `sandbox` library-lending service. One line per page.

## Concepts
- [[concepts/book]] — a lendable copy, its category, status and replacement cost
- [[concepts/member]] — a person who borrows; name, email, active-loan limit
- [[concepts/loan]] — one member holding one book until a due date; renewals
- [[concepts/reservation]] — a member's place in a book's queue and its hold
- [[concepts/late-fee]] — how overdue days turn into cents

## Features
- [[features/lending-flow]] — borrow, renew and return, step by step
- [[features/reservations-queue]] — FIFO queue, holds and hold expiry

## Decisions
- [[decisions/adr-001-in-memory-repository-first]] — start with Map-backed repositories behind one interface
- [[decisions/adr-002-fee-rounding]] — integer cents, round once on the total, half up

## Conventions
- [[conventions/coding-conventions]] — layering, policy constants, money, errors, tests

## Other
- [[log]] — chronological record of wiki changes
