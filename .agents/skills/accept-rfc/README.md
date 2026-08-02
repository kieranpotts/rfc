# Accept RFC

Handles the `PROPOSED` → `ACCEPTED` transition.

Checks the approval gates and marks the RFC accepted, leaving the pull
request open until the decision is implemented.

## How to invoke

> Accept RFC

> Accept the RFC for using event sourcing for the audit log

## Recommended models

A mid-tier model is sufficient for this skill. The state transition is
procedural, but judging whether the points of contention are resolved requires
a bit more effort.
