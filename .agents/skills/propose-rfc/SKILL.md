---
name: propose-rfc
description: Remove the draft status from an RFC pull request, marking it ready for stakeholder review. Use when the user says "propose this RFC", "this RFC is ready for review", "mark the RFC ready", or "take this RFC out of draft".
license: MIT
---

# Propose RFC

Use this skill to move an RFC from draft to **proposed**: confirm the document is complete, apply the `#proposed` label, and remove the pull request's draft status so stakeholders can review it.

Do NOT use this skill to scaffold a new RFC (use [`draft-rfc`](../draft-rfc/SKILL.md)) or to decide one (use [`approve-rfc`](../approve-rfc/SKILL.md), [`reject-rfc`](../reject-rfc/SKILL.md), or [`supersede-rfc`](../supersede-rfc/SKILL.md)).

## Transition rules (draft → proposed)

Before removing draft status, confirm **all** of the following. If any fails, report it and pause — do not mark the PR ready.

-   **The document is reasonably complete.** Every required section contains substantive, decision-specific content — not the generic placeholder prose carried over from `TEMPLATE.md`:
    - `Summary` — a concise description of the decision.
    - `Motivation` — the problem and who it affects.
    - `Impact` — `HIGH`, `MEDIUM`, or `LOW`, plus what is affected.
    - `Current state` — the status quo (or deliberately omitted for a greenfield decision).
    - `Proposed state` — the solution, in enough detail to evaluate.
    - `Alternatives` — at least one alternative considered.
    - `Trade-offs and risks` — an honest account of the downsides.

-   **No leftover template text.** No italic placeholder prompts (eg. `_Describe the proposed solution..._`) and no unfilled tokens (`#...`, `YYYY-MM-DD`) remain in any completed section.

-   **The metadata header is filled in.** `Authors`, `Created`, `Last updated`, and `PR` are set, and `Status` is `PROPOSED`.

-   **Exactly one category label** (`ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`) is on the PR.

## Instructions

1.  **Identify the RFC and its PR.**

    Read the RFC document (`rfc/<category>/<slug>/README.md`) and find its PR (`gh pr view <number> --json isDraft,labels` if needed).

2.  **Verify the transition rules above.**

    Read the document in full and check each gate. Report any failures and stop if unmet.

3.  **Update the document.**

    Set `Last updated` to today's date, and confirm `Status` is `PROPOSED`.

4.  **Apply the `#proposed` label.**

    ```sh
    gh pr edit <number> --add-label "#proposed"
    ```

    Leave the category label in place. (There is no `#draft` label to remove — the draft state is the pull request's own draft flag.)

5.  **Remove the draft status.**

    ```sh
    gh pr ready <number>
    ```

6.  **Commit any document change.**

    ```sh
    git commit -am "rfc: mark <slug> ready for review"
    ```

## Rules

-   **Do not mark a PR ready until the document is complete.**

    An incomplete or boilerplate-laden proposal wastes reviewers' time. The completeness gate is mandatory.

-   **Forward only.**

    This skill only moves draft → proposed. It does not decide the RFC.

## Success criteria

-   **The PR is no longer a draft** (`isDraft: false`).

-   **The `#proposed` label is applied**, alongside the category label.

-   **`Last updated` is today's date** and `Status` is `PROPOSED`.

## References

- [AGENTS.md](../../../AGENTS.md): The full RFC lifecycle.

- [`draft-rfc`](../draft-rfc/SKILL.md): Scaffolds the RFC and opens the draft PR.

- [`approve-rfc`](../approve-rfc/SKILL.md) / [`reject-rfc`](../reject-rfc/SKILL.md): Decide a proposed RFC.
