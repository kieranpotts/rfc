# Approve RFC

Approves a proposed RFC: records its number in the index, sets its status to accepted, and prepares it for merge.

## What it does

Verifies the approval gates, records the next zero-padded sequential number in `rfc/INDEX.md` (no file is renamed), sets `Status: ACCEPTED` with approvers and approval date, swaps the PR label to `#accepted`, closes the discussion thread, and prepares it for merge.

## How to invoke

```
/approve-rfc
```

Optionally name the RFC:

```
/approve-rfc event-sourcing-for-audit-log
```

## Examples

- `/approve-rfc`: Verifies the gates for the current proposed RFC and accepts it.

- `/approve-rfc adopt-pnpm`: Approves the named RFC.
