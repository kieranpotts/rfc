# RFCs

This directory is the permanent archive of every major technical decision proposed for this project.

Every significant technical decision is introduced through an RFC, and every RFC is kept here permanently — including those that were ultimately rejected. Rejected RFCs are not deleted. They remain as a record of the decision and the rationale behind it, so that the same ground is not needlessly re-trodden later.

## How it works

1. An RFC is opened as a pull request. The proposal is written in a single Markdown file in the `rfcs/` directory, based on [`TEMPLATE.md`](./TEMPLATE.md), and committed to an `rfc/[description]` branch. A GitHub issue (labelled `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`) MAY be opened first for lightweight early triage. If so, the proposer closes it when the PR is opened.

2. The RFC moves through its lifecycle: `draft → proposed → accepted | rejected → superseded`.

3. On merge, the project maintainers assign the RFC a sequential, zero-padded ID and rename its file to `NNNN-[description].md`, eg. `0002-event-sourcing-for-audit-log.md`.

4. Once an RFC is `#accepted` or `#rejected`, its document is immutable. Only its `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers may change thereafter — an accepted RFC moves to `#superseded` when a later RFC replaces it. To revisit a decision, open a new RFC that supersedes the original, and cross-reference the two using the `Supersedes` / `Superseded by` fields in the template.

See the [contributing guide](../CONTRIBUTING.md) for the full process.
