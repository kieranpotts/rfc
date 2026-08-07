# Supersede RFC

Handles the `IMPLEMENTED` → `SUPERSEDED` transition.

Retires an implemented RFC once a later implemented RFC has replaced its
decision. Cross-references the two documents by their index numbers, sets the
old RFC's status to `SUPERSEDED`, updates its row in the index, and relabels
its original pull request.

Both RFCs are already merged, so the change is committed directly to `main`
rather than through a pull request. The superseded document itself is never
deleted or rewritten.

## Interactivity

Interactive. The agent may prompt for either RFC when the pair cannot be
inferred from what the user said. Once both are identified, the change is
applied without further prompting.

## How to invoke

> Supersede RFC

> Supersede this RFC

> This RFC is replaced by the temporal data model RFC

> Event sourcing for audit log is superseded by temporal data model

## Recommended models

A fast, cheap model is sufficient for this skill. Identifying the two RFCs and
editing four fields is mechanical work.

## Related skills

- [**complete-rfc**](../complete-rfc/) \
  Puts an RFC into the `IMPLEMENTED` state that this skill retires it from,
  and assigns the index numbers the supersession is expressed in.

- [**draft-rfc**](../draft-rfc/) \
  Starts the successor RFC. A successor has to go the whole way through the
  lifecycle before it can supersede anything.

## References

- [Contributing guidelines](../../../CONTRIBUTING.md) \
  The RFC lifecycle, the permitted state transitions, and the workflow this
  skill implements the final step of.

- [RFC index](../../../rfc/INDEX.md) \
  The numbered catalog whose row this skill flips to `SUPERSEDED`.
