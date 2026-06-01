# RFCs

This directory is the permanent archive of every major technical decision proposed for this project — accepted and rejected alike. Nothing here is ever deleted; rejected RFCs remain as a record of the decision and its rationale, so the same ground is not needlessly re-trodden later.

## Layout

Each RFC is a directory, grouped by category:

```
rfc/
├── INDEX.md          # the catalogue of every RFC, with its number
├── TEMPLATE.md       # the starting point for a new RFC
├── architecture/
├── process/
├── technology/
└── tooling/
    └── <slug>/
        ├── README.md # the RFC document
        └── …         # diagrams or other supporting artifacts
```

An RFC's directory holds its `README.md` (the proposal itself, copied from [`TEMPLATE.md`](./TEMPLATE.md)) plus any supporting artifacts — diagrams, data, prototypes.

## How it works

1. An RFC is opened as a draft pull request, on an `rfc/[slug]` branch, with its document at `rfc/<category>/<slug>/README.md`. The PR carries exactly one category label (`ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`) and an associated discussion thread for all review feedback. (The issue tracker is not used for RFCs; it is reserved for repository maintenance.)

2. The RFC moves through its lifecycle: `draft → proposed → accepted | rejected → superseded`.

3. On merge, the maintainers assign the RFC a sequential, zero-padded number and record it in [`INDEX.md`](./INDEX.md). The number appears only in the index — no file is ever renamed.

4. Once accepted or rejected, the document is immutable. Only its `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers may change thereafter; an accepted RFC moves to superseded when a later RFC replaces it. To revisit a decision, open a new RFC that supersedes the original, cross-referencing the two via the `Supersedes` / `Superseded by` fields.

See the [contributing guide](../CONTRIBUTING.md) for the full process, and the [skills](../.agents/skills/) that automate it.
