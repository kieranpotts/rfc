---
name: draft-rfc
description: >-
  Draft a new RFC. Use this skill when the user wants to make a new
  architecture, process, technology, or tooling decision, or says something like
  "draft an RFC", "new RFC", or "start an RFC". Do not use this skill to write
  the body of the proposal — it only scaffolds the document.
compatibility: >-
  requires Read, Write, Edit, Bash (git, gh)
license: CC0-1.0
---

# Draft RFC

Scaffold a new RFC, ready for its author to complete and take forward to
technical stakeholders. This is the entry point to the RFC lifecycle, and it
leaves the RFC at `DRAFT`. Do not write the proposal's prose sections — that
is the author's job.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **A description of the decision to make — REQUIRED.** A one-line summary of
  the change being proposed. Prompt the user if the surrounding context does
  not supply one.

- **The RFC category — OPTIONAL.** One of architecture, process, technology,
  or tooling. Infer it from the description where the fit is obvious; ask the
  user otherwise.

## Success criteria

- Branch `rfc/<slug>` MUST exist and MUST be checked out.

- `rfc/<category>/<slug>/README.md` MUST exist, a copy of `rfc/TEMPLATE.md`
  with the metadata header filled in and its `Status` field set to `DRAFT`.

- A draft pull request titled `rfc: <short lowercase rfc description>` MUST be
  open, carrying exactly one category label and no lifecycle label.

- A discussion thread MUST be open, linked from the document's
  `Discussion thread` field and from the pull request body.

- The document's prose sections MUST still hold the template's placeholder
  text, and no RFC number MUST have been assigned.

## Instructions

1.  Determine the RFC description and slug.

    Establish a short, hyphen-delimited slug, eg.
    `event-sourcing-for-audit-log`. Derive it from what the user said about
    the decision. Prompt the user if they did not describe it.

2.  Determine the RFC category.

    Infer the category from the description, or ask the user if you're not
    sure which fits best. The options are:

    - Architecture: system design or implementation patterns.
    - Process: development or operations lifecycle concerns.
    - Technology: production technology or infrastructure.
    - Tooling: automation tools or devops infrastructure.

3.  Create the branch.

    ```sh
    git checkout main
    git pull --rebase
    git checkout -b rfc/<slug>
    ```

4.  Create the RFC from the template.

    Copy `rfc/TEMPLATE.md` to `rfc/<category>/<slug>/README.md`, where
    `<category>` is the lowercase category directory (`architecture`,
    `process`, `technology`, or `tooling`).

5.  Fill in the metadata header.

    - `Authors`: the Git user's name and GitHub handle — run
      `git config user.name` if needed.
    - `Created` and `Last updated`: today's date, in `YYYY-MM-DD` format.
    - `Status`: `DRAFT`.

    Leave the prose sections for the author to complete. Leave the remaining
    metadata fields blank for now — except `PR` and `Discussion thread`,
    which are filled in later in this procedure, once those artifacts exist.

6.  Commit and open a draft pull request.

    ```sh
    git add rfc/<category>/<slug>/
    git commit -m "draft: <short lowercase rfc description>"
    git push -u origin rfc/<slug>
    gh pr create --draft --title "rfc: <short lowercase rfc description>" --fill
    ```

    Record the returned PR number in the document's `PR` field. The readiness
    gate downstream requires that field to be set, and this is the first
    point at which the number exists.

7.  Apply the category label.

    ```sh
    gh pr edit <number> --add-label "<category>"
    ```

    Apply exactly one category label to the pull request, in full uppercase:
    `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`.

8.  Open a discussion thread.

    Every RFC pull request needs an associated discussion thread, where all
    review feedback is gathered. `gh` has no native discussion command, so
    use the GraphQL API. Look up the repository ID and the discussion
    category matching the RFC's category (`ARCHITECTURE`, `PROCESS`,
    `TECHNOLOGY`, or `TOOLING`):

    ```sh
    gh api graphql -f query='
      query($owner:String!, $name:String!) {
        repository(owner:$owner, name:$name) {
          id
          discussionCategories(first:20) { nodes { id name } }
        }
      }' -F owner=<owner> -F name=<repo>
    ```

    Create the discussion, referencing the pull request, and capture its URL:

    ```sh
    gh api graphql -f query='
      mutation($repoId:ID!, $categoryId:ID!, $title:String!, $body:String!) {
        createDiscussion(input:{repositoryId:$repoId, categoryId:$categoryId, title:$title, body:$body}) {
          discussion { url }
        }
      }' -F repoId=<repoId> -F categoryId=<categoryId> \
        -f title="rfc: <short lowercase rfc description>" \
        -f body="Discussion thread for the <short lowercase rfc description> RFC (PR #<number>). Please leave all feedback here, not on the pull request."
    ```

    Record the returned URL in the document's `Discussion thread` field, and
    add it to the pull request body, so the two cross-reference each other:

    ```sh
    gh pr edit <number> --body "$(gh pr view <number> --json body -q .body)

    Discussion thread: <discussionUrl> — Please leave all review feedback there, not on this pull request."
    ```

    Then commit and push the document change:

    ```sh
    git commit -am "chore: link discussion thread"
    git push
    ```

9.  Report what you did, and hand the document back to its author to write.

## Rules

- You SHOULD only draft an RFC for a significant decision.

  RFCs are for significant, multi-stakeholder technical decisions, not
  routine feature work, bug fixes, or trivial changes, which go through the
  normal pull-request workflow. If the request looks too small to warrant an
  RFC, say so before drafting.

- You MUST NOT bundle more than one RFC into a single branch or pull request.

  If the user describes changes that span multiple independent concerns,
  recommend drafting a separate RFC branch for each. Each RFC has to be
  reviewable, decidable, and mergeable on its own.

- You MUST branch from `main`, not from any other branch.

  RFCs are always cut from `main`. If the local `main` is behind the remote,
  pull first, rebasing to keep the history linear.

- You MUST open the pull request as a draft.

  A new RFC is not yet ready for review, and the draft status is what
  distinguishes `DRAFT` from `PROPOSED` on the remote.

- You MUST open a discussion thread for every RFC pull request.

  Open it when the pull request is opened, even though the pull request is
  still a draft, and link it from both the document and the pull request. All
  review feedback belongs in the discussion, not in the pull request's own
  comments, which are reserved for edits to the RFC artifacts.

- You MUST NOT assign an RFC number.

  Numbers are assigned in `rfc/INDEX.md` only when an RFC's pull request is
  merged into `main` — at `IMPLEMENTED` for a decision that is carried out,
  or at `REJECTED` for one that is not taken forward.

- You MUST NOT write the RFC's prose sections.

  Drafting scaffolds the document; the author supplies the motivation, the
  proposed state, the alternatives, and the trade-offs.
