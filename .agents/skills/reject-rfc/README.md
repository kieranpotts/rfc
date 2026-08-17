# Reject RFC

Handles the `PROPOSED` → `REJECTED` transition.

Records the rejection in the RFC document, swaps the pull request's lifecycle
label to `#rejected`, merges the document into `latest/main` as a permanent
record of the decision, closes the discussion thread, and assigns the RFC its
number in the index.

The agent is told never to delete a rejected RFC. The archive keeps every
decision, including the ones that went the other way, so the same ground is
not needlessly covered again later.

## Interactivity

Interactive. The agent may prompt the user to choose which RFC to reject, and
it must obtain the user's explicit confirmation twice: once that the decision
really is to reject, and again before the pull request is merged. It is not
suitable for unattended use.

## How to invoke

> Reject RFC

> Reject this RFC

> The RFC was not accepted

> The RFC was not approved

> Reject event sourcing for audit log

## Recommended models

A mid-tier model is sufficient for this skill. The steps are procedural, but
holding the confirmation gate in front of them requires a bit more effort.

## Related skills

- [**propose-rfc**](../propose-rfc/) \
  Opens the review period that this skill closes against the RFC.

- [**accept-rfc**](../accept-rfc/) \
  The other outcome of the same review period, for a proposal that is taken
  forward.

- [**draft-rfc**](../draft-rfc/) \
  The way back in. A rejected decision is revisited by drafting a fresh RFC,
  never by editing the rejected one.

## References

- [Contributing guidelines](../../../CONTRIBUTING.md) \
  The RFC lifecycle, the permitted state transitions, and the workflow this
  skill implements a step of.
