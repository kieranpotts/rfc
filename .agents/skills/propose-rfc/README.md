# Propose RFC

Removes the draft status from an RFC pull request, marking it ready for stakeholder review.

## What it does

Verifies the document is complete and free of template boilerplate, sets `Last updated`, applies the `#proposed` label, and takes the PR out of draft (`gh pr ready`).

## How to invoke

```
/propose-rfc
```

Optionally name the RFC:

```
/propose-rfc event-sourcing-for-audit-log
```

## Examples

- `/propose-rfc`: Checks the current RFC's completeness, then marks its PR ready for review.

- `/propose-rfc event-sourcing-for-audit-log`: Proposes the named RFC.
