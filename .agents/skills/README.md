# Agent skills

This repository ships a small set of [agent skills](https://agentskills.io/) — invoked as slash commands through agentic tools such as Claude Code — that automate the RFC workflow.

There is one skill per RFC state transition: `DRAFT` → `PROPOSED` → `ACCEPTED` → `IMPLEMENTED`, plus `PROPOSED` → `REJECTED` and `IMPLEMENTED` → `SUPERSEDED`. Each skill knows the gate rules for its own transition and will not proceed until they are met, which keeps the process consistent whether a human or an agent is driving it.

The skills are, in lifecycle order:

- **[`/draft-rfc`](./draft-rfc/)**: Scaffolds a new RFC, ready for the user to complete. Opens a draft PR, and opens a linked discussion thread.

- **[`/propose-rfc`](./propose-rfc/)**: `DRAFT` → `PROPOSED` — Confirms the RFC document is complete and free of leftover template text. Sets the document's `Status` to `PROPOSED`, applies the `#proposed` label to the PR, and takes the pull request out of draft, ready for stakeholder review.

- **[`/accept-rfc`](./accept-rfc/)**: `PROPOSED` → `ACCEPTED` — Verifies the approval gates, sets the document's `Status` to `ACCEPTED`, labels the pull request `#accepted`, and closes the discussion thread. The pull request stays open through implementation – it is not merged here.

- **[`/implement-rfc`](./implement-rfc/)**: `ACCEPTED` → `IMPLEMENTED` — Sets the document's `Status` to `IMPLEMENTED`, labels the pull request `#implemented`, and squash-merges it to `main`. After the merge, the RFC is given a unique reference number and listed in the RFC index.

- **[`/reject-rfc`](./reject-rfc/)**: `PROPOSED` → `REJECTED` — Records the rejection, sets the document's `Status` to `REJECTED`, labels the pull request `#rejected`, closes the discussion thread, and squash-merges it to `main`. After the merge, the RFC is given a unique reference number and listed in the RFC index.

- **[`/supersede-rfc`](./supersede-rfc/)**: `IMPLEMENTED` → `SUPERSEDED` — Marks an implemented RFC as replaced by a newer one. Sets up cross-references between the two.

A typical journey runs `/draft-rfc` → the user writes the proposal → `/propose-rfc` → stakeholder review → `/accept-rfc` (or `/reject-rfc` if the decision is not to proceed) → implementation → `/implement-rfc`. Much later, `/supersede-rfc` retires a decision that a newer RFC has replaced.
