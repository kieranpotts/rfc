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

3.  **Create the RFC directory from the template.**

    Copy `rfc/TEMPLATE.md` to `rfc/<category>/<slug>/README.md`, where `<category>` is the lowercase category directory (`architecture`, `process`, `technology`, or `tooling`) matching step 1. The RFC lives in its own directory, so the author can add supporting artifacts (eg. architectural diagrams) alongside the `README.md` and link them from its `References` section. Do not add a numeric ID anywhere — RFC numbers are assigned only in `rfc/INDEX.md`, at merge.

4.  **Fill in the metadata header.**

    - `Authors`: The Git user's name and GitHub handle (run `git config user.name` if needed).
    - `Created` and `Last updated`: Today's date in `YYYY-MM-DD` format.
    - `Status`: `PROPOSED`.
    - Leave `Approvers`, `Approval date`, `PR`, and `Implementation trackers` blank or as placeholders. The `Discussion thread` field is filled in at step 7.

    Leave the prose sections as the template placeholders for the author to complete.

5.  **Commit and open a draft pull request.**

    ```sh
    git add rfc/<category>/<slug>/
    git commit -m "rfc: <slug>"
    git push -u origin rfc/<slug>
    gh pr create --draft --title "rfc: <slug>" --fill
    ```

6.  **Apply the category label.**

    ```sh
    gh pr edit <number> --add-label "<CATEGORY>"
    ```

    Apply exactly one category label — `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING` — matching step 1. Do not apply a lifecycle label yet: the draft PR represents work in progress, and `#proposed` is applied later by [`propose-rfc`](../propose-rfc/SKILL.md).

7.  **Open the associated discussion thread.**

    Every RFC pull request MUST have an associated discussion thread, where all review feedback is gathered. `gh` has no native discussion command, so use the GraphQL API. Look up the repository ID and the discussion category matching the RFC's category (`Architecture`, `Process`, `Technology`, or `Tooling`):

    ```sh
    gh api graphql -f query='
      query($owner:String!, $name:String!) {
        repository(owner:$owner, name:$name) {
          id
          discussionCategories(first:20) { nodes { id name } }
        }
      }' -F owner=<owner> -F name=<repo>
    ```

    Create the discussion, referencing the PR, and capture its URL:

    ```sh
    gh api graphql -f query='
      mutation($repoId:ID!, $categoryId:ID!, $title:String!, $body:String!) {
        createDiscussion(input:{repositoryId:$repoId, categoryId:$categoryId, title:$title, body:$body}) {
          discussion { url }
        }
      }' -F repoId=<repoId> -F categoryId=<categoryId> \
        -f title="rfc: <slug>" \
        -f body="Discussion thread for the **<slug>** RFC (PR #<number>). Please leave all feedback here, not on the pull request."
    ```

    Record the returned URL in the RFC document's `Discussion thread` field and in the pull request body, then commit and push:

    ```sh
    git commit -am "rfc: link discussion thread for <slug>"
    git push
    ```

## Rules

-   **One RFC per branch and pull request.**

    Never bundle multiple decisions into a single branch. If the user describes changes that span multiple independent concerns, scaffold separate RFC branches.

-   **Branch from `main`, not from any other branch.**

    RFCs are always cut from `main`. If the local `main` is behind the remote, pull first.

-   **Open the PR as a draft.**

    A new RFC is not yet ready for review; it MUST be opened as a GitHub draft pull request.

-   **Every RFC pull request has an associated discussion thread.**

    The thread MUST be opened when the PR is opened (even as a draft) and linked from both the document and the PR. All review feedback belongs in the discussion, not in the PR's own comments.

-   **Do not assign a numeric ID.**

    RFC numbers are assigned only in `rfc/INDEX.md`, at merge. Nothing is ever renamed; the RFC stays at `rfc/<category>/<slug>/`.

## Success criteria

-   **Branch `rfc/<slug>` exists and is checked out.**

-   **`rfc/<category>/<slug>/README.md` exists**, a copy of `TEMPLATE.md` with the metadata header filled in and `Status: PROPOSED`.

-   **A draft pull request titled `rfc: <slug>` is open**, carrying exactly one category label and no lifecycle label.

-   **An associated discussion thread is open**, linked from the document's `Discussion thread` field and from the PR.

## References

- [`rfc/TEMPLATE.md`](../../../rfc/TEMPLATE.md): The RFC template to copy.

- [AGENTS.md](../../../AGENTS.md): The full RFC lifecycle and conventions, written for agents.

- [`propose-rfc`](../propose-rfc/SKILL.md): Removes the draft status once the document is complete.
