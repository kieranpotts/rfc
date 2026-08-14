# [Project Name] – Requests for Comments (RFCs)

The capitalized words REQUIRED, MUST, MUST NOT, RECOMMENDED, SHOULD,
SHOULD NOT, OPTIONAL, and MAY are to be interpreted as described in
[IETF RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## Project overview

See the [README](./README.md) for an overview of this project, and how it fits
alongside the sibling SRS, design, plans, audits, and risks repositories.

This repository is documentation, not code. There is nothing to build, lint,
or run.

## Project structure

- `rfc/`. The permanent, append-only archive of every RFC, including
  rejected ones. Each RFC is a directory (`rfc/<category>/<slug>/`) with a
  `README.md` file being the entry point.

  - `rfc/INDEX.md` is the numbered catalog of implemented, rejected, and
    superseded RFCs.

  - `rfc/TEMPLATE.md` is the starting point for a new RFC.

- `docs/`. General guidelines for humans to get the most out of the RFC
  process.

## Lifecycle

See [CONTRIBUTING.md > Lifecycle](./CONTRIBUTING.md#lifecycle) for the state
machine and the table of permitted transitions.

## Workflow

See [CONTRIBUTING.md > Workflow](./CONTRIBUTING.md#workflow) for the
step-by-step process for shepherding an RFC from `DRAFT` to
`IMPLEMENTED`/`REJECTED`.

## Rules

Agents MUST follow the rules in [CONTRIBUTING.md > Rules](./CONTRIBUTING.md#rules).
Re-read the rules before creating, transitioning, or merging an RFC, rather
than relying on your memory of a prior state of the rules.

## Skills

The `.agents/skills/` directory provides on-demand skills for managing the
lifecycle of an RFC. See the [README](./.agents/skills/README.md) for
descriptions of the available skills and their triggers.

It is RECOMMENDED to use these skills to drive state transitions.

## References

The following technical standards (TS) govern this project. Fetch and ingest
the relevant standards as-and-when required for the task at hand.

- [**TS-3: Design Docs**](https://kieranpotts.com/standards/003) \
  Use when writing, reviewing, or maintaining design docs, RFCs, architecture
  decision records (ADRs), or architecture audit reports.

- [**TS-25: Technical Documentation**](https://kieranpotts.com/standards/025) \
  Use when deciding what documentation a project needs, where it should live,
  who it's for, or whether it's still trustworthy.

- [**TS-26: Technical Writing Style Guide**](https://kieranpotts.com/standards/026) \
  Use when writing or editing the prose of a technical document. Covers
  tone-of-voice, headings, terminology, lists, and citations.

- [**TS-9: Version Control**](https://kieranpotts.com/standards/009) \
  Use when working with Git. Covers commits, branching, merging, integration
  strategies, cutting releases, and configuring Git/PR/CI tooling.
