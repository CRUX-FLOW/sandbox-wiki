---
type: concept
status: active
date: 2026-09-15
tags: [domain, catalogue]
---

# Book

A **book** is one physical copy in the catalogue. Two copies of the same title are two
books with different ids.

| Field | Meaning |
|---|---|
| `title`, `author`, `isbn` | catalogue data; `title` is required |
| `category` | `general`, `children` or `reference` |
| `replacementCostCents` | what the library pays to replace the copy; a positive integer |
| `status` | `available`, `on_loan` or `on_hold` |

## Categories

- **general** — lendable, full [[concepts/late-fee]] rate.
- **children** — lendable, half the daily late-fee rate.
- **reference** — never leaves the library; borrowing it is refused.

## Status

```
available ──borrow──▶ on_loan ──return, queue empty──▶ available
                         │
                         └──return, queue not empty──▶ on_hold ──borrow by holder──▶ on_loan
                                                          └──hold expires, queue empty──▶ available
```

A book is `on_hold` only while a [[concepts/reservation]] for it is `ready`. See
[[features/lending-flow]] and [[features/reservations-queue]].
