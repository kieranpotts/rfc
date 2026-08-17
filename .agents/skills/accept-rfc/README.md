# Accept RFC

Handles the `PROPOSED` → `ACCEPTED` transition.

Checks the approval gates, records the decision and its date in the RFC
document, and swaps the pull request's lifecycle label to `#accepted`. The
pull request is left open until the decision has been implemented.

The agent is told not to merge the pull request or assign the RFC a number.
Both wait for implementation.

## Interactivity

Interactive. The agent may prompt the user to choose which RFC to accept,
when the target cannot be inferred from the checked-out branch or from what
the user said.

## How to invoke

> Accept RFC

> Accept this RFC

> Approve this RFC

> Mark this RFC as accepted

> Accept the RFC for using event sourcing for the audit log

## Recommended models

A mid-tier model is sufficient for this skill. The state transition is
procedural, but judging whether the points of contention are resolved
requires a bit more effort.

## Related skills

- [**propose-rfc**](../propose-rfc/) \
  Opens the review period that this skill closes in the RFC's favor.

- [**reject-rfc**](../reject-rfc/) \
  The other outcome of the same review period, for a proposal that is not
  taken forward.

- [**complete-rfc**](../complete-rfc/) \
  Picks the RFC up once the tooling and infrastructure the decision calls for
  are in place, and lands it in `latest/main`.

## References

- [Contributing guidelines](../../../CONTRIBUTING.md) \
  The RFC lifecycle, the permitted state transitions, and the workflow this
  skill implements a step of.
