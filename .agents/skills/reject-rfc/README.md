# Reject RFC

Rejects a proposed RFC, preserving the decision permanently.

## What it does

- Verifies the document is a complete record.
- Sets `Status: REJECTED`.
- Swaps the PR label to `#rejected`.
- Closes the discussion thread.
- Merges the PR using the squash-merge strategy.
- After the merge, assigns the next sequential number in `rfc/INDEX.md` on `main`.

## How to invoke

```
/reject-rfc
```

The agent will infer the target RFC from the current checked-out branch. If you are on `main`, the agent will prompt you, providing a list of open PRs with the `#proposed` label from which you can select your target.

Alternatively, provide a short description of the RFC, from which the agent will try to infer the correct target

```
/reject-rfc event sourcing for audit log
```

