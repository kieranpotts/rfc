# Complete RFC

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

> Complete RFC

> Event sourcing for audit log has been implemented.

## Recommended models

A fast or mid-tier model is enough. Verifying the implementation gates —
whether the tooling and infrastructure exist — is a factual check, not a
judgment call.
