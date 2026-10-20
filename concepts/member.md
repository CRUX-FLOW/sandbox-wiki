---
type: concept
status: active
date: 2026-09-15
tags: [domain, members]
---

# Member

A **member** is a person registered with the library who can borrow [[concepts/book]]s.

| Field | Meaning |
|---|---|
| `name` | required, not blank |
| `email` | required, must look like `local@domain.tld` |
| `joinedAt` | set by the service when the member is created |

## Limits

- At most **5 active loans** at a time; a sixth borrow is refused (`conflict`).
- One open [[concepts/reservation]] per book per member.

Members are not deleted in this version. Unpaid [[concepts/late-fee]]s are recorded on
the loan but do not block borrowing yet.
