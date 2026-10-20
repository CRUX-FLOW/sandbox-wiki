---
type: concept
status: active
date: 2026-10-12
tags: [domain, reservations]
---

# Reservation

A **reservation** is a [[concepts/member]]'s place in the queue for a [[concepts/book]]
that is currently not available.

## Status

| Status | Meaning |
|---|---|
| `waiting` | in the queue |
| `ready` | the copy is on hold for this member until `holdExpiresAt` |
| `fulfilled` | the member borrowed the held copy |
| `expired` | the hold ran out before the member came |
| `cancelled` | the member withdrew |

## Rules

- An `available` book cannot be reserved: the member should borrow it.
- A member has at most one `waiting` or `ready` reservation per book.
- A hold lasts **3 days** from the moment the reservation becomes `ready`.

How the queue moves is described in [[features/reservations-queue]].
