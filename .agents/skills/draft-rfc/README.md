# Draft RFC

Scaffolds a new RFC and opens it as a draft pull request, ready for the author to complete.

## What it does

Creates an `rfc/<slug>` branch from `main`, copies `rfcs/TEMPLATE.md` to `rfcs/<slug>.md`, fills in the metadata header (authors, dates, `Status: PROPOSED`), opens a draft pull request, and applies the category label.

## How to invoke

```
/draft-rfc
```

Optionally include the slug and category upfront:

```
/draft-rfc event-sourcing-for-audit-log architecture
```

## Examples

- `/draft-rfc`: Agent asks for the slug and category, then scaffolds the branch, document, and draft PR.

- `/draft-rfc trunk-based-branching process`: Scaffolds a PROCESS RFC with the given slug.

- `/draft-rfc adopt-pnpm tooling`: Scaffolds a TOOLING RFC.

Once the document is complete, use [`propose-rfc`](../propose-rfc/README.md) to mark the PR ready for review.
