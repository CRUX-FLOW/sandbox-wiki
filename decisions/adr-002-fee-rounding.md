---
type: decision
status: active
date: 2026-10-05
tags: [adr, fees, money]
---

# ADR-002: Fee rounding rule

## Context

The children's-book rate is half of 25¢, so daily amounts can end in half a cent.
Rounding each day separately made a 3-day fee 39¢ (13 + 13 + 13) while the desk staff
expected 38¢.

## Decision

- All money is integer cents.
- A [[concepts/late-fee]] is computed as one product (`days × rate × multiplier`) and
  **rounded once, half up**, to whole cents.
- The cap at the [[concepts/book]] replacement cost is applied after rounding.

## Consequences

- Fees no longer depend on how the days are grouped.
- Formatting (`$0.38`) happens only at the edge, never in calculations; see
  [[conventions/coding-conventions]].
