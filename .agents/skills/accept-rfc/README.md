# Accept RFC

Transitions an RFC from `PROPOSED` to `ACCEPTED` and prepares it for merge.

## What it does

- Verifies the approval gates.
- Sets `Status` to `ACCEPTED`.
- Add approvers and approval date.
- Swaps the PR label to `#accepted`.
- Closes the discussion thread.
- Merges the PR using the squash-merge strategy.
- Assigns the RFC the next sequential number, logs it in `rfc/INDEX.md`.

## How to invoke

```
/accept-rfc
```

The agent will infer the target RFC from the current checked-out branch. If you are on `main`, the agent will prompt you, providing a list of open PRs with the `#proposed` label from which you can select the target PR you want to progress to `ACCEPTED`.

Alternatively, provide a short description of the RFC, from which the agent will try to infer the correct target

```
/accept-rfc event sourcing for audit log
```
