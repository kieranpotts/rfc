# Supersede RFC

Marks an implemented RFC as superseded by a later one.

## What it does

- Confirms that a later, currently-implemented RFC has replaced a
  previously-implemented decision.
- Sets the superseded RFC's `Status: SUPERSEDED`.
- Updates the `Superseded by` link.
- Verifies the successor links back via `Supersedes`.
- Swaps the lifecycle label to `#superseded`.

## How to invoke

> Supersede RFC

> Event sourcing for audit log is superseded by temporal data model

## Recommended models

A fast, inexpensive model is enough. Confirming the cross-references between
the two RFCs is a mechanical check.
