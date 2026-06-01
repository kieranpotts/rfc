# Approve RFC

Approves a proposed RFC: assigns its sequential ID, sets its status to accepted, and prepares it for merge.

## What it does

Verifies the approval gates, assigns the next zero-padded sequential ID (renaming the file to `NNNN-<slug>.md`), sets `Status: ACCEPTED` with approvers and approval date, swaps the PR label to `#accepted`, and prepares it for merge.

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
