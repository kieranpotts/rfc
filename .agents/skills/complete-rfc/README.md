# Complete RFC

Handles the `ACCEPTED` → `IMPLEMENTED` transition.

Checks that the tooling and infrastructure the decision calls for are in
place, sets the RFC's status to `IMPLEMENTED`, swaps the pull request's
lifecycle label, merges the document into the `main` trunk, closes the
discussion thread, and assigns the RFC its number in the index.

The agent is told not to do the implementation work. That is delivered in the
code and infrastructure repositories, tracked by the issues linked from the
RFC's `Implementation trackers` section.

## Interactivity

Interactive. The agent may prompt the user to choose which RFC to complete,
and it must obtain explicit confirmation before merging the pull request. It
is not suitable for unattended use.

## How to invoke

> Complete RFC

> Implement this RFC

> Implement RFC

> This RFC is implemented

> The tooling is in place

> The infrastructure is built

> Event sourcing for audit log has been implemented.

## Recommended models

A mid-tier model is sufficient for this skill. The state transition is
procedural, but confirming the decision was actually carried out requires a
bit more effort.

## Related skills

- [**accept-rfc**](../accept-rfc/) \
  Settles the decision and opens the implementation phase that this skill
  closes.

- [**supersede-rfc**](../supersede-rfc/) \
  Retires an implemented RFC once a later implemented RFC replaces its
  decision.

## References

- [Contributing guidelines](../../../CONTRIBUTING.md) \
  The RFC lifecycle, the permitted state transitions, and the workflow this
  skill implements a step of.

- [RFC index](../../../rfc/INDEX.md) \
  The numbered catalog this skill appends to once the RFC has merged.
