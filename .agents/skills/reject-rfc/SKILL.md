---
name: reject-rfc
description: Reject a proposed RFC — assign its sequential ID, set its status to rejected, label the PR, and prepare it for merge so the decision is preserved permanently. Use when the user says "reject this RFC", "the RFC was not approved", or advances a proposal to rejected.
license: MIT
---

# Reject RFC

Use this skill to move an RFC from **proposed** to **rejected**. A rejected RFC is not discarded — its document is merged into `main` and preserved permanently in `rfcs/` as the record of the decision and its rationale, so the same ground is not needlessly re-trodden later. Because this repository is an append-only archive (it holds no "current state" a rejected RFC would have changed), rejection is straightforward — there is nothing to revert.

Do NOT use this skill for any other transition — to accept use [`approve-rfc`](../approve-rfc/SKILL.md), to retire a superseded decision use [`supersede-rfc`](../supersede-rfc/SKILL.md).

## Transition rules (proposed → rejected)

The RFC MUST currently be `PROPOSED`. Confirm **all** of the following before rejecting. If any is unmet, report it and pause.

-   **Stakeholder review has concluded** and the decision is to reject. Do not proceed until this is explicit.
-   **The document is a complete record.** `Motivation`, `Proposed state`, `Alternatives`, and `Trade-offs and risks` are substantive — the document will be permanently archived as the record of this decision, so its rationale must stand on its own.
-   **Only maintainers may reject.** If there is any indication the current user is not a maintainer, ask for confirmation first.

## Instructions

1.  **Confirm the RFC and the decision.**

    Identify the document and PR. Confirm with the user that review is concluded and the decision is to reject.

2.  **Verify the transition rules above.**

    Report any unmet gate and stop.

3.  **Assign the sequential ID.**

    Find the highest existing numeric ID in `rfcs/`, increment by one, zero-padded to four digits, and rename:

    ```sh
    git mv rfcs/<slug>.md rfcs/<NNNN>-<slug>.md
    ```

    Rejected RFCs are numbered in the same sequence as accepted ones.

4.  **Update the document.**

    - Set `Status` to `REJECTED`.
    - Update `Last updated` to today's date.
    - Do not alter any other field as part of this change — the document's substance is immutable from this point.

5.  **Apply the label.**

    ```sh
    gh pr edit <number> --add-label "#rejected" --remove-label "#proposed"
    ```

    This swaps only the lifecycle label; leave the category label in place.

6.  **Commit.**

    ```sh
    git commit -am "rfc: reject <NNNN>-<slug>"
    ```

7.  **Prepare for merge.**

    Confirm with the user that the PR is ready to merge into `main`. Do not merge without explicit instruction.

## Rules

-   **Only maintainers may reject.** If unsure of the user's role, ask first.

-   **Never delete the RFC document.** Rejected RFCs are permanently archived as the record of the decision and its rationale.

-   **Immutable after rejection.** Once `REJECTED`, only the `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers may change. To revisit the decision, open a new RFC that supersedes this one.

-   **Do not merge without instruction.**

## Success criteria

-   **The file is renamed** `NNNN-<slug>.md` with the correct sequential ID.

-   **`Status` is `REJECTED`** and `Last updated` is today's date.

-   **The PR carries `#rejected`** (and its category label).

-   **The user has explicitly confirmed** the rejection before any changes were made.

## References

- [AGENTS.md](../../../AGENTS.md): The full RFC lifecycle, rejection path, and immutability rules.

- [`approve-rfc`](../approve-rfc/SKILL.md) / [`supersede-rfc`](../supersede-rfc/SKILL.md): The other decision transitions.
