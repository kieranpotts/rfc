# Propose RFC

Handles the `DRAFT` → `PROPOSED` transition.

Checks the RFC document is complete, sets its status to `PROPOSED`, applies
the `#proposed` label, and takes the pull request out of draft so that
technical stakeholders can review it.

The agent is told not to decide the RFC. Proposing invites a decision; it
does not take one.

## Interactivity

Interactive. The agent may prompt the user to choose which RFC to propose,
when the target cannot be inferred from the checked-out branch. Once the
target is known, the readiness gate is applied without further prompting.

## How to invoke

> Propose RFC

> Propose this RFC

> Take this RFC out of draft

> Mark the RFC as ready

> Progress this RFC to the next stage

> This RFC is ready for stakeholder review.

## Recommended models

A mid-tier model is sufficient for this skill. It applies a readiness gate to
a concrete case, and decides nothing about the RFC's merits.

## Related skills

- [**draft-rfc**](../draft-rfc/) \
  Scaffolds the RFC, its pull request, and its discussion thread. This skill
  is what picks the RFC up once its author has finished writing it.

- [**accept-rfc**](../accept-rfc/) \
  Takes the RFC forward once stakeholder review has concluded in its favor.

- [**reject-rfc**](../reject-rfc/) \
  Takes the RFC out of the lifecycle if stakeholder review concludes against
  it.

## References

- [Contributing guidelines](../../../CONTRIBUTING.md) \
  The RFC lifecycle, the permitted state transitions, and the workflow this
  skill implements a step of.
