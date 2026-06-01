# Advance RFC

Transitions an RFC to the next permitted lifecycle state, verifying the gates first.

## What it does

Confirms the requested transition is permitted, runs `audit-rfc` to verify the gates, assigns a sequential ID on acceptance, updates the document's `Status` and `Last updated` fields, applies the matching GitHub label, regenerates the index, and commits.

## How to invoke

```
/advance-rfc
```

Optionally name the RFC and/or the target state:

```
/advance-rfc 0003-adopt-pnpm accepted
```

## Examples

- `/advance-rfc`: Determines the current state and advances to the next permitted one after gate checks.

- `/advance-rfc event-sourcing-for-audit-log superseded`: Marks an accepted RFC as superseded once a later RFC has replaced it.

For the rejection path, use [`reject-rfc`](../reject-rfc/README.md) instead.
