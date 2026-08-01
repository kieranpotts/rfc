---
name: propose-rfc
description: >-
  Transition an RFC from draft to proposed, ready for stakeholder review.
  Use this skill when the user says something like "propose this RFC",
  "this RFC is ready for review", "mark the RFC as ready",
  "take this RFC out of draft", "progress this RFC to the next stage", or
  "propose RFC".
license: CC0-1.0
metadata:
  interactive: yes
  preferred_model: ollama/technical-reasoning
---

# Propose RFC

Use this skill to transition an RFC from `DRAFT` to `PROPOSED`. Confirm the
document is complete, apply the `#proposed` label, and remove the pull
request's draft status so stakeholders can review it.

## Parameters

Determine the following information from the surrounding context and
environment, if possible.

- **Target — REQUIRED.** Infer the RFC from the checked-out branch
  (`rfc/<slug>`). If on `main`, list open draft pull requests and ask the
  user to choose.

## Success criteria

You will achieve the following outcomes:

<!-- The RFC document updated to `Status: PROPOSED`, the PR carrying `#proposed`
and taken out of draft. -->

- The PR is no longer a draft (`isDraft: false`).

- The `#proposed` label is applied, alongside the category label.

- `Last updated` is today's date and `Status` is `PROPOSED`.

## Instructions

1.  Identify the RFC and its PR.

    Infer the target from the current checked-out branch (`rfc/<slug>`). If
    on `main`, list all open draft pull requests and ask the user to choose:

    ```sh
    gh pr list --draft --json number,title,headRefName
    ```

    Then checkout the branch, read the RFC document
    (`rfc/<category>/<slug>/README.md`), and confirm its PR (`gh pr view
    <number> --json isDraft,labels`) if needed.

2.  Verify the rules.

    Read the document in full and check each rule. Report any failures and
    stop if unmet.

3.  Update the document.

    Set `Status` to `PROPOSED` and `Last updated` to today's date.

4.  Apply the `#proposed` label.

    ```sh
    gh pr edit <number> --add-label "#proposed"
    ```

    Leave the category label in place, eg. `ARCHITECTURE`.

5.  Remove the PR's draft status.

    ```sh
    gh pr ready <number>
    ```

6.  Commit any document changes.

    ```sh
    git commit -am "propose: <short lowercase rfc description>"
    git push
    ```

## Rules

- You MUST NOT mark a PR ready until the document is complete.

  An incomplete or boilerplate-laden proposal wastes reviewers' time. The
  completeness gate is mandatory.

- The document MUST be reasonably complete.

  Every required section contains substantive, decision-specific content.
  The decision-bearing sections are:

  - `Summary`: A concise description of the decision.
  - `Motivation`: The problem and who it affects.
  - `Impact`: `HIGH`, `MEDIUM`, or `LOW`, plus what is affected.
  - `Current state`: The status quo (or deliberately omitted for a greenfield
    decision).
  - `Proposed state`: The solution, in enough detail to evaluate.
  - `Alternatives`: At least one alternative considered.
  - `Trade-offs and risks`: An honest account of the downsides.

- There MUST be no leftover template text.

  There's no generic placeholder prose carried over from
  [`rfc/TEMPLATE.md`](../../../rfc/TEMPLATE.md). No italic placeholder prompts
  (eg. `_Describe the proposed solution..._`) and no unfilled tokens (`#...`,
  `YYYY-MM-DD`) remain in any completed section.

- The metadata header MUST be filled in.

  `Authors`, `Created`, `Last updated`, and `PR` are set. `Status` is still
  `DRAFT` at this point.

- There MUST be exactly one category label on the PR.

  `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`.

- You MUST NOT use this skill to decide the RFC.

  This skill only moves `DRAFT` → `PROPOSED`. It does not decide the RFC.
