# Skills

This repository ships a small set of [agent skills](https://agentskills.io/) — invoked as slash commands through agentic tools such as Claude Code — that automate the RFC workflow.

There is one skill per RFC state transition: `DRAFT` → `PROPOSED` → `ACCEPTED` | `REJECTED`, and `ACCEPTED` → `SUPERSEDED`. Each skill knows the gate rules for its own transition and will not proceed until they are met, which keeps the process consistent whether a human or an agent is driving it.

The skills are, in lifecycle order:

- **[`/draft-rfc`](./draft-rfc/)**: Starts a new RFC as as `DRAFT` — scaffolds the branch and document from the template, opens a draft pull request with one category label applied, and opens the associated discussion thread — ready for you to complete.

- **[`/propose-rfc`](./propose-rfc/)**: `DRAFT` → `PROPOSED` — confirms the RFC document is complete and free of leftover template text, sets `Status` to `PROPOSED`, applies the `#proposed` label, and takes the pull request out of draft so stakeholders can review it.

- **[`/accept-rfc`](./accept-rfc/)**: `PROPOSED` → `ACCEPTED` — verifies the approval gates, sets the document's `Status` to `ACCEPTED`, labels the pull request `#accepted`, closes the discussion thread, and squash-merges it (on your confirmation). The RFC's number is recorded in `INDEX.md` on `main` after the merge.

- **[`/reject-rfc`](./reject-rfc/)**: `PROPOSED` → `REJECTED` — records the rejection: sets the document's `Status` to `REJECTED`, labels the pull request `#rejected`, closes the discussion thread, and squash-merges it (on your confirmation) as a permanent record. The number is recorded in `INDEX.md` on `main` after the merge.

- **[`/supersede-rfc`](./supersede-rfc/)**: `ACCEPTED` → `SUPERSEDED` — marks an accepted RFC as replaced by a newer (currently `ACCEPTED`) one, and sets up cross-references between the two.

A typical journey runs `/draft-rfc` → you write the proposal → `/propose-rfc` → stakeholder review → `/accept-rfc` or `/reject-rfc`. Much later, `/supersede-rfc` retires a decision that a newer RFC has replaced.
