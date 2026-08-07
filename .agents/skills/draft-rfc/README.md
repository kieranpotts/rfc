# Draft RFC

Scaffolds a new RFC, ready for the user to write up.

Cuts an `rfc/<slug>` branch from `main`, prepares a fresh RFC document from
the template, opens a draft pull request with its category label, and opens
the discussion thread where review feedback will be gathered. The RFC's
status is set to `DRAFT`.

The agent is told not to write the proposal's prose sections. That work
belongs to the author.

## Interactivity

Interactive. The agent may prompt for a description of the decision if none
can be found in the surrounding context, and for the RFC's category where the
description does not make the fit obvious. It is not suitable for unattended
or away-from-keyboard use.

## How to invoke

> Draft RFC

> New RFC

> Start an RFC

> We will adopt event sourcing for our audit log architecture - draft an RFC.

## Recommended models

A mid-tier model with strong prose output is best suited to this skill. The
scaffolding is mechanical, but naming the decision and picking its category
requires a bit more effort.

## Related skills

- [**propose-rfc**](../propose-rfc/) \
  Picks up where this skill stops, once the author has written the proposal:
  it checks the document for completeness and takes the pull request out of
  draft for stakeholder review.

## References

- [Contributing guidelines](../../../CONTRIBUTING.md) \
  The RFC lifecycle, the permitted state transitions, and the workflow this
  skill implements the first step of.

- [RFC template](../../../rfc/TEMPLATE.md) \
  The document this skill copies to create a new RFC.
