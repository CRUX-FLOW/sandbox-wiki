---
type: log
status: active
date: 2026-10-12
tags: [log]
---

# Log

## [2026-10-12] ingest | Hold expiry and reservation cancel
Holds now expire after 3 days; cancelling a ready reservation passes the copy on. [[features/reservations-queue]], [[concepts/reservation]]

## [2026-10-05] ingest | Fee rounding rule
Fees are rounded once on the total, half up. [[decisions/adr-002-fee-rounding]], [[concepts/late-fee]]

## [2026-09-28] ingest | Reservations and renewals
Added the FIFO queue and loan renewals. [[features/reservations-queue]], [[features/lending-flow]], [[concepts/loan]]

## [2026-09-15] ingest | Initial spec
Books, members, loans and late fees; in-memory storage first. [[concepts/book]], [[concepts/member]], [[decisions/adr-001-in-memory-repository-first]], [[conventions/coding-conventions]]
