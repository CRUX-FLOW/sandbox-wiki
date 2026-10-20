---
type: feature
status: active
date: 2026-09-28
tags: [feature, lending]
---

# Lending flow

Borrow, renew and return a [[concepts/book]]. Every step is one HTTP call to the
`sandbox` service.

## Borrow — `POST /loans`

Body: `{ bookId, memberId, loanDays? }`.

1. The [[concepts/member]] and the book must exist (`not_found`).
2. Reference books are refused (`conflict`).
3. A member with 5 active loans is refused (`conflict`).
4. A book `on_loan` is refused. A book `on_hold` is lent only to the member whose
   [[concepts/reservation]] is `ready`; that reservation becomes `fulfilled`.
5. A [[concepts/loan]] is created with `dueAt = now + loanDays` (default 14) and the
   book becomes `on_loan`.

## Renew — `POST /loans/:id/renew`

Allowed at most twice per loan and only while nobody waits for the book. Each renewal
adds 14 days to `dueAt`.

## Return — `POST /loans/:id/return`

1. The loan must be open.
2. `returnedAt` is set and the [[concepts/late-fee]] is fixed on the loan.
3. If members are waiting, the first one gets a hold (see
   [[features/reservations-queue]]); otherwise the book is `available` again.

## Errors

`invalid` → 400, `not_found` → 404, `conflict` → 409, always as `{ error, code }`.
