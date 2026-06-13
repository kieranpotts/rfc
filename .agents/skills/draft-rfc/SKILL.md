---
name: draft-rfc
description: Scaffold a new RFC. Use this skill when the user wants to make a new architecture, process, technology, or tooling decision, or says "draft an RFC", "new RFC", or "start an RFC".
license: MIT
metadata:
  interactive: yes
---

# `/draft-rfc`

Use this skill to scaffold a new RFC, ready for the author to complete and take forward to technical stakeholders. This is the entry point to the RFC lifecycle. The end status of the RFC is `DRAFT`.

Do NOT use this skill to advance an existing RFC. Use [`/propose-rfc`](../propose-rfc/SKILL.md), [`/accept-rfc`](../accept-rfc/SKILL.md), [`/implement-rfc`](../implement-rfc/SKILL.md), [`/reject-rfc`](../reject-rfc/SKILL.md), or [`/supersede-rfc`](../supersede-rfc/SKILL.md) for that.

##  Instructions

1.  **Determine the RFC description and slug.**

    Establish a short, hyphen-delimited slug eg. `event-sourcing-for-audit-log`. Decide this from information provided by the user about the RFC. Prompt the user if they did not describe the RFC.

2.  **Determine the RFC topic category.**

    Infer the category from the RFC description, or ask the user if you're not sure which category fits best. The options are:

    - **Architecture**: System design or implementation patterns.
    - **Process**: Development or operations lifecycle concerns.
    - **Technology**: Production technology or infrastructure.
    - **Tooling**: Automation tools or devops infrastructure.

3.  **Create the branch.**

    ```sh
    git checkout main
    git pull
    git checkout -b rfc/<slug>
    ```

4.  **Create the RFC from the template.**

    Copy `rfc/TEMPLATE.md` to `rfc/<category>/<slug>/README.md`, where `<category>` is the lowercase category directory (`architecture`, `process`, `technology`, or `tooling`).

5.  **Fill in the metadata header.**

    - `Authors`: The Git user's name and GitHub handle – run `git config user.name` if needed.
    - `Created` and `Last updated`: Today's date in `YYYY-MM-DD` format.
    - `Status`: `DRAFT`.

    Leave other fields blank or as placeholders for now. Leave the prose sections for the author to complete.

6.  **Commit and open a draft pull request.**

    ```sh
    git add rfc/<category>/<slug>/
    git commit -m "draft: <short lowercase rfc description>"
    git push -u origin rfc/<slug>
    gh pr create --draft --title "rfc: <short lowercase rfc description>" --fill
    ```

7.  **Apply the category label.**

    ```sh
    gh pr edit <number> --add-label "<category>"
    ```

    Apply exactly one category label to the PR, full uppercase: `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`.

8.  **Open a discussion thread.**

    Every RFC pull request MUST have an associated discussion thread, where all review feedback is gathered. `gh` has no native discussion command, so use the GraphQL API. Look up the repository ID and the discussion category matching the RFC's category (`ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`):

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
        -f title="rfc: <short lowercase rfc description>" \
        -f body="Discussion thread for the **<short lowercase rfc description>** RFC (PR #<number>). Please leave all feedback here, not on the pull request."
    ```

    Record the returned URL in the RFC document's `Discussion thread` field, and add it to the pull request description, so the two cross-reference each other:

    ```sh
    gh pr edit <number> --body "$(gh pr view <number> --json body -q .body)

    Discussion thread: <discussionUrl> — Please leave all review feedback there, not on this pull request."
    ```

    Then commit and push the document change:

    ```sh
    git commit -am "chore: link discussion thread"
    git push
    ```

##  Rules

-   **An RFC is for a significant decision.**

    RFCs are for significant, multi-stakeholder technical decisions, not routine feature work, bug fixes, or trivial changes, which go through the normal pull-request workflow. If the request looks too small to warrant an RFC, say so before scaffolding.

-   **One RFC per branch and pull request.**

    Never bundle multiple decisions into a single branch. If the user describes changes that span multiple independent concerns, recommend to the user that you scaffold separate RFC branches.

-   **Branch from `main`, not from any other branch.**

    RFCs are always cut from `main`. If the local `main` is behind the remote, pull first.

-   **Open the PR as a draft.**

    A new RFC is not yet ready for review. It MUST be opened as a draft pull request.

-   **Every RFC pull request has an associated discussion thread.**

    The thread MUST be opened when the PR is opened (even as a draft) and linked from both the document and the PR. All review feedback belongs in the discussion, not in the PR's own comments.

-   **Do not assign a numeric ID.**

    RFC numbers are assigned in `rfc/INDEX.md` only when an RFC's PR is merged to `main` — at `IMPLEMENTED` for an accepted decision, or at `REJECTED` for one that is not taken forward.

## Success criteria

- Branch `rfc/<slug>` exists and is checked out.

- `rfc/<category>/<slug>/README.md` exists, a copy of `TEMPLATE.md` with the metadata header filled in and `Status: DRAFT`.

- A draft pull request titled `rfc: <short lowercase rfc description>` is open, carrying exactly one category label and no lifecycle label.

- An associated discussion thread is open, linked from the document's `Discussion thread` field and from the PR.

## References

- [`AGENTS.md`](../../../AGENTS.md): The full RFC lifecycle and conventions, written for agents.
