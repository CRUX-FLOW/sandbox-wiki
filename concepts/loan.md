---
type: concept
status: active
date: 2026-09-28
tags: [domain, lending]
---

# Loan

A **loan** records one [[concepts/member]] holding one [[concepts/book]].

| Field | Meaning |
|---|---|
| `borrowedAt` | when the book left the desk |
| `dueAt` | `borrowedAt` plus the loan period |
| `returnedAt` | `null` while the loan is open |
| `renewals` | how many times the loan was renewed |
| `feeCents` | the [[concepts/late-fee]] fixed at return time |

## Loan period

The loan period defaults to **14 days**. A client may ask for a different period when
borrowing.

## Renewal

- A renewal moves `dueAt` forward by **14 days** from the current due date.
- A loan can be renewed **at most 2 times**.
- A renewal is refused while any other member is waiting for the book in the
  [[features/reservations-queue]].
- A closed loan cannot be renewed.

The full sequence is in [[features/lending-flow]].
