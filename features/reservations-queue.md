---
type: feature
status: active
date: 2026-10-12
tags: [feature, reservations]
---

# Reservations queue

Each [[concepts/book]] has its own first-in-first-out queue of `waiting`
[[concepts/reservation]]s, ordered by `createdAt`.

## Joining — `POST /reservations`

Body: `{ bookId, memberId }`. Refused when the book is `available` or the member already
has an open reservation for it.

## Promotion

When the book comes back (return, expired hold or cancelled hold):

1. The oldest `waiting` reservation becomes `ready` with `holdExpiresAt = now + 3 days`.
2. The book becomes `on_hold`; only that [[concepts/member]] may borrow it.
3. If nobody is waiting, the book becomes `available`.

## Hold expiry

A sweep runs every hour. Each `ready` reservation past `holdExpiresAt` becomes `expired`
and the copy is promoted to the next member as above.

## Cancelling — `DELETE /reservations/:id`

A `waiting` or `ready` reservation can be cancelled. Cancelling a `ready` one promotes
the next member immediately.

## Interaction with renewals

While the queue is not empty, the current [[concepts/loan]] cannot be renewed; see
[[features/lending-flow]].
