# Reject RFC

Rejects a proposed RFC, preserving the decision permanently.

## What it does

- Verifies the document is a complete record.
- Sets `Status: REJECTED`.
- Swaps the PR label to `#rejected`.
- Closes the discussion thread.
- Merges the PR using the squash-merge strategy.
- After the merge, assigns the next sequential number in `rfc/INDEX.md` on
  `main`.

## How to invoke

> Reject RFC

> Reject event sourcing for audit log
