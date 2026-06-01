---
name: propose-rfc
description: Scaffold and propose a new RFC for a significant technical decision. Use when the user wants to propose an architecture, process, technology, or tooling decision, or says "propose an RFC", "draft an RFC", "new RFC", or "start an RFC".
license: MIT
---

# Propose RFC

Use this skill to scaffold a new RFC in the `rfcs/` directory. It creates the branch, copies the template, and fills in the metadata so the proposer can focus on writing the content.

Do NOT use this skill to advance an RFC that already exists (use [`advance-rfc`](../advance-rfc/SKILL.md)), or to audit an existing RFC document (use [`audit-rfc`](../audit-rfc/SKILL.md)).

## Instructions

1.  **Confirm the RFC slug and category.**

    Establish a short, hyphen-delimited slug for the RFC (eg. `event-sourcing-for-audit-log`). Also confirm the category: `ARCHITECTURE` (a decision about system design or implementation patterns), `PROCESS` (a decision about the development or operations lifecycle), `TECHNOLOGY` (a decision about production technology or infrastructure), or `TOOLING` (a decision about automation tools or devops infrastructure). If the user hasn't stated this, ask.

2.  **Create the branch.**

    ```sh
    git checkout main
    git pull
    git checkout -b rfc/<slug>
    ```

3.  **Copy the template.**

    Copy `rfcs/TEMPLATE.md` to `rfcs/<slug>.md`. Do not rename it with a numeric ID yet — that happens at merge time.

4.  **Fill in the metadata header.**

    Populate these fields in the new RFC document:

    - `Authors`: The Git user's name and GitHub handle (run `git config user.name` if needed).
    - `Created`: Today's date in `YYYY-MM-DD` format.
    - `Last updated`: Same as `Created` initially.
    - `PR`: Leave as `#...` — the PR number is not yet known.
    - Leave `Approvers`, `Approval date`, `Discussion thread`, and `Implementation trackers` blank.

5.  **Set the status.**

    Set the `Status` field to `PROPOSED`. There is no separate draft status — an RFC still being refined is simply an open draft pull request.

6.  **Remind the proposer of next steps.**

    The proposer should open the pull request as a GitHub draft (`gh pr create --draft`), titled `rfc: <slug>`. The PR MUST carry one category label — `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING` — matching the category confirmed in step 1, plus the `#proposed` label. The PR stays a draft while the document is refined; the proposer marks it ready for review when it is ready for stakeholder review. See [AGENTS.md](../../../AGENTS.md) for the full process.

## Rules

-   **One RFC per branch and pull request.**

    Never bundle multiple decisions into a single branch. If the user describes changes that span multiple independent concerns, scaffold separate RFC branches.

-   **Branch from `main`, not from any other branch.**

    RFCs are always cut from `main`. If the local `main` is behind the remote, pull first.

-   **Do not assign a numeric ID.**

    IDs are assigned by the maintainers at merge time. Leave the filename as `<slug>.md`.

## Success criteria

-   **Branch `rfc/<slug>` exists and is checked out.**

-   **`rfcs/<slug>.md` exists** and is a copy of `TEMPLATE.md` with metadata fields populated.

-   **Status is `PROPOSED`.**

-   **The RFC's category** (`ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`) **is confirmed**, ready to apply as the PR's category label when the PR is opened.

-   **`Authors`, `Created`, and `Last updated` fields are filled in.**

## References

- [`rfcs/TEMPLATE.md`](../../../rfcs/TEMPLATE.md): The RFC template to copy.

- [AGENTS.md](../../../AGENTS.md): Full end-to-end contributing process, including the state machine and permitted transitions, written for agents.

- [`advance-rfc`](../advance-rfc/SKILL.md): Skill for advancing an RFC through its lifecycle after it is proposed.

- [`audit-rfc`](../audit-rfc/SKILL.md): Skill for auditing an RFC before advancing it to a decision.
