# Propose RFC

Removes the draft status from an RFC pull request, making it ready for stakeholder review.

## What it does

- Acts as an audit gate by verifying the RFC document is complete and free of template boilerplate.
- Bumps `Last updated` date.
- Applies the `#proposed` label.
- Takes the PR out of draft (`gh pr ready`).

## How to invoke

```
/propose-rfc
```

The agent will infer the target RFC from the current checked-out branch. If you are on `main`, the agent will prompt you, providing you with a list of open draft RFCs that can be progressed to `PROPOSED`.
