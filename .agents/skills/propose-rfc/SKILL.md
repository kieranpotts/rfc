---
name: propose-rfc
description: Transition an RFC from `DRAFT` to `PROPOSED`, preparing it for stakeholder review. Use this skill when the user says "propose this RFC", "this RFC is ready for review", "mark the RFC as ready", "take this RFC out of draft", or "progress this RFC".
license: MIT
---

# Propose RFC

Use this skill to transition an RFC from `DRAFT` to `PROPOSED`. Confirm the document is complete, apply the `#proposed` label, and remove the pull request's draft status so stakeholders can review it.

Do NOT use this skill to scaffold a new RFC (use [`draft-rfc`](../draft-rfc/SKILL.md)) or to advance one to a later state (use [`accept-rfc`](../accept-rfc/SKILL.md), [`implement-rfc`](../implement-rfc/SKILL.md), [`reject-rfc`](../reject-rfc/SKILL.md), or [`supersede-rfc`](../supersede-rfc/SKILL.md)).

## Transition gates: `DRAFT` → `PROPOSED`

Before removing draft status, confirm _all_ of the following. If any fails, report it and pause — do not mark the PR ready.

-   **The document is reasonably complete.**

    Every required section contains substantive, decision-specific content. The decision-bearing sections are:

    - `Summary`: A concise description of the decision.
    - `Motivation`: The problem and who it affects.
    - `Impact`: `HIGH`, `MEDIUM`, or `LOW`, plus what is affected.
    - `Current state`: The status quo (or deliberately omitted for a greenfield decision).
    - `Proposed state`: The solution, in enough detail to evaluate.
    - `Alternatives`: At least one alternative considered.
    - `Trade-offs and risks`: An honest account of the downsides.

-   **No leftover template text.**

    There's no generic placeholder prose carried over from [`rfc/TEMPLATE.md`](../../../rfc/TEMPLATE.md). No italic placeholder prompts (eg. `_Describe the proposed solution..._`) and no unfilled tokens (`#...`, `YYYY-MM-DD`) remain in any completed section.

-   **The metadata header is filled in.**

    `Authors`, `Created`, `Last updated`, and `PR` are set. `Status` is still `DRAFT` at this point.

-   **Exactly one category label on the PR.**

    `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`.

##  Instructions

1.  **Identify the RFC and its PR.**

    Infer the target from the current checked-out branch (`rfc/<slug>`). If on `main`, list all open draft pull requests and ask the user to choose:

    ```sh
    gh pr list --draft --json number,title,headRefName
    ```

    Then checkout the branch, read the RFC document (`rfc/<category>/<slug>/README.md`), and confirm its PR (`gh pr view <number> --json isDraft,labels`) if needed.

2.  **Verify the transition gates.**

    Read the document in full and check each gate. Report any failures and stop if unmet.

3.  **Update the document.**

    Set `Status` to `PROPOSED` and `Last updated` to today's date.

4.  **Apply the `#proposed` label.**

    ```sh
    gh pr edit <number> --add-label "#proposed"
    ```

    Leave the category label in place, eg. `ARCHITECTURE`.

5.  **Remove the PR's draft status.**

    ```sh
    gh pr ready <number>
    ```

6.  **Commit any document changes.**

    ```sh
    git commit -am "propose: <short lowercase rfc description>"
    git push
    ```

##  Rules

-   **Do not mark a PR ready until the document is complete.**

    An incomplete or boilerplate-laden proposal wastes reviewers' time. The completeness gate is mandatory.

-   **Forward only.**

    This skill only moves `DRAFT` → `PROPOSED`. It does not decide the RFC.

## Success criteria

- The PR is no longer a draft (`isDraft: false`).

- The `#proposed` label is applied, alongside the category label.

- `Last updated` is today's date and `Status` is `PROPOSED`.

## References

- [`AGENTS.md`](../../../AGENTS.md): The full RFC lifecycle.
