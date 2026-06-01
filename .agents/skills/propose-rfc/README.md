# Propose RFC

Scaffolds and proposes a new RFC for a significant technical decision.

## What it does

Creates an `rfc/<slug>` branch from `main`, copies `rfcs/TEMPLATE.md` to `rfcs/<slug>.md`, fills in the metadata header (authors, dates), and sets the status to `PROPOSED`.

## How to invoke

```
/propose-rfc
```

Optionally include the slug and category upfront:

```
/propose-rfc event-sourcing-for-audit-log architecture
```

## Examples

- `/propose-rfc`: Agent asks for the slug and category, then scaffolds the branch and document.

- `/propose-rfc trunk-based-branching process`: Scaffolds a PROCESS RFC with the given slug.

- `/propose-rfc adopt-pnpm tooling`: Scaffolds a TOOLING RFC.
