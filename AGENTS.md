# [Project Name] — Requests for Comments (RFCs)

## Project overview

This repository holds the Requests for Comments (RFC) archive for [Project Name]. This is the permanent, chronological record of the project's significant _technical_ decisions: its architecture, its development and operations processes, and its choices of technologies and tools.

Each RFC captures one technical decision: its motivation, the chosen solution, the alternatives considered, and the trade-offs.

It is documentation, not code. There is nothing to build, lint, or run.

Product requirements (what the system does, in business terms) are recorded separately. This repository is concerned only with technical decisions (how the system is built and operated).

## Repository structure

- `rfc/`: The permanent, append-only archive of every RFC, including rejected ones. Each RFC is a directory (`rfc/<category>/<slug>/`) with a `README.md` file being the entry point. Supporting artifacts such as architectural diagrams may be included in the same directory or stored separately, but every artifact MUST be referenced from the `README.md` — if it is not referenced there, it is not part of the RFC.
  - `rfc/INDEX.md` is the numbered catalog of accepted, rejected, and superseded RFCs.
  - `rfc/TEMPLATE.md` is the starting point for a new RFC.
- `docs/`: General guidelines for humans to get the most out of the RFC process.

## RFC lifecycle

Each RFC moves through a defined state machine:

- `DRAFT`: The RFC is being written. The pull request is in draft status, ie. not yet ready for review.
- `PROPOSED`: The RFC is complete and open for a decision. The pull request is marked ready for review and labeled `#proposed`.
- `ACCEPTED`: The RFC is accepted. Final comments have been solicited, so the discussion thread is closed. The RFC artifacts are merged into `main`, and the RFC is recorded in `rfc/INDEX.md` and given the next sequential number to identify it. An accepted decision stays in effect until a later RFC supersedes it.
- `REJECTED`: The RFC is not being taken forward. The document is merged into `main` and its number recorded in `rfc/INDEX.md`, preserved permanently as the record of the decision and its rationale.
- `SUPERSEDED`: The RFC was previously accepted but has been replaced by a later RFC. This is the only state reachable after ACCEPTED.

The authors of an RFC drive its lifecycle. Each state transition has a corresponding agent skill (see below), which the authors can use to automate recurring steps in RFC management. The possible state transitions are:

- (New RFC) → DRAFT
- DRAFT → PROPOSED
- PROPOSED → ACCEPTED
- PROPOSED → REJECTED
- ACCEPTED → SUPERSEDED

## Rules

- Write in American English.

- An RFC is for a _significant_ technical decision, one that affects multiple stakeholders and is worth building consensus on before implementation. Routine feature work, bug fixes, and trivial changes go through the normal pull-request workflow on the relevant repository, not an RFC.

- An RFC MUST be a single, atomic technical decision. Author it on an `rfc/<slug>` branch cut from `main`, and open a pull request titled `rfc: <short lowercase description>`.

- If a body of work spans several independent decisions, open one RFC per decision and link them as related.

- Transitions not listed above are NOT permitted. A decision MUST NOT move backwards or skip states.

- When a pull request is opened, it MUST be labeled with exactly one category — `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING` — matching the kind of decision.

- Every RFC pull request MUST have an associated discussion thread, opened when the PR is opened (even as a draft). The discussion thread is the forum for all review feedback, keeping the PR's own comment thread focused on edits to the RFC artifacts. The thread is closed when the RFC is accepted or rejected.

- The current lifecycle state of an RFC is tracked via a lifecycle label on the PR. Apply the matching label — `#proposed`, `#accepted`, `#rejected`, `#superseded` — as the RFC advances.

- A pull request MUST be opened initially as a draft. The author marks the PR ready for review, and applies the `#proposed` label, once it is ready for stakeholder review.

- An RFC MUST NOT be merged into `main` until it has been decided — either accepted or rejected.

- RFC branches MUST be squash-merged to `main`, and the squash commit message MUST take the form `rfc: <short lowercase description> - ACCEPTED|REJECTED`. The description is the prose title of the RFC, not the branch slug (eg. `rfc: event sourcing for audit log - ACCEPTED`). A sequential RFC number is assigned after merge, recorded in `rfc/INDEX.md` (the number lives only in the index).

- Once an RFC's `Status` is `ACCEPTED` or `REJECTED`, its document is immutable. Only its `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers may change thereafter.

- An accepted RFC may only be superseded by another RFC. To change the _substance_ of a past decision, open a new RFC that supersedes it — do NOT edit the original.

- Never delete an RFC document, including rejected ones.

- The GitHub issue tracker is used only for maintenance work on this repository itself (via the `MAINTENANCE` template). RFCs are proposed, decided, and archived entirely through pull requests.

## Skills

The [`.agents/skills/`](.agents/skills/) directory provides on-demand skills for managing the RFC workflow. There's one agent skill per RFC state transition. Each skill carries the gate rules for its own discrete transition.

- [`draft-rfc`](.agents/skills/draft-rfc/SKILL.md): Scaffolds a new RFC, opens it as a draft PR, and opens a linked discussion thread.
- [`propose-rfc`](.agents/skills/propose-rfc/SKILL.md): Verifies and handles the `DRAFT` → `PROPOSED` transition.
- [`accept-rfc`](.agents/skills/accept-rfc/SKILL.md): Verifies and handles the `PROPOSED` → `ACCEPTED` transition. Also closes the discussion thread.
- [`reject-rfc`](.agents/skills/reject-rfc/SKILL.md): Verifies and handles the `PROPOSED` → `REJECTED` transition. Also closes the discussion thread.
- [`supersede-rfc`](.agents/skills/supersede-rfc/SKILL.md): Verifies and handles the `ACCEPTED` → `SUPERSEDED` transition for an old RFC.
