---
name: propose-rfc
description: >-
  Transition an RFC from draft to proposed, ready for stakeholder review.
  Use this skill when the user says something like "propose this RFC",
  "this RFC is ready for review", "mark the RFC as ready",
  "take this RFC out of draft", "progress this RFC to the next stage", or
  "propose RFC". Do not use this skill to decide an RFC.
compatibility: >-
  requires Read, Edit, Glob, Bash (git, gh)
license: CC0-1.0
---

# Propose RFC

Transition an RFC from `DRAFT` to `PROPOSED`: confirm the document is
complete, apply the `#proposed` label, and take the pull request out of draft
so stakeholders can review it. Do not accept, reject, or merge the RFC.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **Target — REQUIRED.** The RFC to propose. Infer it from the checked-out
  branch (`rfc/<slug>`). If on `main`, list the open draft pull requests and
  ask the user to choose.

## Success criteria

- The pull request MUST no longer be a draft (`isDraft: false`).

- The `#proposed` label MUST be applied, alongside the category label.

- The document's `Status` field MUST be `PROPOSED` and `Last updated` MUST be
  today's date, committed and pushed to the pull request's branch.

- The pull request MUST remain open and unmerged, carrying no `#accepted` or
  `#rejected` label — proposing solicits a decision, it does not take one.

## Instructions

1.  Identify the RFC and its pull request.

    Infer the target from the checked-out branch (`rfc/<slug>`). If on
    `main`, list the open draft pull requests and ask the user to choose:

    ```sh
    gh pr list --draft --json number,title,headRefName
    ```

    Check out the branch, then resolve the document by globbing
    `rfc/*/<slug>/README.md` — the category directory is not recoverable from
    the slug alone. Confirm the pull request's state if needed:

    ```sh
    gh pr view <number> --json isDraft,labels
    ```

2.  Verify the rules.

    Read the document in full and check each rule below. Report any failure
    and stop without changing anything.

3.  Update the document.

    Set the `Status` field to `PROPOSED` and `Last updated` to today's date.
    Change nothing else.

4.  Apply the `#proposed` label.

    ```sh
    gh pr edit <number> --add-label "#proposed"
    ```

    Leave the category label in place, eg. `ARCHITECTURE`.

5.  Take the pull request out of draft.

    ```sh
    gh pr ready <number>
    ```

6.  Commit and push the document change.

    Push as well as commit. Reviewers read the RFC's status from the remote,
    so an unpushed commit leaves the pull request still reading `DRAFT`.

    ```sh
    git commit -am "propose: <short lowercase rfc description>"
    git push
    ```

7.  Report what you did, and remind the user to request comments from the
    relevant technical stakeholders on the RFC's discussion thread.

## Rules

- You MUST NOT propose an RFC that is not currently `DRAFT`.

  Never move an RFC backwards, and never skip a state.

- The document MUST be reasonably complete before the pull request is taken
  out of draft.

  An incomplete or boilerplate-laden proposal wastes reviewers' time. Every
  decision-bearing section has to hold substantive, decision-specific
  content:

  - `Summary`: a concise description of the decision.
  - `Motivation`: the problem and who it affects.
  - `Impact`: `HIGH`, `MEDIUM`, or `LOW`, plus what is affected.
  - `Current state`: the status quo, or deliberately omitted for a greenfield
    decision.
  - `Proposed state`: the solution, in enough detail to evaluate.
  - `Alternatives`: at least one alternative considered.
  - `Trade-offs and risks`: an honest account of the downsides.

- No section MUST retain leftover template text.

  No generic placeholder prose carried over from
  [the template](../../../rfc/TEMPLATE.md) — no italic placeholder prompts
  (eg. `_Describe the proposed solution..._`) and no unfilled tokens (`#...`,
  `YYYY-MM-DD`) in any completed section.

- The metadata header MUST be filled in.

  `Authors`, `Created`, `Last updated`, and `PR` are all set. `Status` is
  still `DRAFT` at the point this skill runs.

- A discussion thread MUST already be open and linked from the document's
  `Discussion thread` field.

  Review feedback is gathered there rather than on the pull request, so the
  thread has to exist before reviewers are invited.

- There MUST be exactly one category label on the pull request:
  `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`.

- You MUST NOT decide the RFC.

  This skill moves `DRAFT` → `PROPOSED` and stops. Acceptance, rejection, and
  merging are separate transitions, taken after the review period.
