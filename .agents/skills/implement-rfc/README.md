# Implement RFC

Transitions an RFC from `ACCEPTED` to `IMPLEMENTED`, then squash-merges the PR and assigns its index number.

## What it does

- Verifies the implementation gates — the tooling and infrastructure the decision calls for are actually in place.
- Sets `Status` to `IMPLEMENTED`.
- Swaps the PR label to `#implemented`.
- Merges the PR using the squash-merge strategy.
- Assigns the RFC the next sequential number, logs it in `rfc/INDEX.md` on `main`.

## How to invoke

```
/implement-rfc
```

The agent will infer the target RFC from the current checked-out branch. If you are on `main`, the agent will prompt you, providing a list of open PRs with the `#accepted` label from which you can select the target PR you want to progress to `IMPLEMENTED`.

Alternatively, provide a short description of the RFC, from which the agent will try to infer the correct target:

```
/implement-rfc event sourcing for audit log
```
