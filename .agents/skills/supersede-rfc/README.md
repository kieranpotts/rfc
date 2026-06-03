# Supersede RFC

Marks an accepted RFC as superseded by a later one.

## What it does

- Confirms that a later, currently-accepted RFC has replaced a previously-accepted decision.
- Sets the superseded RFC's `Status: SUPERSEDED`.
- Updates the `Superseded by` link.
- Verifies the successor links back via `Supersedes`.
- Swaps the lifecycle label to `#superseded`.

## How to invoke

```
/supersede-rfc
```

The agent will prompt you for the RFC that is being superseded, and it will ask you to confirm the newer RFC that replaces it.

The agent verifies that both RFCs are currently in `ACCEPTED` state, and that the second RFC is newer.

Alternatively, provide a short description, from which the agent will try to infer the target:

```
/supersede-rfc event sourcing for audit log is superseded by temporal data model
```
