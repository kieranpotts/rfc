# Supersede RFC

Marks an accepted RFC as superseded by a later one.

## What it does

Confirms a later, accepted RFC has replaced the decision, sets the superseded RFC's `Status: SUPERSEDED` and `Superseded by` link, verifies the successor links back via `Supersedes`, and swaps the lifecycle label to `#superseded`.

## How to invoke

```
/supersede-rfc
```

Name the superseded RFC and (optionally) its successor:

```
/supersede-rfc event-sourcing-for-audit-log kafka-event-log
```

## Examples

- `/supersede-rfc event-sourcing-for-audit-log kafka-event-log`: Marks the event-sourcing RFC as superseded by the kafka-event-log RFC.
