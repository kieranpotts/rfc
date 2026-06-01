# [Project Name] — Requests for Comments (RFCs)

## Project overview

This repository holds the Requests for Comments (RFC) archive for [Project Name]: the permanent, chronological record of the project's significant _technical_ decisions — its architecture, its development and operations processes, and its technology choices.

It is documentation, not code. There is nothing to build, lint, or run.

Product requirements (what the system does, in business terms) are recorded separately. This repository is concerned only with technical decisions (how the system is built and operated). Each RFC captures one decision: its motivation, the chosen solution, the alternatives considered, and the trade-offs.

## Repository structure

- `rfcs/`: The permanent, append-only archive of every RFC, including rejected ones. `TEMPLATE.md` is the starting point for a new RFC.

## Rules

The capitalized words REQUIRED, MUST, MUST NOT, RECOMMENDED, SHOULD, SHOULD NOT, OPTIONAL, and MAY, in the context of this document and agent skills/instructions/rules, are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

- Write in American English.

- An RFC MUST be a single, atomic technical decision. Author it on an `rfc/[description]` branch cut from `main`, and open a pull request titled `rfc: [description]`. A GitHub issue (`ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`) MAY be opened first for early triage; if so, close it when the PR is opened and link the two via the `Issue` field in the RFC document.

- The default branch is `main`. An RFC is merged into `main` once it has been decided — `#accepted` or `#rejected`. A sequential ID is assigned at merge and the file is renamed to `NNNN-[slug].md`.

- The current lifecycle state of an RFC is tracked via labels on the issue and PR. Apply the matching label (`#draft`, `#proposed`, `#accepted`, `#rejected`, `#superseded`) as the RFC advances.

- Once an RFC is `#accepted` or `#rejected`, its document is immutable. Only the `Status` field and cross-references may change thereafter. An accepted RFC may only be superseded by another RFC. To change the _substance_ of a past decision, open a new RFC that supersedes it — do NOT edit the original.

- Never delete an RFC document, including rejected ones.

## Skills

The `.agents/skills/` directory provides on-demand agent skills for managing the RFC workflow.
