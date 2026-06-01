# Audit RFC

Checks an RFC document for completeness, consistency, and process compliance before it advances.

## What it does

Verifies that the metadata header is complete, the GitHub label matches the document `Status`, the required prose sections contain real content, cross-references resolve to existing RFCs, and the PR carries exactly one category label. It reports passes and failures/warnings, but it makes no changes itself.

## How to invoke

```
/audit-rfc
```

Optionally name the RFC:

```
/audit-rfc event-sourcing-for-audit-log
```

## Examples

- `/audit-rfc`: Audits the most recently modified RFC and reports findings.

- `/audit-rfc 0003-adopt-pnpm`: Audits the named RFC before it is advanced.
