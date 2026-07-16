# Accept RFC

Transitions an RFC from `PROPOSED` to `ACCEPTED`. The PR stays open until the
decision is implemented.

## What it does

- Verifies the approval gates.
- Sets `Status` to `ACCEPTED`.
- Adds approvers and approval date.
- Swaps the PR label to `#accepted`.
- Keeps the PR open during implementation. The discussion thread stays open too,
  and is closed when the PR is merged.

## How to invoke

> Accept RFC

> Accept the RFC for using event sourcing for the audit log
