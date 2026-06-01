---
name: draft-rfc
description: Scaffold a new RFC and open it as a draft pull request, ready for the author to complete. Use when the user wants to start a new architecture, process, technology, or tooling decision, or says "draft an RFC", "new RFC", or "start an RFC".
license: MIT
---

# Draft RFC

Use this skill to start a new RFC: scaffold the branch and document from the template, then open a **draft pull request** with the artifacts in place, ready for the author to complete.

This is the entry point to the RFC lifecycle. The PR stays a GitHub draft while the author writes the proposal; [`propose-rfc`](../propose-rfc/SKILL.md) removes the draft status once the document is ready for review. Do NOT use this skill to advance an existing RFC — see [`propose-rfc`](../propose-rfc/SKILL.md), [`approve-rfc`](../approve-rfc/SKILL.md), [`reject-rfc`](../reject-rfc/SKILL.md), or [`supersede-rfc`](../supersede-rfc/SKILL.md).

## Instructions

1.  **Confirm the RFC slug and category.**

    Establish a short, hyphen-delimited slug (eg. `event-sourcing-for-audit-log`). Confirm the category: `ARCHITECTURE` (system design or implementation patterns), `PROCESS` (development or operations lifecycle), `TECHNOLOGY` (production technology or infrastructure), or `TOOLING` (automation tools or devops infrastructure). If the user hasn't stated these, ask.

2.  **Create the branch.**

    ```sh
    git checkout main
    git pull
    git checkout -b rfc/<slug>
    ```

3.  **Copy the template.**

    Copy `rfcs/TEMPLATE.md` to `rfcs/<slug>.md`. Do not rename it with a numeric ID — that happens when the RFC is accepted or rejected.

4.  **Fill in the metadata header.**

    - `Authors`: The Git user's name and GitHub handle (run `git config user.name` if needed).
    - `Created` and `Last updated`: Today's date in `YYYY-MM-DD` format.
    - `Status`: `PROPOSED`.
    - Leave `Approvers`, `Approval date`, `PR`, `Discussion thread`, and `Implementation trackers` blank or as placeholders.

    Leave the prose sections as the template placeholders for the author to complete.

5.  **Commit and open a draft pull request.**

    ```sh
    git add rfcs/<slug>.md
    git commit -m "rfc: <slug>"
    git push -u origin rfc/<slug>
    gh pr create --draft --title "rfc: <slug>" --fill
    ```

6.  **Apply the category label.**

    ```sh
    gh pr edit <number> --add-label "<CATEGORY>"
    ```

    Apply exactly one category label — `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING` — matching step 1. Do not apply a lifecycle label yet: the draft PR represents work in progress, and `#proposed` is applied later by [`propose-rfc`](../propose-rfc/SKILL.md).

## Rules

-   **One RFC per branch and pull request.**

    Never bundle multiple decisions into a single branch. If the user describes changes that span multiple independent concerns, scaffold separate RFC branches.

-   **Branch from `main`, not from any other branch.**

    RFCs are always cut from `main`. If the local `main` is behind the remote, pull first.

-   **Open the PR as a draft.**

    A new RFC is not yet ready for review; it MUST be opened as a GitHub draft pull request.

-   **Do not assign a numeric ID.**

    The sequential ID is assigned on acceptance or rejection. Leave the filename as `<slug>.md`.

## Success criteria

-   **Branch `rfc/<slug>` exists and is checked out.**

-   **`rfcs/<slug>.md` exists**, a copy of `TEMPLATE.md` with the metadata header filled in and `Status: PROPOSED`.

-   **A draft pull request titled `rfc: <slug>` is open**, carrying exactly one category label and no lifecycle label.

## References

- [`rfcs/TEMPLATE.md`](../../../rfcs/TEMPLATE.md): The RFC template to copy.

- [AGENTS.md](../../../AGENTS.md): The full RFC lifecycle and conventions, written for agents.

- [`propose-rfc`](../propose-rfc/SKILL.md): Removes the draft status once the document is complete.
