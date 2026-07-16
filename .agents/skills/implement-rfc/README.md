# Implement RFC

Transitions an RFC from `ACCEPTED` to `IMPLEMENTED`, then squash-merges the PR
and assigns its index number.

## What it does

- Verifies the implementation gates — the tooling and infrastructure the
  decision calls for are actually in place.
- Sets `Status` to `IMPLEMENTED`.
- Swaps the PR label to `#implemented`.
- Merges the PR using the squash-merge strategy.
- Closes the discussion thread.
- Assigns the RFC the next sequential number, logs it in `rfc/INDEX.md` on
  `main`.

## How to invoke

> Implement RFC

> Event sourcing for audit log has been implemented.
