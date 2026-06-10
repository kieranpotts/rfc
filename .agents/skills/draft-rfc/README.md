# Draft RFC

Scaffolds a new RFC, ready for the author to complete.

## What it does

- Creates an `rfc/<slug>` branch from `main`.
- Copies `rfc/TEMPLATE.md` to `rfc/<category>/<slug>/README.md`.
- Fills in the metadata header (authors, dates, `Status: DRAFT`).
- Commits and pushes the change.
- Opens a draft pull request.
- Applies a category label to the PR, eg, `TOOLING`.
- Opens a discussion thread.
- Creates cross-references between the discussion and the PR.

## How to invoke

```
/draft-rfc
```

Optionally, describe the RFC:

```
/draft-rfc We will adopt event-sourcing for our audit log architecture
```

## Examples

- `/draft-rfc`: The agent will prompt you for details of the RFC, then it will scaffold the branch, the RFC document, and create a draft PR.

- `/draft-rfc <Description>`: Provide more information about the RFC, from which the agent will attempt to infer details such as title, slug,and category (eg. "architecture").

You will need to complete the RFC document yourself. Once you've done that, use [`propose-rfc`](../propose-rfc/README.md) to mark the PR as "ready for review".
