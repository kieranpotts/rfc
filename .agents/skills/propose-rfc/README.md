# Propose RFC

Removes the draft status from an RFC pull request, marking it ready for stakeholder review.

## What it does

Acts as an audit gate by verifying the RFC document is complete and free of template boilerplate. It also bumps `Last updated`, applies the `#proposed` label, and takes the PR out of draft (`gh pr ready`).

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
