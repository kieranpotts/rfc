# Reject RFC

Handles the rejection path for an RFC, preserving the decision permanently.

## What it does

Confirms the decision to reject, runs a pre-rejection audit, assigns the sequential ID, sets the document `Status` to `REJECTED`, applies the `#rejected` label, regenerates the index, and prepares the PR for merge. The rejected RFC is kept permanently in `rfcs/` as the record — nothing is reverted, because the archive holds no current state for a rejected RFC to have changed.

## How to invoke

```
/reject-rfc
```

Optionally name the RFC:

```
/reject-rfc event-sourcing-for-audit-log
```

## Examples

- `/reject-rfc`: Confirms the decision, then prepares the named or most-recently-modified RFC for merge as a rejected record.

- `/reject-rfc 0004-graphql-gateway`: Rejects the named RFC.
