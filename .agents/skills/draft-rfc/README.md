# Draft RFC

Scaffolds a new RFC for a significant technical decision.

## What it does

Creates an `rfc/<slug>` branch from `main`, copies `rfcs/TEMPLATE.md` to `rfcs/<slug>.md`, fills in the metadata header (authors, dates, issue link), and sets the initial status.

## How to invoke

```
/draft-rfc
```

Optionally include the slug and category upfront:

```
/draft-rfc event-sourcing-for-audit-log architecture
```

## Examples

- `/draft-rfc`: Agent asks for the slug and category, then scaffolds the branch and document.

- `/draft-rfc trunk-based-branching process`: Scaffolds a PROCESS RFC with the given slug.

- `/draft-rfc adopt-pnpm tooling`: Scaffolds a TOOLING RFC.
