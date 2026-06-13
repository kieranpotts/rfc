# `/accept-rfc`

Transitions an RFC from `PROPOSED` to `ACCEPTED`. The PR stays open until the decision is implemented.

## What it does

- Verifies the approval gates.
- Sets `Status` to `ACCEPTED`.
- Adds approvers and approval date.
- Swaps the PR label to `#accepted`.
- Keeps the PR open during implementation. The discussion thread stays open too, and is closed when the PR is merged.

## How to invoke

```
/accept-rfc
```

The agent will infer the target RFC from the current checked-out branch. If you are on `main`, the agent will prompt you, providing a list of open PRs with the `#proposed` label from which you can select the target PR you want to progress to `ACCEPTED`.

Alternatively, provide a short description of the RFC, from which the agent will try to infer the correct target

```
/accept-rfc event sourcing for audit log
```
