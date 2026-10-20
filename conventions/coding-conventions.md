---
type: convention
status: active
date: 2026-09-15
tags: [convention, code]
---

# Coding conventions

## Tooling

Bun runs, tests (`bun test`) and installs; TypeScript is strict with
`noUncheckedIndexedAccess`. `bun run typecheck` must pass.

## Layering

`http` → `service` → `fees` / `repository` → `domain`. Inner layers never import outer
ones. HTTP handlers only parse input, call the service and map errors.

## Rules live in one place

Every lending number (loan days, renewals, limits, hold days, fee rates) is a constant in
`src/domain/policy.ts`. The wiki pages [[concepts/loan]] and [[concepts/late-fee]] are
the source of truth for their values.

## Money

Integer cents everywhere, rounded as [[decisions/adr-002-fee-rounding]] says.

## Errors

Use cases throw `DomainError` with a code: `invalid`, `not_found` or `conflict`. Never
throw plain strings; never return error objects.

## Time

Services take a `clock` function instead of calling `new Date()` directly, so tests can
fix and advance time.

## Tests

One `bun test` case per rule. Build fixtures with `test/helpers.ts`; storage is the
in-memory repository from [[decisions/adr-001-in-memory-repository-first]].
