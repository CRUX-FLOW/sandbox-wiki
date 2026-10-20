---
type: concept
status: active
date: 2026-10-05
tags: [domain, fees]
---

# Late fee

A **late fee** is charged when a [[concepts/loan]] is returned after its due date. It is
computed once, at return time, and stored on the loan as `feeCents`.

## Overdue days

Returning a book on its due date is free. The fee starts on the **first calendar day
after the due date**: a book returned one day after its due date is 1 day overdue, two
days after is 2 days overdue, and so on. Overdue days are counted in calendar days, not
24-hour periods.

## Amount

```
fee = round_half_up(overdueDays × 25¢ × categoryMultiplier)
fee = min(fee, book.replacementCostCents)
```

| [[concepts/book]] category | multiplier |
|---|---|
| general | 1 |
| children | 0.5 |
| reference | — (never lent) |

Example: a children's book returned 3 days late costs `3 × 25 × 0.5 = 37.5` → **38¢**.

Rounding happens once, on the total; see [[decisions/adr-002-fee-rounding]].
