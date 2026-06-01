# Reject RFC

Rejects a proposed RFC, preserving the decision permanently.

## What it does

Confirms the decision to reject, verifies the document is a complete record, assigns the sequential ID, sets `Status: REJECTED`, swaps the PR label to `#rejected`, and prepares the PR for merge. The rejected RFC is kept permanently in `rfcs/` as the record — nothing is reverted, because the archive holds no current state for a rejected RFC to have changed.

## How to invoke

```
/reject-rfc
```

Optionally name the RFC:

```
/reject-rfc graphql-gateway
```

## Examples

- `/reject-rfc`: Confirms the decision, then prepares the named or current RFC for merge as a rejected record.

- `/reject-rfc graphql-gateway`: Rejects the named RFC.
